# OST Service

**URL**: https://ost.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/ost  
**Server**: 195.154.82.7 (Large, shared)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 1.9M web requests (30 days)
- **Background Jobs**: 77K jobs (30 days)
- **Uptime**: No uptime monitoring errors detected
- **Open Incidents**: 7 currently open (Meilisearch and Redis issues)

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **ContributorsController#show** - 841,965 requests (43.7%)
   - Individual contributor profile pages
   - Highest traffic endpoint by far

2. **CategoriesController#show** - 605,422 requests (31.5%)
   - Category/topic browsing pages
   - Major content driver

3. **ProjectsController#show** - 333,946 requests (17.4%)
   - Individual project detail pages
   - Core functionality

4. **ProjectsController#index** - 80,160 requests (4.2%)
   - Project listing and browsing
   - Main discovery endpoint

5. **Api::V1::ProjectsController#show** - 24,533 requests (1.3%)
   - API project details
   - Active API usage

### Medium-Traffic Endpoints

- **ProjectsController#search**: 20,686 requests (1.1%)
- **ReleasesController#index**: 16,232 requests (0.8%)

### Low-Traffic Endpoints

- **Api::V1::IssuesController#openclimateaction**: 607 requests
- **ProjectsController#review**: 641 requests
- **ProjectsController#packages**: 171 requests
- **IssuesController#index**: 78 requests

## Critical Issues

### **CRITICAL** **MULTIPLE SYSTEM INTEGRATION FAILURES**

#### **Meilisearch Timeout Issues** (4 open incidents)
- **Incident #78**: SyncProjectWorker timeouts (694 occurrences, most severe)
- **Incident #86**: Search controller timeouts (91 occurrences)
- **Incident #87**: API timeout errors (6 occurrences)  
- **Incident #89**: Project import timeouts (2 occurrences)
- **Impact**: Search functionality degraded, background synchronization failing

#### **Redis Connection Failure** (1 open incident)
- **Incident #66**: RedisClient::CannotConnectError
- **156 total occurrences**, blocking background job processing
- Connection refused to redis://dokku-redis-ost:6379

#### **Application Logic Errors** (2 open incidents)
- **Incident #46**: NoMethodError in CategoriesController (185 occurrences)
- **Incident #92**: NoMethodError in ReadmeParser during project imports

## Performance Characteristics

### **HIGH PRIORITY** **High-Traffic OST Platform with Integration Issues**
- **Moderate web traffic**: 1.9M requests over 30 days (~64K per day)
- **Background processing**: 77K background jobs for project synchronization
- **Contributor-focused**: 43.7% of traffic viewing contributor profiles
- **Search-dependent**: Critical reliance on Meilisearch for project discovery

### **Usage Pattern**
- **Community-driven**: Heavy focus on contributors and project categories
- **Project discovery**: Strong search and categorization functionality
- **API integration**: Active API usage for project data
- **Background synchronization**: Continuous project data updates

## Server Infrastructure

**Server Details**:
- **IP**: 195.154.82.7
- **Type**: Large server (shared with 17 other services)
- **OS**: Ubuntu 20.04.6 LTS
- **Shared Services**: Part of successful 18-service consolidation

**Resource Utilization**:
- **Moderate load**: Balanced traffic across multiple endpoints
- **Efficient sharing**: Good fit for shared server architecture
- **External dependencies**: Meilisearch and Redis connectivity issues

## Background Jobs Analysis

- **Total Background Jobs**: 76,716 jobs (30 days)
- **Job Volume**: ~2,600 jobs per day average
- **Primary Purpose**: Project synchronization, data imports, search indexing
- **Critical Issues**: 
  - Redis connectivity blocking job processing
  - Meilisearch timeouts causing sync failures
  - Project import errors in ReadmeParser

## Action Items

### **CRITICAL - Fix External Service Dependencies**
1. **Meilisearch connectivity issues** - resolve timeout errors affecting search and sync
2. **Redis connection restoration** - fix redis://dokku-redis-ost:6379 connectivity
3. **Search service optimization** - improve Meilisearch response times
4. **Background job recovery** - process backlogged synchronization jobs

### **HIGH PRIORITY**
1. **Application error fixes** - resolve NoMethodError in CategoriesController and ReadmeParser
2. **Search performance tuning** - optimize Meilisearch queries and indexing
3. **Connection pooling** - implement Redis connection pooling for reliability
4. **Error monitoring** - comprehensive alerting for external service failures

### **LOW PRIORITY**  **MEDIUM PRIORITY**
1. **Caching strategy** - reduce load on Meilisearch and database
2. **API optimization** - improve API endpoint performance
3. **Search fallbacks** - implement fallback search when Meilisearch fails
4. **Performance monitoring** - track response times for high-traffic endpoints

### **MONITORING**
1. **External service monitoring** - Meilisearch and Redis health checks
2. **Search performance tracking** - query response times and success rates
3. **Background job monitoring** - queue depth and failure rate alerts
4. **Application error tracking** - monitor NoMethodError patterns

## Technical Notes

**Service Architecture**:
- **Open Source Today (OST) platform**: Project discovery and contributor analytics
- **Search-centric**: Heavy reliance on Meilisearch for project discovery
- **Contributor-focused**: Major functionality around contributor profiles
- **Background processing**: Continuous project data synchronization

**Critical Dependencies**:
- **Meilisearch**: Essential for search functionality, currently experiencing timeouts
- **Redis**: Required for background job processing, connection issues
- **PostgreSQL**: Primary data store, appears stable

**Performance Profile**:
- **High contributor traffic**: 43.7% of requests to contributor profiles
- **Balanced endpoint usage**: Good distribution across major features
- **External service bottlenecks**: Performance limited by Meilisearch timeouts
- **Synchronization challenges**: Background jobs failing due to service issues

## Recommendations

**Status**: CRITICAL **REQUIRES ATTENTION** - External service integration failures affecting search functionality and background processing.

**Priority Actions**:
1. **CRITICAL**: Fix Meilisearch timeout issues to restore search functionality
2. **CRITICAL**: Resolve Redis connectivity for background job processing
3. **HIGH**: Fix application logic errors in core controllers
4. **MEDIUM**: Implement fallback mechanisms for external service failures

**Performance Focus**:
1. **Search optimization**: Improve Meilisearch query performance and reliability
2. **Resilience**: Add circuit breakers and fallbacks for external services
3. **Monitoring**: Comprehensive tracking of external service health
4. **Caching**: Reduce dependency on real-time external service calls

**Role in Ecosystem**: Important project discovery platform focusing on contributor analytics and open source project categorization. The service handles significant traffic but is hampered by external service integration issues that need resolution.

This service demonstrates good traffic distribution and user engagement but requires immediate attention to restore full search and background processing functionality.