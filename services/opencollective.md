# Opencollective Service

**URL**: https://opencollective.ecosyste.ms  
**GitHub**: https://github.com/ecosyste-ms/opencollective  
**Server**: 195.154.82.7 (Large, shared)  
**Performance Period**: July 24 - August 23, 2025 (30 days)

## Performance Summary

- **Total Requests**: 7.2M web requests (30 days)
- **Background Jobs**: 1.0M jobs (30 days)
- **Uptime**: No uptime monitoring errors detected
- **Open Incidents**: 14 currently open (severe database and Redis issues)

## Endpoint Analysis

### Most Used Endpoints (by request volume)

1. **CollectivesController#batch** - 2,072,830 requests (28.9%)
   - Batch collective operations
   - Highest traffic endpoint

2. **ProjectsController#commits** - 946,259 requests (13.2%)
   - Project commit history pages
   - High-volume content

3. **ProjectsController#issues** - 648,085 requests (9.0%)
   - Project issues pages
   - Core functionality

4. **ProjectsController#show** - 557,340 requests (7.8%)
   - Individual project details
   - Major content driver

5. **ProjectsController#releases** - 420,706 requests (5.9%)
   - Project release information

### High-Traffic Endpoints

- **ChartsController#issues**: 383,310 requests (5.3%)
- **ProjectsController#advisories**: 360,127 requests (5.0%)
- **CollectivesController#show**: 352,961 requests (4.9%)
- **ChartsController#transactions**: 329,411 requests (4.6%)
- **ProjectsController#packages**: 312,675 requests (4.4%)

### Medium-Traffic Endpoints

- **CollectivesController#issues**: 151,401 requests (2.1%)
- **ChartsController#commits**: 138,320 requests (1.9%)
- **Api::V1::ProjectsController#show**: 128,415 requests (1.8%)
- **CollectivesController#commits**: 125,214 requests (1.7%)

## Critical Issues

### **CRITICAL** **CATASTROPHIC DATABASE FAILURE**
Multiple critical database connectivity and disk space issues:

#### **Database Connection Failures** (8 open incidents)
- ActiveRecord::ConnectionNotEstablished affecting multiple controllers
- Connection refused to PostgreSQL server (172.17.0.23:5432)
- Database system startup/shutdown errors

#### **PostgreSQL Disk Full Errors** (6 open incidents)
- PG::DiskFull: Could not resize shared memory segments
- Affecting all major controllers: CollectivesController, ProjectsController
- Over 2,200 occurrences on CollectivesController#batch alone
- Recent incidents still occurring as of August 11, 2025

#### **Redis Connection Failure** (1 open incident)
- RedisClient::CannotConnectError for background jobs
- 90 total occurrences, blocking Sidekiq processing
- Connection refused to redis://dokku-redis-opencollective:6379

## Performance Characteristics

### **CRITICAL** **Service in Critical Failure State**
- **High traffic volume**: 7.2M requests over 30 days (~240K per day)
- **Substantial background processing**: 1.0M background jobs
- **Multiple system failures**: Database, Redis, and storage issues
- **Service degradation**: 14 open incidents affecting core functionality

### **Usage Pattern**
- **Collective-focused**: Heavy usage of collective batch operations (28.9% of traffic)
- **Project analytics**: Strong focus on commits, issues, and releases
- **Chart/visualization heavy**: Multiple chart endpoints with significant traffic
- **API integration**: Active API usage for project lookups and data access

## Server Infrastructure

**Server Details**:
- **IP**: 195.154.82.7
- **Type**: Large server (shared with 17 other services)
- **OS**: Ubuntu 20.04.6 LTS
- **Shared Services**: Part of 18-service consolidation

**Resource Crisis**:
- **Database disk full**: PostgreSQL cannot resize shared memory segments
- **Connection pool exhausted**: Database connections being refused
- **Redis connectivity issues**: Background job processing blocked
- **Shared server impact**: May be affecting other services

## Background Jobs Analysis

- **Total Background Jobs**: 955,420 jobs (30 days)
- **Job Volume**: ~31,800 jobs per day average
- **Status**: Partially blocked by Redis connection issues
- **Purpose**: Collective data synchronization, project analytics, funding data processing

## Action Items

### **CRITICAL** **EMERGENCY (Critical System Failure)**
1. **Immediate PostgreSQL disk space cleanup** - resolve disk full errors preventing database operations
2. **Database connection pool investigation** - fix connection refused errors
3. **Database restart/recovery** - resolve "database system is shutting down/starting up" errors
4. **Redis connectivity fix** - restore background job processing
5. **Service health assessment** - evaluate full scope of system failures

### **CRITICAL** **URGENT DATABASE RECOVERY**
1. **PostgreSQL disk space expansion** - increase available storage immediately
2. **Shared memory configuration** - adjust PostgreSQL shared memory settings
3. **Connection pool tuning** - increase max connections and optimize pool settings
4. **Database performance analysis** - identify queries causing resource exhaustion
5. **Data archival** - move old data to reduce database size

### **HIGH PRIORITY**
1. **Redis service restoration** - fix dokku-redis-opencollective connection
2. **Background job recovery** - process backlogged jobs once Redis is restored
3. **Error monitoring** - implement comprehensive alerting for database/Redis issues
4. **Performance monitoring** - add database and Redis health monitoring

### **LOW PRIORITY**  **INFRASTRUCTURE RECOVERY**
1. **Database optimization** - query performance analysis and indexing
2. **Connection pooling** - implement PgBouncer or similar connection pooling
3. **Caching strategy** - reduce database load with Redis caching (once Redis is fixed)
4. **Resource monitoring** - implement disk space and memory alerts

## Technical Notes

**Service Architecture**:
- **Open Collective funding platform**: Tracks collective funding and project analytics
- **High-volume data processing**: Combines web traffic with substantial background jobs
- **Database-intensive**: Heavy reliance on PostgreSQL for analytics and reporting
- **Visualization focus**: Multiple chart endpoints for funding and project analytics

**Critical System Dependencies**:
- **PostgreSQL database**: Currently experiencing disk full and connection issues
- **Redis**: Required for background job processing, currently failing
- **Shared server resources**: May be contributing to resource exhaustion

## Recommendations

**Status**: CRITICAL **SYSTEM FAILURE - EMERGENCY RESPONSE REQUIRED** - Service experiencing catastrophic database and Redis failures affecting core functionality.

**Emergency Actions Required**:
1. **CRITICAL**: Resolve PostgreSQL disk space crisis immediately
2. **CRITICAL**: Fix database connection pool exhaustion
3. **CRITICAL**: Restore Redis connectivity for background job processing
4. **URGENT**: Assess impact on other services sharing this server

**System Recovery Priority**:
1. Database disk space expansion and cleanup
2. PostgreSQL service restart and health verification
3. Redis connection restoration
4. Background job queue processing
5. Comprehensive monitoring implementation

**Role in Ecosystem**: Critical funding analytics platform for open source projects. The current system failures make it largely non-functional and likely impact the broader Ecosyste.ms platform.

This service requires immediate emergency intervention to restore basic functionality before any optimization work can begin.