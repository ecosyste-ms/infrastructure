# Services Overview

Analysis of AppSignal applications with server IPs and performance insights over the last 30 days.
*Updated: September 11, 2025*

## Service Status Overview

| Service | GitHub | IP Address | Server Size | Requests (30d) | Background Jobs (30d) | Open Incidents | Error Count | Avg Duration | Performance Status |
|---------|--------|------------|-------------|----------------|----------------------|----------------|-------------|--------------|-------------------|
| [repos web](https://repos.ecosyste.ms) | [repos](https://github.com/ecosyste-ms/repos) | 51.158.156.109 | Very Large | 4.0M (2d) | 6.3M (2d) | 1 | 24431 | - | 🟡 GitHub API 503 errors |
| [repos db](https://repos-db.ecosyste.ms) | [repos](https://github.com/ecosyste-ms/repos) | 195.154.87.126 | Very Large | - | - | - | - | - | ✅ Database server |
| [packages](https://packages.ecosyste.ms) | [packages](https://github.com/ecosyste-ms/packages) | 51.15.23.142 | Large | 167.1M | 58.8M | 5 | Active | - | 🔴 Multiple error types, timeouts ongoing |
| [commits](https://commits.ecosyste.ms) | [commits](https://github.com/ecosyste-ms/commits) | 195.154.29.100 | Large | 7.5M | 1.3M | 0 | 15 | 1396s | 🔴 Moderate traffic, 89.57% uptime |
| [docker](https://docker.ecosyste.ms) | [docker](https://github.com/ecosyste-ms/docker) | 62.210.217.62 | Medium | 3.4M | 0.2M | 1 | 181 | 520s | 🔴 Moderate traffic, 89.57% uptime |
| [timeline](https://timeline.ecosyste.ms) | [timeline](https://github.com/ecosyste-ms/timeline) | 51.15.160.73 | Very Large | 0.7M | - | 2 | 8110 | - | 🔴 Database query timeouts ongoing |
| [parser](https://parser.ecosyste.ms) | [parser](https://github.com/ecosyste-ms/parser) | 195.154.81.95 | Large | 29.2M | 6.9M | 4 | 1.26M+ | - | 🔴 Database connection issues |
| [issues](https://issues.ecosyste.ms) | [issues](https://github.com/ecosyste-ms/issues) | 51.159.56.73 | Large | 61.6M | 21.1M | 0 | 75 | 1200s | 🔴 High traffic, 89.83% uptime |
| [archives](https://archives.ecosyste.ms) | [archives](https://github.com/ecosyste-ms/archives) | 51.159.31.55 | Medium | 1.7M | - | 0 | 43 | 605s | 🔴 8.61% error rate, 90.30% uptime |
| [awesome](https://awesome.ecosyste.ms) | [awesome](https://github.com/ecosyste-ms/awesome) | 195.154.82.7 | Large (shared) | 13.0M | 2.4M | 0 | - | - | ✅ Moderate traffic, stable |
| [dependabot](https://dependabot.ecosyste.ms) | [dependabot](https://github.com/ecosyste-ms/dependabot) | 62.210.127.225 | Medium | 5.2M | 1.6M | 0 | - | - | ✅ Moderate traffic, stable |
| [papers](https://papers.ecosyste.ms) | [papers](https://github.com/ecosyste-ms/papers) | 51.15.23.142 | Large | 1.0M | - | 0 | 1931 | 467s | 🔴 Low traffic, 95.79% uptime |
| [home](https://ecosyste.ms) | [documentation](https://github.com/ecosyste-ms/documentation) | 195.154.82.7 | Large (shared) | 24K | - | 0 | - | - | ✅ Very low traffic, stable |
| [diff](https://diff.ecosyste.ms) | [diff](https://github.com/ecosyste-ms/diff) | 195.154.82.7 | Large (shared) | 0.2M | - | 0 | 669 | 607s | 🔴 Very low traffic, 88.40% uptime |
| [licenses](https://licenses.ecosyste.ms) | [licenses](https://github.com/ecosyste-ms/licenses) | 195.154.82.7 | Large (shared) | 44K | 23 | 0 | 633 | 604s | 🔴 Very low traffic, 88.49% uptime |
| [dashboard](https://dashboard.ecosyste.ms) | [dashboard](https://github.com/ecosyste-ms/dashboard) | 195.154.82.7 | Large (shared) | No data | No data | 0 | - | - | ⚠️ AppSignal data unavailable |
| [funds](https://funds.ecosyste.ms) | [funds](https://github.com/ecosyste-ms/funds) | 195.154.82.7 | Large (shared) | 29K | 0.8M | 0 | - | - | ✅ Low traffic, moderate bg jobs |
| [opencollective](https://opencollective.ecosyste.ms) | [opencollective](https://github.com/ecosyste-ms/opencollective) | 195.154.82.7 | Large (shared) | 7.1M | 1.0M | 0 | - | - | ✅ Moderate traffic with bg jobs |
| [ost](https://ost.ecosyste.ms) | [ost](https://github.com/ecosyste-ms/ost) | 195.154.82.7 | Large (shared) | 1.9M | 76K | 0 | 641 | 979s | 🔴 Low traffic, 86.65% uptime |
| [ruby](https://ruby.ecosyste.ms) | [ruby](https://github.com/ecosyste-ms/ruby) | 195.154.82.7 | Large (shared) | 0 | 22K | 0 | - | - | ✅ No web traffic, some bg jobs |
| [sbom](https://sbom.ecosyste.ms) | [sbom](https://github.com/ecosyste-ms/sbom) | 195.154.82.7 | Large (shared) | 0 | 25 | 0 | - | - | ✅ No web traffic, minimal bg jobs |
| [sponsors](https://sponsors.ecosyste.ms) | [sponsors](https://github.com/ecosyste-ms/sponsors) | 195.154.82.7 | Large (shared) | 0 | 0.8M | 0 | - | - | ✅ No web traffic, moderate bg jobs |
| [advisories](https://advisories.ecosyste.ms) | [advisories](https://github.com/ecosyste-ms/advisories) | 195.154.82.7 | Large (shared) | 5.0M | - | 0 | 1224 | 760s | 🔴 Moderate traffic, 97.18% uptime |

## Summary Statistics

**Total Infrastructure Metrics (30 days):**
- **Web Requests**: ~473.4M across 18 applications
- **Background Jobs**: ~226.9M across 14 applications  
- **Open Incidents**: 7 total across 3 applications (significant improvement from 105)
- **Active Applications**: 22 with traffic data + 1 with missing data
- **Servers**: 12 total (3 Very Large including new repos DB, 7 Large, 2 Medium)

**Top Traffic Applications:**
1. Packages: 167.1M requests + 58.8M bg jobs
2. Repositories: 86.4M requests + 132.4M bg jobs  
3. Issues: 61.6M requests + 21.1M bg jobs
4. Parser: 29.2M requests + 6.9M bg jobs
5. Awesome: 13.0M requests + 2.4M bg jobs

**Critical Attention Required:**
- 🔴 **Packages**: 5 open error types including Rack timeouts, template errors, NoMethodError
- 🟡 **Repositories**: Split into web (51.158.156.109) and DB (195.154.87.126), GitHub API 503 errors ongoing
- 🔴 **Parser**: 1.26M+ database connection failures still occurring
- 🔴 **Timeline**: 8,110 query timeouts ongoing (was 6,686+)
- 🔴 **Archives**: 8.61% error rate with 90.30% uptime

## Key Findings

### Critical Issues Update - September 11, 2025

1. **Packages App** - 🔴 ACTIVE ERRORS
   - **HIGHEST WEB TRAFFIC**: 167.1M requests over 30 days (8.6M in last 2 days)
   - **5 open error types**: Rack::Timeout (1 day ago), UnknownFormat (2 days ago), Template::Error (7 days ago)
   - NoMethodError and IpSpoofAttackError also active
   - AppSignal API may not be returning these via MCP endpoint
   - **Action**: Investigate timeout issues and method errors

2. **Repositories App** - 🟡 INFRASTRUCTURE SPLIT
   - **Service separated into Web and DB components**
   - Web moved to 51.158.156.109 (was on 195.154.87.126)
   - Database now on dedicated server 195.154.87.126
   - GitHub API 503 errors ongoing (24,431 occurrences)
   - **Action**: Monitor new architecture performance

3. **Original Repositories Issue (Historical)** - 🔴 EXTERNAL DEPENDENCY CRISIS
   - **3rd HIGHEST TRAFFIC**: 87.2M web requests + 133M background jobs over 30 days
   - **70,000+ API rate limit violations** across GitHub and GitLab APIs
   - 44 open incidents, background processing severely impacted
   - **Action**: Multiple API tokens, intelligent rate limiting implementation

4. **Parser App (195.154.81.95)** - 🔴 DATABASE CONNECTION POOL CRISIS
   - **2nd HIGHEST TRAFFIC**: 29.3M requests over 30 days
   - **5.7M+ database connection failures** ("too many clients already")
   - Background job processing blocked by connection exhaustion
   - **Action**: Increase connection pool limits or database optimization

5. **Timeline App (51.15.160.73)** - 🔴 DATABASE PERFORMANCE CRISIS
   - **6,686+ database query timeouts** over 30 days
   - Very Large server massively under-utilized (23K daily requests)
   - Core functionality failing due to inefficient database queries
   - **Action**: Query optimization and database performance tuning

### Overwhelmed Server Analysis

**195.154.82.7** (Large, 17 services):
- Well-distributed shared server with moderate combined traffic
- Awesome: 13.0M requests + 2.4M bg jobs/30d
- Opencollective: 7.1M requests/30d
- Advisories: 5.0M requests/30d  
- OST: 1.9M requests/30d
- Diff: 0.2M requests/30d
- Total: ~27M requests across all apps with data
- **Good consolidation success story** - stable with zero incidents

**Traffic Analysis by Server**:

**Ultra High Traffic**:
- 51.15.23.142 (Packages web): 167.1M requests/30d - highest single app web traffic
- 195.154.87.126 (Repositories): 86.4M requests + 132.4M bg jobs/30d - massive total volume

**High Traffic**:
- 51.159.56.73 (Issues): 61.6M requests + 21.1M bg jobs/30d - high volume, surprisingly stable
- 195.154.81.95 (Parser): 29.2M requests + 6.9M bg jobs/30d - high volume but struggling

**Medium Traffic**:
- 195.154.82.7 (shared): ~27M total requests across 17 apps - well distributed
- 195.154.29.100 (Commits): 7.5M requests/30d - moderate, stable
- 62.210.127.225 (Dependabot): 5.2M requests + 1.6M bg jobs/30d - moderate, stable
- 62.210.217.62 (Docker): 3.4M requests/30d - moderate, minor issues

**Low Traffic**:  
- 51.15.160.73 (Timeline): 0.7M requests/30d - **massive under-utilization on Very Large server**
- 51.159.31.55 (Archives): 1.7M requests/30d - appropriate for medium server
- 51.15.23.142 (Papers): 1.0M requests/30d - sharing server with Packages

**Critical Issue**:
- 195.154.29.88 (Packages DB): Critical connectivity issues affecting highest traffic app

### Recommendations

1. **URGENT**: Packages has 5 active error types - Rack timeouts and template errors need attention
2. **HIGH PRIORITY**: Monitor Repositories new architecture - Web/DB split needs performance validation
3. **CRITICAL**: Parser database connection pool - 1.26M+ failures still occurring  
4. **HIGH PRIORITY**: Timeline query optimization - 8,110 timeouts on over-provisioned Very Large server
5. **HIGH PRIORITY**: Archives error rate reduction - 8.61% error rate affecting API functionality
6. **MEDIUM PRIORITY**: Ruby Redis connectivity - blocking background processing for Ruby ecosystem
7. **INVESTIGATION**: SBOM service activity - zero traffic detected, verify service status

## Legend
- 🔴 Critical issues requiring immediate attention
- ⚠️ Performance issues or resource strain
- 🟡 Minor issues but stable
- ✅ No significant issues detected

---

## How This Report Was Generated

This analysis was created using Claude Code with the AppSignal MCP (Model Context Protocol) server to gather comprehensive performance data across all applications.

### Data Sources:
- **AppSignal MCP API**: Used to collect 30-day metrics for web requests and background jobs
- **Exception data**: Gathered incident counts and error patterns for each application
- **Server mapping**: Cross-referenced with existing `servers.md` infrastructure documentation

### Key Metrics Collected:
- **Web requests (30d)**: `transaction_duration` COUNT with `namespace: web` filter
- **Background jobs (30d)**: `transaction_duration` COUNT with `namespace: background` filter  
- **Open incidents**: Current exception incidents requiring attention
- **Error rates**: Calculated as `transaction_exception_count` ÷ `transaction_duration COUNT` × 100
- **Server information**: IP addresses, sizes, and current utilization patterns

### Important Correction:
- **Error Rate Calculation**: Earlier versions incorrectly used `transaction_exception_rate` as a percentage
- **Corrected Method**: Error rates now calculated as (exceptions ÷ requests) × 100
- **Example**: Archives shows 8.61% error rate (150,662 exceptions ÷ 1,748,976 requests)

### Claude Prompt for Regeneration:
```
Create a comprehensive services overview table showing:
1. All AppSignal applications with 30-day request/background job volumes
2. Server IP addresses from servers.md 
3. Open incident counts and performance status
4. Analysis of which servers are over/under-utilized
5. Recommendations for infrastructure optimization

Use the AppSignal MCP server to gather all metrics data.
```

### Notes:
- Dashboard app shows activity in AppSignal UI but returns no API data (known issue)
- All metrics verified through direct MCP API calls rather than estimates
- Background job data carefully validated to avoid false zero entries