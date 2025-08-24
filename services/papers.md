# Papers Service

**URL**: https://papers.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/papers  
**Server**: 51.15.23.142 (Large, shared with Packages)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 1.0M web requests (30 days)
- **Background Jobs**: None detected
- **Uptime**: No uptime monitoring errors detected
- **Open Incidents**: 7 currently open (application logic issues)

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **PapersController#show** - 857,188 requests (84.5%)
   - Individual paper detail pages
   - Dominates all traffic by far

2. **ProjectsController#show** - 93,655 requests (9.2%)
   - Project detail pages
   - Secondary content driver

3. **Api::V1::ProjectsController#show** - 30,688 requests (3.0%)
   - Project details API
   - Primary API usage

4. **ProjectsController#index** - 30,572 requests (3.0%)
   - Project listing pages
   - Discovery endpoint

5. **PapersController#index** - 2,055 requests (0.2%)
   - Paper listing pages
   - Low usage compared to individual papers

### Low-Traffic Endpoints

- **ProjectsController#ecosystem**: 384 requests
- **ExportsController#index**: 9 requests  
- **Api::V1::PapersController#mentions**: 7 requests
- **Api::V1::PapersController#show**: 5 requests
- **Api::V1::PapersController#index**: 1 request

## Critical Issues

### =á **APPLICATION LOGIC AND TEMPLATING ISSUES**

#### **Pagination Validation Errors** (2 incidents)
- **Incident #10**: Pagy::VariableError in ProjectsController#show (68 occurrences)
- **Incident #17**: Pagy::VariableError in ProjectsController#index (1 occurrence)
- **Issue**: Page parameter validation failing (page >= 1 expected, got 0)

#### **SQL Query Security Issues** (2 incidents)  
- **Incident #16**: ActiveRecord::UnknownAttributeReference in ProjectsController#index (15 occurrences)
- **Incident #15**: ActiveRecord::UnknownAttributeReference in PapersController#index (6 occurrences)
- **Issue**: Dangerous query methods with non-attribute arguments (potential SQL injection risk)

#### **Template Missing Errors** (2 incidents)
- **Incident #18**: ActionController::UnknownFormat in Api::V1::ProjectsController#show (1 occurrence)
- **Incident #14**: ActionController::UnknownFormat in ProjectsController#show (5 occurrences)
- **Issue**: Missing templates for request format/variant handling

#### **File System Error** (1 incident)
- **Incident #7**: Errno::ENOENT in sitemap:create rake task (27 occurrences)
- **Issue**: Missing sitemap configuration file (/usr/src/app/config/sitemap.rb)

## Performance Characteristics

### =Ê **Moderate-Traffic Academic Paper Platform**
- **Focused traffic**: 1.0M requests over 30 days (~33K per day)
- **Paper-centric**: 84.5% of traffic viewing individual papers
- **No background processing**: Pure web request-driven service
- **Academic focus**: Research paper discovery and analysis platform

### **Usage Pattern**
- **Research-driven**: Heavy focus on individual paper consumption
- **Project integration**: Significant project-related traffic
- **Low API usage**: Minimal programmatic access
- **Content-heavy**: Users browsing and reading academic content

## Server Infrastructure

**Server Details**:
- **IP**: 51.15.23.142
- **Type**: Large server (shared with Packages service)
- **OS**: Ubuntu 20.04.6 LTS
- **Shared Resources**: Co-located with highest-traffic service (Packages)

**Resource Utilization**:
- **Moderate load**: 33K requests per day is reasonable load
- **Efficient sharing**: Good neighbor on shared server despite Packages crisis
- **No background overhead**: Web-only service reduces server load
- **Stable operations**: No infrastructure-level issues detected

## Background Jobs Analysis

- **Total Background Jobs**: None detected
- **Architecture**: Pure web-driven service without background processing
- **Simplicity**: No job queues, workers, or asynchronous processing complexity
- **Focus**: Direct web content delivery model

## Action Items

### =á **HIGH PRIORITY - Fix Application Logic Issues**
1. **Pagination parameter validation** - fix Pagy::VariableError when page=0 is provided
2. **SQL query security hardening** - resolve ActiveRecord::UnknownAttributeReference security issues
3. **Template completion** - add missing templates for API and web format variants
4. **Sitemap configuration** - create missing /usr/src/app/config/sitemap.rb file

### ™ **MEDIUM PRIORITY**
1. **Input validation** - comprehensive parameter validation for all controllers
2. **Error handling** - improve error responses for malformed requests
3. **API development** - expand API functionality if needed (currently minimal usage)
4. **Performance optimization** - optimize paper detail page loading (84.5% of traffic)

### =È **MONITORING**
1. **Application error monitoring** - track SQL injection attempts and pagination errors
2. **Performance monitoring** - track response times for paper detail pages
3. **Security monitoring** - monitor for malicious SQL query attempts
4. **Usage analytics** - track paper and project discovery patterns

### =Ú **FUNCTIONALITY IMPROVEMENTS**
1. **Search enhancement** - improve paper and project search capabilities
2. **API expansion** - develop more comprehensive API if demand increases
3. **Content optimization** - improve paper detail page performance and UX
4. **Integration improvements** - better project-paper relationship features

## Technical Notes

**Service Architecture**:
- **Academic paper platform**: Focus on research paper discovery and analysis
- **Simple web architecture**: No background processing complexity
- **Paper-centric design**: 84.5% traffic to individual paper pages
- **Project integration**: Significant project-related functionality

**Performance Profile**:
- **Content-heavy traffic**: Users consuming research paper content
- **Low API usage**: Primarily web-driven rather than programmatic access
- **Stable load**: Predictable academic research access patterns
- **Efficient resource usage**: Good fit for shared server environment

**Security Considerations**:
- **SQL injection risks**: ActiveRecord::UnknownAttributeReference errors indicate potential security vulnerabilities
- **Input validation**: Need better parameter validation for pagination and queries
- **Error handling**: Missing template errors suggest incomplete request handling

## Recommendations

**Status**: =á **REQUIRES ATTENTION** - Moderate-traffic service with application logic issues that need fixing, especially security-related SQL query problems.

**Priority Actions**:
1. **SECURITY**: Fix SQL query security issues (ActiveRecord::UnknownAttributeReference)
2. **STABILITY**: Resolve pagination validation errors (Pagy::VariableError)  
3. **COMPLETENESS**: Add missing templates and sitemap configuration
4. **MONITORING**: Implement security monitoring for SQL injection attempts

**Performance Focus**:
1. **Paper optimization**: Improve individual paper page performance (84.5% of traffic)
2. **Search enhancement**: Better discovery mechanisms for papers and projects
3. **Error handling**: Comprehensive input validation and error responses
4. **API development**: Consider expanding API if demand grows

**Role in Ecosystem**: Important academic research platform providing paper discovery and analysis. The service handles moderate traffic efficiently but has application logic issues that need attention, particularly around security and error handling.

This service represents a stable, focused platform that serves its academic research purpose well but requires code quality improvements to ensure security and reliability.