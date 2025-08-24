# Advisories Service

**URL**: https://advisories.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/advisories  
**Server**: 195.154.82.7 (Large, shared)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 5.0M web requests (30 days)
- **Background Jobs**: None detected
- **Uptime**: 97.18% (1,224 uptime monitor errors)
- **Open Incidents**: 0 currently open

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **AdvisoriesController#index** - 4,556,179 requests (91.7%)
   - Primary landing page for browsing advisories

2. **Api::V1::AdvisoriesController#index** - 312,080 requests (6.3%)  
   - API endpoint for listing advisories

3. **AdvisoriesController#show** - 53,607 requests (1.1%)
   - Individual advisory detail pages

4. **HomeController#index** - 28,314 requests (0.6%)
   - Home page endpoint

5. **Api::V1::AdvisoriesController#show** - 21,266 requests (0.4%)
   - API endpoint for individual advisories

### Low-Traffic Endpoints

- **ExportsController#index**: 11 requests
- **Api::V1::AdvisoriesController#lookup**: 80 requests  
- **Api::V1::AdvisoriesController#packages**: 2 requests
- **PgHero** endpoints: Database monitoring (1-8 requests each)

## Critical Issues

### Uptime Problems
- **1,224 uptime monitoring errors** over 30 days
- **97.18% uptime** (below 99% threshold)

## Server Infrastructure

**Server Details**:
- **IP**: 195.154.82.7 
- **Type**: Large server (shared with 17 other services)
- **OS**: Ubuntu 20.04.6 LTS
- **Shared Services**: Hosting 18 total applications

**Resource Sharing**: Well-distributed load across shared server - other services on same server are stable.

## Background Jobs

- **No background job activity detected** in monitoring period
- Service appears to be purely web-request driven

## Action Items

### **HIGH PRIORITY**
1. **Uptime improvement investigation** - analyze cause of 1,224 uptime monitoring errors
2. **Service reliability enhancement** - address factors causing 2.82% downtime
3. **Error monitoring setup** - implement comprehensive error tracking
4. **Database connectivity check** - verify database connections are stable

### **MEDIUM PRIORITY**
1. **Health check endpoint** - add `/health` endpoint for better monitoring
2. **Performance profiling** - identify bottlenecks in main controller actions (91.7% traffic through index)
3. **API optimization** - improve advisories API performance (6.3% of traffic)
4. **Database query optimization** - optimize queries for advisory listing

### **LOW PRIORITY**  **MEDIUM PRIORITY**  
1. **Load testing** - determine if issues are load-related
2. **Caching strategy** - implement Redis caching for frequently accessed advisories
3. **API rate limiting** - protect against API abuse
4. **Uptime monitoring alerts** - set up alerts for <99% uptime

### **MONITORING**
1. Set up alerts for error rates >5%
2. Monitor database connection pool utilization  
3. Track response time percentiles (P95, P99)
4. Set up uptime monitoring thresholds

## Recommendations

**Status**: CRITICAL **UPTIME RELIABILITY ISSUES** - Service experiencing availability problems with 97.18% uptime affecting user access.

**Priority Actions**:
1. **Uptime improvement**: Address 1,224 monitoring errors causing 2.82% downtime
2. **Performance optimization**: Improve advisories index endpoint handling 91.7% of traffic
3. **Reliability enhancement**: Implement better error handling and recovery mechanisms
4. **Monitoring improvements**: Better tracking of service availability and performance

**Role in Ecosystem**: Important security service providing vulnerability advisory data for the open source ecosystem. The 97.18% uptime needs improvement to ensure reliable access to critical security information.