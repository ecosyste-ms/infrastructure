# Parser Service

**URL**: https://parser.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/parser  
**Server**: 195.154.81.95 (Large, dedicated)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 29.3M web requests (30 days) - **2nd HIGHEST TRAFFIC SERVICE**
- **Background Jobs**: 6.9M jobs (30 days) - **2nd HIGHEST BACKGROUND PROCESSING**
- **Uptime**: No uptime monitoring errors detected
- **Open Incidents**: 5 currently open - **MASSIVE DATABASE CONNECTION CRISIS**

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **Api::V1::JobsController#show** - 22,355,810 requests (76.2%)
   - Job status/result API
   - Dominates all traffic by far
   - **MOST CRITICAL ENDPOINT**

2. **Api::V1::JobsController#create** - 6,935,891 requests (23.7%)
   - Job submission API
   - Second highest traffic endpoint

3. **HomeController#index** - 45,233 requests (0.2%)
   - Landing page
   - Minimal web interface usage

### Low-Traffic Endpoints

- **PgHero database monitoring**: 26 total requests across all endpoints
- **Api::V1::JobsController#formats**: 5 requests
- **Api::V1::JobsController#index**: 1 request

## Critical Issues

### **CRITICAL** **CATASTROPHIC DATABASE CONNECTION FAILURE**
**Complete Database Connectivity Crisis with 5.7M+ Connection Failures**

#### **Most Severe Database Issues**
- **Incident #7**: ActiveRecord::ConnectionNotEstablished (4,479,511 occurrences)
  - "too many clients already" - **DATABASE CONNECTION POOL EXHAUSTED**
  - Background worker ParseDependenciesWorker completely blocked
  - 808 recent occurrences as of August 11

- **Incident #10**: ActiveRecord::ConnectionNotEstablished (1,255,208 occurrences) 
  - "database system is starting up" - **DATABASE RESTART LOOPS**
  - Api::V1::JobsController#show failing constantly
  - 10 recent occurrences as of August 23

#### **Additional Critical Issues**
- **Database server instability**: Connection failures indicate server under extreme stress
- **Connection pool exhaustion**: "too many clients already" suggests inadequate connection limits
- **Database restart cycles**: "system is starting up" indicates repeated database restarts

#### **Secondary Issues**
- **Incident #19**: AbstractController::ActionNotFound (69 occurrences) - missing controller actions
- **Incident #15**: ActionController::InvalidAuthenticityToken (8 occurrences) - HTTPS/HTTP mismatch
- **Incident #54**: ActiveRecord::ConnectionFailed (19 occurrences) - admin-terminated connections

## Performance Characteristics

### **CRITICAL** **HIGH-VOLUME API SERVICE IN TOTAL DATABASE FAILURE**
- **Massive API traffic**: 29.3M requests over 30 days (~978K per day)
- **API-only architecture**: 99.8% traffic through job management APIs
- **Background-heavy processing**: 6.9M background jobs for parsing operations
- **Complete system failure**: Database connectivity crisis affecting all functionality

### **Usage Pattern** (When Functional)
- **Parser-as-a-Service**: External services submitting parsing jobs
- **Job management focused**: Create jobs (23.7%) and check status (76.2%)
- **Minimal web interface**: API-first design with minimal UI
- **High-frequency polling**: Status checking dominates traffic

## Server Infrastructure

**Server Details**:
- **IP**: 195.154.81.95
- **Type**: Large server (dedicated)
- **OS**: Ubuntu 20.04.6 LTS
- **Dedicated Resources**: Full server for parser service

**Database Crisis**:
- **Database Server**: 172.17.0.2:5432 (PostgreSQL)
- **Status**: **SEVERE INSTABILITY**
- **Connection pool**: Completely exhausted ("too many clients already")
- **Database restarts**: Frequent restart cycles causing "system is starting up" errors
- **Impact**: Total service failure

**Resource Implications**:
- **Massive scale**: 29.3M web requests + 6.9M background jobs require significant resources
- **Database overload**: Connection pool cannot handle combined API + background job load
- **Dedicated server stressed**: Even dedicated large server struggling with database connectivity

## Background Jobs Analysis

- **Total Background Jobs**: 6,933,143 jobs (30 days)
- **Job Volume**: ~231K jobs per day average (**2nd HIGHEST IN INFRASTRUCTURE**)
- **Primary Worker**: ParseDependenciesWorker (dependency parsing)
- **Status**: **COMPLETELY BLOCKED** by database connection exhaustion
- **Critical Impact**: 4.4M+ connection failures in background processing alone

## Action Items

### **CRITICAL** **EMERGENCY RESPONSE (Critical System Failure)**
1. **IMMEDIATE**: Database connection pool emergency expansion
2. **CRITICAL**: PostgreSQL server stability investigation (172.17.0.2)
3. **URGENT**: Database connection limits analysis and tuning
4. **EMERGENCY**: Implement database connection pooling (PgBouncer)
5. **ESCALATE**: This affects the 2nd highest traffic service in infrastructure

### **CRITICAL** **DATABASE CONNECTION POOL CRISIS**
1. **PostgreSQL max_connections increase** - expand connection limits immediately
2. **Connection pooling implementation** - deploy PgBouncer or similar
3. **Background job throttling** - reduce concurrent job processing temporarily
4. **Database server resource analysis** - check CPU, memory, disk I/O
5. **Connection leak detection** - identify and fix connection leaks

### **HIGH PRIORITY** **POST-RECOVERY PRIORITIES**
1. **Monitoring implementation** - comprehensive database connection monitoring
2. **Performance optimization** - optimize high-frequency job status queries
3. **Connection management** - implement proper connection lifecycle management
4. **Load balancing** - consider database read replicas for status queries

### **LOW PRIORITY**  **INFRASTRUCTURE IMPROVEMENTS**
1. **Database scaling** - implement read replicas for status queries
2. **Connection pooling** - permanent PgBouncer deployment
3. **Caching strategy** - cache job status to reduce database load
4. **Background job optimization** - batch processing and queue management

## Technical Notes

**Service Architecture**:
- **Parser-as-a-Service platform**: Processes dependency files for package analysis
- **API-first design**: 99.8% traffic through job management APIs
- **Background-heavy**: Massive background processing for parsing operations
- **High-frequency polling**: Status checking creates enormous database load

**Critical Infrastructure Role**:
- **2nd highest traffic service**: 29.3M requests over 30 days
- **2nd highest background processing**: 6.9M jobs over 30 days
- **Core dependency**: Essential for package dependency analysis across ecosystem
- **API service hub**: Other services likely depend heavily on parser results

**Database Dependency**:
- **Single point of failure**: Complete reliance on 172.17.0.2 PostgreSQL server
- **Connection pool exhaustion**: Database cannot handle combined API + background load
- **High-frequency queries**: Status checking creates extreme database pressure
- **No redundancy**: No apparent failover or read replicas

## Recommendations

**Status**: CRITICAL **TOTAL SYSTEM FAILURE - EMERGENCY RESPONSE REQUIRED** - The 2nd highest-traffic service is completely non-functional due to database connection pool exhaustion.

**Emergency Response Protocol**:
1. **IMMEDIATE**: Database connection pool emergency expansion
2. **CRITICAL**: PostgreSQL server stability restoration
3. **URGENT**: Background job processing recovery (231K jobs per day)
4. **ESCALATE**: Infrastructure team emergency response for 2nd highest traffic service

**Database Recovery Priority**:
1. PostgreSQL max_connections increase (immediate)
2. PgBouncer connection pooling deployment
3. Database server resource optimization
4. Connection leak identification and fixes
5. Background job queue management

**Future Architecture**:
1. **Database read replicas**: Separate read traffic from write operations
2. **Connection pooling**: Permanent PgBouncer infrastructure
3. **Caching layer**: Redis caching for frequent job status queries
4. **Load distribution**: Balance database load across multiple servers

**Impact Assessment**: This represents a critical failure of the 2nd most important service in the Ecosyste.ms infrastructure. The 29.3M+ monthly requests and 6.9M+ background jobs make this service essential for dependency parsing across the entire platform. The database connection pool exhaustion affects not just this service but potentially impacts the entire infrastructure.

The service's role as a central parsing hub for the ecosystem demands immediate emergency response to restore database connectivity and implement proper connection management infrastructure.