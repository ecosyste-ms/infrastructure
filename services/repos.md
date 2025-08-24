# Repositories Service

**URL**: https://repos.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/repos  
**Server**: 195.154.87.126 (Very Large, dedicated)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 87.2M web requests (30 days) - **3rd HIGHEST TRAFFIC SERVICE**
- **Background Jobs**: 133.0M jobs (30 days) - **HIGHEST BACKGROUND PROCESSING**
- **Uptime**: No uptime monitoring errors detected
- **Open Incidents**: 44 currently open - **MASSIVE EXTERNAL API RATE LIMITING**

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **Api::V1::RepositoriesController#lookup** - 23,550,688 requests (27.0%)
   - Repository lookup API
   - Highest single endpoint in service

2. **RepositoriesController#show** - 13,550,917 requests (15.5%)
   - Repository detail web pages
   - Major web interface traffic

3. **RepositoriesController#readme** - 8,410,514 requests (9.6%)
   - README file viewing
   - High-value content endpoint

4. **Api::V1::RepositoriesController#show** - 7,942,380 requests (9.1%)
   - Repository details API

5. **RepositoriesController#dependencies** - 7,349,965 requests (8.4%)
   - Repository dependency analysis
   - Core functionality

### High-Traffic Endpoints

- **Api::V1::OwnersController#show**: 5,613,560 requests (6.4%)
- **Api::V1::RepositoriesController#sbom**: 3,350,051 requests (3.8%)
- **Api::V1::RepositoriesController#ping**: 3,045,381 requests (3.5%)
- **Api::V1::TagsController#index**: 2,600,913 requests (3.0%)
- **Api::V1::OwnersController#repositories**: 2,314,188 requests (2.7%)

### Medium-Traffic Endpoints

- **RepositoriesController#releases**: 1,781,624 requests (2.0%)
- **HostsController#topic**: 1,585,293 requests (1.8%)
- **TopicsController#show**: 1,253,129 requests (1.4%)
- **OwnersController#show**: 1,093,196 requests (1.3%)
- **Api::V1::ReleasesController#index**: 948,348 requests (1.1%)

## Critical Issues

### **CRITICAL** **MASSIVE EXTERNAL API RATE LIMITING CRISIS**
**Over 100,000 API Rate Limit Violations Across GitHub and GitLab**

#### **GitHub API Rate Limiting** (Multiple severe incidents)
- **Incident #102**: GitHub rate limit exceeded (13,418 occurrences) - SyncRepositoryWorker
- **Incident #101**: GitHub rate limit exceeded (5,625 occurrences) - UpdateRepositoryWorker
- **Incident #437**: GitHub rate limit exceeded (76 occurrences) - DownloadTagsWorker
- **Incident #172**: GitHub rate limit exceeded (3,321 occurrences) - SyncExtraDetailsWorker
- **Incident #171**: GitHub rate limit exceeded (349 occurrences) - SyncOwnerWorker
- **Total GitHub rate limits**: **22,789+ occurrences**

#### **GitLab API Rate Limiting** (Most severe incidents)
- **Incident #275**: GitLab rate limit exceeded (30,958 occurrences) - SyncOwnerWorker
- **Incident #42**: GitLab rate limit exceeded (16,299 occurrences) - SyncRepositoryWorker
- **Incident #72**: GitLab rate limit exceeded (26 occurrences) - UpdateRepositoryWorker
- **Total GitLab rate limits**: **47,283+ occurrences**

#### **External Service Failures** (Additional critical issues)
- **Incident #154**: GitHub Service Unavailable (33,294 occurrences)
- **Incident #178**: GitHub Service Unavailable (21,235 occurrences) 
- **Incident #176**: GitHub Service Unavailable (24,413 occurrences)
- **Incident #320**: GitLab Service Unavailable (1,187 occurrences)
- **Incident #186**: GitHub Unauthorized (9,137 occurrences)

#### **Additional Severe Issues**
- **Incident #124**: NoMethodError (125,700 occurrences) - GitLab data processing failures
- **Incident #38**: Faraday middleware errors (19,689 occurrences)
- **Database constraint violations**: 572 occurrences of null value violations
- **External connectivity failures**: Connection refused, SSL errors, timeouts

## Performance Characteristics

### **CRITICAL** **ULTRA-HIGH VOLUME SERVICE CRIPPLED BY EXTERNAL DEPENDENCIES**
- **Massive scale**: 87.2M web requests + 133M background jobs (3rd highest traffic, highest background processing)
- **Repository-centric**: Core infrastructure for repository data and analysis
- **External API dependent**: Heavy reliance on GitHub, GitLab, and other Git hosting APIs
- **Rate limit crisis**: Over 70,000 API rate limit violations blocking core functionality

### **Usage Pattern** (When Functional)
- **Repository analytics platform**: Central hub for repository metadata and analysis
- **API-heavy**: 60%+ traffic through API endpoints for integrations
- **Content-driven**: High traffic to README, dependencies, releases
- **Background synchronization**: Massive background processing for repository data updates

## Server Infrastructure

**Server Details**:
- **IP**: 195.154.87.126
- **Type**: Very Large server (dedicated)
- **OS**: Ubuntu 20.04.6 LTS
- **Dedicated Resources**: Largest server type, dedicated to repositories service

**Resource Implications**:
- **Ultra-high scale**: 87.2M web requests + 133M background jobs require massive resources
- **Very large server justified**: Handles highest background processing load in infrastructure
- **External API bottleneck**: Server resources available but blocked by external rate limits
- **Dedicated architecture**: Single-service deployment for maximum performance

## Background Jobs Analysis

- **Total Background Jobs**: 132,967,257 jobs (30 days)
- **Job Volume**: ~4.43M jobs per day average (**HIGHEST IN INFRASTRUCTURE**)
- **Primary Workers**: 
  - SyncRepositoryWorker (repository synchronization)
  - UpdateRepositoryWorker (repository updates)
  - SyncOwnerWorker (owner/organization synchronization)
  - SyncExtraDetailsWorker (detailed repository analysis)
- **Status**: **SEVERELY IMPACTED** by external API rate limiting
- **Critical Impact**: 70,000+ rate limit failures blocking background processing

## Action Items

### **CRITICAL** **EMERGENCY RESPONSE (Critical External API Crisis)**
1. **IMMEDIATE**: GitHub API rate limit quota emergency increase
2. **CRITICAL**: GitLab API rate limit quota emergency increase
3. **URGENT**: Implement API rate limiting backoff and queuing strategies
4. **EMERGENCY**: API credential rotation and scaling (multiple API keys)
5. **ESCALATE**: This affects the 3rd highest traffic service with highest background processing

### **CRITICAL** **API RATE LIMITING MITIGATION**
1. **Multiple API tokens deployment** - spread load across multiple GitHub/GitLab API keys
2. **Intelligent rate limiting** - implement exponential backoff and queue management
3. **API call optimization** - reduce unnecessary API calls and batch requests
4. **Background job throttling** - implement job rate limiting to stay within API quotas
5. **Caching strategy** - cache repository data to reduce external API dependencies

### **HIGH PRIORITY** **POST-MITIGATION PRIORITIES**
1. **API monitoring implementation** - track API usage against quotas in real-time
2. **Background job optimization** - prioritize critical vs. non-critical updates
3. **Error handling improvement** - graceful degradation when APIs are unavailable
4. **Performance monitoring** - track external API response times and success rates

### **LOW PRIORITY**  **INFRASTRUCTURE IMPROVEMENTS**
1. **API federation** - distribute load across multiple Git hosting providers
2. **Data freshness tiers** - different update frequencies for different data types
3. **Circuit breakers** - automatic fallback when external APIs fail
4. **Queue management** - intelligent background job scheduling and prioritization

## Technical Notes

**Service Architecture**:
- **Repository metadata platform**: Central hub for repository analysis and data aggregation
- **External API dependent**: Heavy integration with GitHub, GitLab, Bitbucket APIs
- **Background-heavy**: Massive background processing for continuous repository synchronization
- **Multi-host support**: Handles repositories from multiple Git hosting providers

**Critical Infrastructure Role**:
- **3rd highest traffic service**: 87.2M requests over 30 days
- **Highest background processing**: 133M jobs over 30 days
- **Repository backbone**: Essential for repository metadata across ecosystem
- **Integration hub**: Provides repository data to other services

**External Dependencies**:
- **GitHub API**: Primary dependency with severe rate limiting
- **GitLab API**: Secondary dependency also hitting rate limits  
- **Bitbucket API**: Additional hosting provider integration
- **Multiple Git hosts**: Various Git hosting provider APIs

## Recommendations

**Status**: CRITICAL **CRITICAL EXTERNAL DEPENDENCY CRISIS** - The 3rd highest-traffic service with highest background processing is severely impacted by external API rate limiting across GitHub and GitLab.

**Emergency Response Protocol**:
1. **IMMEDIATE**: API quota negotiations with GitHub and GitLab
2. **CRITICAL**: Multiple API token deployment for load distribution
3. **URGENT**: Background job throttling to respect rate limits
4. **ESCALATE**: Infrastructure team coordination for API scaling

**API Rate Limiting Recovery**:
1. Multiple GitHub and GitLab API tokens (immediate)
2. Intelligent rate limiting with exponential backoff
3. Background job queue management and prioritization
4. API call optimization and unnecessary request elimination
5. Comprehensive API usage monitoring and alerting

**Future Architecture**:
1. **API federation**: Reduce single-point-of-failure on GitHub/GitLab APIs
2. **Caching layer**: Aggressive caching to reduce external API dependencies
3. **Data freshness tiers**: Different update frequencies for critical vs. non-critical data
4. **Circuit breakers**: Automatic fallback mechanisms for API failures

**Impact Assessment**: This represents a critical external dependency crisis affecting the repository backbone of the Ecosyste.ms infrastructure. The 87.2M+ monthly requests and 133M+ background jobs make this service essential for repository analysis across the entire platform. The 70,000+ API rate limit violations indicate systematic issues with external API integration that require immediate architectural changes.

The service's role as the central repository metadata hub demands immediate API scaling and intelligent rate limiting implementation to restore full functionality and prevent future API quota exhaustion.