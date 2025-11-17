# ClickHouse Query Guide for APISIX Access Logs

This guide provides useful queries for analyzing APISIX access logs stored in ClickHouse.

## Prerequisites

You'll need SSH access to the server and permission to query the ClickHouse database.

## Getting Started

### SSH to the Server

```bash
ssh deploy@195.154.80.114
```

### Connect to ClickHouse

```bash
clickhouse-client --port 9500 --password
```

You'll be prompted for the password.

### View Available Databases

```sql
SHOW DATABASES;
```

### View Tables

```sql
SHOW TABLES FROM apisix_logs;
```

### View Table Schema

```sql
DESCRIBE TABLE apisix_logs.access_logs_v2;
```

Or get the full CREATE statement:

```sql
SHOW CREATE TABLE apisix_logs.access_logs_v2;
```

## Available Columns

The `access_logs_v2` table contains:
- `timestamp` (Float64) - Unix timestamp
- `route_id` (LowCardinality(String))
- `host` (LowCardinality(String)) - Service domain
- `real_ip` (String) - Client IP address
- `country` (LowCardinality(String))
- `method` (LowCardinality(String)) - HTTP method (GET, POST, etc.)
- `uri` (String) - Request path
- `status` (UInt16) - HTTP status code
- `latency` (Float32) - Request latency in ms
- `upstream_latency` (Float32) - Backend latency in ms
- `user_agent` (String)
- `cache_status` (LowCardinality(String))
- `api_key` (LowCardinality(String)) - API key used (Note: internal ecosyste.ms services use their service name as the API key, e.g., "repos.ecosyste.ms")
- `from_header` (String)

**Note:** Internal ecosyste.ms services identify themselves using their service name as both the `user_agent` and `api_key`. For example, `repos.ecosyste.ms` will have:
- `user_agent` = "repos.ecosyste.ms"
- `api_key` = "repos.ecosyste.ms"

To filter out internal service traffic in your queries:
```sql
WHERE user_agent NOT LIKE '%.ecosyste.ms'
```

## Basic Queries

### Count Total Requests

```sql
SELECT count() as total_requests
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR);
```

### Requests by Status Code

```sql
SELECT
    status,
    count() as count,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY status
ORDER BY count DESC;
```

### Top Services by Traffic

```sql
SELECT
    host,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY host
ORDER BY requests DESC
LIMIT 20;
```

### Top User Agents

```sql
SELECT
    user_agent,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY user_agent
ORDER BY requests DESC
LIMIT 20;
```

## Traffic Analysis

### Hourly Request Volume

```sql
SELECT
    toStartOfHour(toDateTime(toUInt64(timestamp))) as hour,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY hour
ORDER BY hour DESC;
```

### Daily Request Volume

```sql
SELECT
    toDate(toDateTime(toUInt64(timestamp))) as date,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 30 DAY)
GROUP BY date
ORDER BY date DESC;
```

### Top IPs by Request Count

```sql
SELECT
    real_ip,
    country,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY real_ip, country
ORDER BY requests DESC
LIMIT 30;
```

### Traffic by Country

```sql
SELECT
    country,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY country
ORDER BY requests DESC
LIMIT 20;
```

## Status Code Analysis

### Status Code Distribution by Service

```sql
SELECT
    host,
    count() as total_requests,
    formatReadableQuantity(count()) as readable,
    round(countIf(status >= 200 AND status < 300) * 100.0 / count(), 2) as pct_success_2xx,
    round(countIf(status >= 300 AND status < 400) * 100.0 / count(), 2) as pct_redirect_3xx,
    round(countIf(status = 404) * 100.0 / count(), 2) as pct_404,
    round(countIf(status = 429) * 100.0 / count(), 2) as pct_429_rate_limit,
    round(countIf(status >= 500) * 100.0 / count(), 2) as pct_server_error_5xx
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY host
ORDER BY total_requests DESC
LIMIT 20;
```

### Top 404 URLs

```sql
SELECT
    host,
    uri,
    count() as not_found_count,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND status = 404
GROUP BY host, uri
ORDER BY not_found_count DESC
LIMIT 30;
```

### Top 500 Errors

```sql
SELECT
    host,
    uri,
    count() as errors_500,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND status = 500
GROUP BY host, uri
ORDER BY errors_500 DESC
LIMIT 30;
```

## Rate Limiting Analysis

### Rate Limit Rejections Over Time

```sql
SELECT
    toStartOfHour(toDateTime(toUInt64(timestamp))) as hour,
    count() as rate_limited,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND status = 429
GROUP BY hour
ORDER BY hour DESC;
```

### Top IPs Getting Rate Limited

```sql
SELECT
    real_ip,
    country,
    count() as rate_limited,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND status = 429
GROUP BY real_ip, country
ORDER BY rate_limited DESC
LIMIT 30;
```

### User Agents Getting Rate Limited

```sql
SELECT
    user_agent,
    count() as total_requests,
    countIf(status = 429) as rate_limited,
    formatReadableQuantity(countIf(status = 429)) as readable,
    round(countIf(status = 429) * 100.0 / count(), 2) as pct_rate_limited
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY user_agent
HAVING rate_limited > 1000
ORDER BY rate_limited DESC
LIMIT 20;
```

## Performance Analysis

### Latency Percentiles

```sql
SELECT
    host,
    count() as requests,
    round(quantile(0.50)(latency), 2) as p50_latency_ms,
    round(quantile(0.95)(latency), 2) as p95_latency_ms,
    round(quantile(0.99)(latency), 2) as p99_latency_ms,
    round(max(latency), 2) as max_latency_ms
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND status != 429
GROUP BY host
ORDER BY requests DESC
LIMIT 20;
```

### Slowest Endpoints

```sql
SELECT
    host,
    uri,
    count() as requests,
    round(avg(latency), 2) as avg_latency_ms,
    round(quantile(0.95)(latency), 2) as p95_latency_ms
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY host, uri
HAVING requests > 100
ORDER BY avg_latency_ms DESC
LIMIT 30;
```

## User Agent Analysis

### User Agent 404 Patterns

```sql
SELECT
    user_agent,
    count() as total_requests,
    countIf(status = 404) as not_found,
    formatReadableQuantity(countIf(status = 404)) as readable,
    round(countIf(status = 404) * 100.0 / count(), 2) as pct_404
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 7 DAY)
AND status != 429
AND status < 500
GROUP BY user_agent
HAVING not_found > 10000
ORDER BY not_found DESC
LIMIT 30;
```

### Specific User Agent Analysis

```sql
SELECT
    toDate(toDateTime(toUInt64(timestamp))) as date,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    countIf(status = 200) as status_200,
    countIf(status = 304) as status_304,
    countIf(status = 404) as status_404,
    countIf(status = 429) as status_429,
    countIf(status = 500) as status_500
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 30 DAY)
AND user_agent = 'your-user-agent-here'
GROUP BY date
ORDER BY date DESC;
```

## HTTP Method Analysis

### Method Distribution

```sql
SELECT
    method,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    round(count() * 100.0 / sum(count()) OVER (), 2) as pct_of_total
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY method
ORDER BY requests DESC;
```

### POST Requests by Status

```sql
SELECT
    host,
    status,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND method = 'POST'
GROUP BY host, status
ORDER BY requests DESC
LIMIT 30;
```

## API Key / Consumer Analysis

### Top API Keys by Usage

```sql
SELECT
    api_key,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips,
    countIf(status = 429) as rate_limited
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
AND api_key != ''
GROUP BY api_key
ORDER BY requests DESC
LIMIT 20;
```

### API Key vs Anonymous Traffic

```sql
SELECT
    if(api_key != '', 'API Key', 'Anonymous') as user_type,
    count() as requests,
    formatReadableQuantity(count()) as readable,
    round(count() * 100.0 / sum(count()) OVER (), 2) as percentage
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY user_type;
```

## Traffic Distribution Analysis

### Request Distribution by IP

```sql
-- How many IPs make how many requests?
SELECT
    CASE
        WHEN requests_per_ip = 1 THEN '1 request'
        WHEN requests_per_ip <= 10 THEN '2-10 requests'
        WHEN requests_per_ip <= 100 THEN '11-100 requests'
        WHEN requests_per_ip <= 1000 THEN '101-1K requests'
        WHEN requests_per_ip <= 10000 THEN '1K-10K requests'
        WHEN requests_per_ip <= 100000 THEN '10K-100K requests'
        ELSE '>100K requests'
    END as request_bucket,
    count() as num_ips,
    sum(requests_per_ip) as total_requests_in_bucket,
    formatReadableQuantity(sum(requests_per_ip)) as readable,
    round(sum(requests_per_ip) * 100.0 / sum(sum(requests_per_ip)) OVER (), 2) as pct_of_traffic
FROM (
    SELECT
        real_ip,
        count() as requests_per_ip
    FROM apisix_logs.access_logs_v2
    WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
    GROUP BY real_ip
)
GROUP BY request_bucket
ORDER BY total_requests_in_bucket DESC;
```

### Traffic Concentration

```sql
-- What % of traffic comes from top N IPs?
WITH ip_requests AS (
    SELECT
        real_ip,
        count() as requests
    FROM apisix_logs.access_logs_v2
    WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
    GROUP BY real_ip
),
total_traffic AS (
    SELECT count() as total
    FROM apisix_logs.access_logs_v2
    WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
)
SELECT
    'Top 10 IPs' as segment,
    sum(requests) as requests,
    round(sum(requests) * 100.0 / (SELECT total FROM total_traffic), 2) as pct_of_traffic
FROM (SELECT requests FROM ip_requests ORDER BY requests DESC LIMIT 10)
UNION ALL
SELECT
    'Top 100 IPs',
    sum(requests),
    round(sum(requests) * 100.0 / (SELECT total FROM total_traffic), 2)
FROM (SELECT requests FROM ip_requests ORDER BY requests DESC LIMIT 100);
```

## Advanced Queries

### Compare Time Periods

```sql
SELECT
    'Last 24 hours' as period,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
UNION ALL
SELECT
    'Previous 24 hours' as period,
    count() as requests,
    formatReadableQuantity(count()) as readable
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 48 HOUR)
AND timestamp < toUnixTimestamp(now() - INTERVAL 24 HOUR);
```

### Find Repeated 404 Requests

```sql
-- URLs getting 404s repeatedly (potential bugs or attacks)
SELECT
    host,
    uri,
    user_agent,
    count() as requests_404,
    formatReadableQuantity(count()) as readable,
    uniq(real_ip) as unique_ips
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 7 DAY)
AND status = 404
GROUP BY host, uri, user_agent
HAVING requests_404 > 100
ORDER BY requests_404 DESC
LIMIT 30;
```

### Identify Potential Bot Traffic

```sql
SELECT
    real_ip,
    country,
    user_agent,
    count() as total_requests,
    formatReadableQuantity(count()) as readable,
    round(count() / 24, 0) as avg_requests_per_hour,
    countIf(status = 429) as rate_limited,
    round(countIf(status = 429) * 100.0 / count(), 2) as rate_limit_pct
FROM apisix_logs.access_logs_v2
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
GROUP BY real_ip, country, user_agent
HAVING total_requests > 10000
ORDER BY total_requests DESC
LIMIT 30;
```

## Tips

### Working with Timestamps

The `timestamp` field is stored as Float64 (Unix timestamp). Convert it for readability:

```sql
-- To DateTime
toDateTime(toUInt64(timestamp))

-- To Date
toDate(toDateTime(toUInt64(timestamp)))

-- To Hour
toStartOfHour(toDateTime(toUInt64(timestamp)))

-- Filter by time range
WHERE timestamp >= toUnixTimestamp(now() - INTERVAL 24 HOUR)
```

### Formatting Large Numbers

Use `formatReadableQuantity()` for human-readable numbers:

```sql
SELECT formatReadableQuantity(1234567) -- Returns "1.23 million"
```

### Percentiles for Performance

Use `quantile()` for percentile calculations:

```sql
quantile(0.50)(latency)  -- Median (p50)
quantile(0.95)(latency)  -- p95
quantile(0.99)(latency)  -- p99
```

### Filtering Out Noise

Exclude rate limits and server errors for cleaner analysis:

```sql
WHERE status != 429 AND status < 500
```

## Common Time Intervals

- Last hour: `INTERVAL 1 HOUR`
- Last 24 hours: `INTERVAL 24 HOUR`
- Last 7 days: `INTERVAL 7 DAY`
- Last 30 days: `INTERVAL 30 DAY`

## Performance Considerations

- ClickHouse is optimized for analytical queries on large datasets
- Use `LIMIT` to avoid overwhelming output
- Filter by time range early in the query for better performance
- The `timestamp` column is indexed for fast time-based queries
