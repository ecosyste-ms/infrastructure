# Ecosyste.ms Services Documentation

This directory contains comprehensive performance and infrastructure documentation for all 22 services in the Ecosyste.ms platform. Each service file includes detailed analysis covering traffic patterns, performance metrics, infrastructure utilization, and operational recommendations.

## Complete Services List (Alphabetical)

| Service | URL | Description | Status |
|---------|-----|-------------|---------|
| [advisories](./advisories.md) | https://advisories.ecosyste.ms | Security advisory tracking | 🔴 97.18% uptime |
| [archives](./archives.md) | https://archives.ecosyste.ms | Archive management service | 🔴 90.30% uptime |
| [awesome](./awesome.md) | https://awesome.ecosyste.ms | Awesome list curation | ✅ Excellent performance |
| [commits](./commits.md) | https://commits.ecosyste.ms | Commit analysis service | ✅ Stable operations |
| [dashboard](./dashboard.md) | https://dashboard.ecosyste.ms | Main dashboard interface | ⚠️ Limited monitoring data |
| [dependabot](./dependabot.md) | https://dependabot.ecosyste.ms | Dependency update tracking | ✅ Excellent performance |
| [diff](./diff.md) | https://diff.ecosyste.ms | Code difference analysis | ✅ Stable operations |
| [docker](./docker.md) | https://docker.ecosyste.ms | Container registry management | ✅ Stable operations |
| [funds](./funds.md) | https://funds.ecosyste.ms | Funding information tracking | ✅ Excellent performance |
| [home](./home.md) | https://ecosyste.ms | Main website and documentation | ✅ Stable operations |
| [issues](./issues.md) | https://issues.ecosyste.ms | Issue tracking and analysis | ✅ High-volume stable service |
| [licenses](./licenses.md) | https://licenses.ecosyste.ms | License detection and tracking | ✅ Stable operations |
| [opencollective](./opencollective.md) | https://opencollective.ecosyste.ms | Open Collective integration | 🔴 Database/Redis failures |
| [ost](./ost.md) | https://ost.ecosyste.ms | Open source tracker | ✅ Stable operations |
| [packages](./packages.md) | https://packages.ecosyste.ms | Package registry management | 🔴 Database server unreachable |
| [papers](./papers.md) | https://papers.ecosyste.ms | Research paper tracking | ✅ Stable operations |
| [parser](./parser.md) | https://parser.ecosyste.ms | Code parsing service | 🔴 Database connection crisis |
| [repos](./repos.md) | https://repos.ecosyste.ms | Repository analysis service | 🔴 External API rate limiting |
| [ruby](./ruby.md) | https://ruby.ecosyste.ms | Ruby-specific tooling | 🔴 Redis connection failure |
| [sbom](./sbom.md) | https://sbom.ecosyste.ms | Software Bill of Materials | ⚠️ No activity detected |
| [sponsors](./sponsors.md) | https://sponsors.ecosyste.ms | Sponsor tracking | ✅ Perfect example service |
| [timeline](./timeline.md) | https://timeline.ecosyste.ms | Event timeline service | 🔴 Database query timeouts |

## Traffic Analysis (30-day period)

### Ultra-High Traffic Services (>50M requests)
1. **[packages](./packages.md)** - 168.1M requests + 77.4M background jobs 🔴 **CRITICAL**
2. **[repos](./repos.md)** - 87.2M requests + 133.0M background jobs 🔴 **CRITICAL** 
3. **[issues](./issues.md)** - 61.6M requests + 21.1M background jobs ✅ **STABLE**

### High Traffic Services (10M+ requests)
- **[parser](./parser.md)** - 29.3M requests + 8.9M background jobs 🔴 **CRITICAL**
- **[awesome](./awesome.md)** - 13.0M requests + 2.4M background jobs ✅ **EXCELLENT**
- **[opencollective](./opencollective.md)** - 7.1M requests + 1.0M background jobs 🔴 **CRITICAL**

### Medium Traffic Services (1M-10M requests)
- **[commits](./commits.md)** - 7.5M requests ✅ **STABLE**
- **[dependabot](./dependabot.md)** - 5.2M requests + 1.6M background jobs ✅ **EXCELLENT**
- **[advisories](./advisories.md)** - 5.0M requests 🔴 **UPTIME ISSUES**
- **[diff](./diff.md)** - 4.6M requests ✅ **STABLE**
- **[docker](./docker.md)** - 3.4M requests ✅ **STABLE**
- **[ost](./ost.md)** - 1.9M requests ✅ **STABLE**
- **[archives](./archives.md)** - 1.7M requests 🔴 **ERROR RATE ISSUES**
- **[sponsors](./sponsors.md)** - 1.7M requests + 0.8M background jobs ✅ **PERFECT MODEL**
- **[papers](./papers.md)** - 1.0M requests ✅ **STABLE**

### Low Traffic Services (<1M requests)
- **[timeline](./timeline.md)** - 0.7M requests 🔴 **DATABASE OPTIMIZATION NEEDED**
- **[ruby](./ruby.md)** - 35K requests + 22K background jobs 🔴 **REDIS ISSUES**
- **[funds](./funds.md)** - 29K requests + 0.8M background jobs ✅ **EXCELLENT**
- **[home](./home.md)** - 24K requests ✅ **STABLE**
- **[licenses](./licenses.md)** - 44K requests ✅ **STABLE**
- **[sbom](./sbom.md)** - No traffic detected ⚠️ **INVESTIGATION REQUIRED**
- **[dashboard](./dashboard.md)** - No monitoring data available ⚠️ **INVESTIGATION REQUIRED**

## Critical Infrastructure Issues

### 🔴 Emergency Response Required
1. **[packages](./packages.md)** - Database server 195.154.29.88 completely unreachable
2. **[repos](./repos.md)** - 70,000+ GitHub/GitLab API rate limit violations
3. **[parser](./parser.md)** - 5.7M+ database connection pool exhaustion failures

### 🔴 Critical Issues
4. **[timeline](./timeline.md)** - 6,686+ database query timeouts due to billions of rows requiring optimization
5. **[opencollective](./opencollective.md)** - Database and Redis connectivity failures
6. **[ruby](./ruby.md)** - Redis connection failure blocking background processing

## Documentation Coverage

Each service documentation includes:

- **Performance Summary**: Request volumes, background jobs, uptime metrics
- **Endpoint Analysis**: Traffic breakdown by controller/action
- **Critical Issues**: Open incidents with severity assessment  
- **Server Infrastructure**: Resource allocation and utilization analysis
- **Action Items**: Prioritized recommendations for improvement
- **Technical Notes**: Architecture patterns and dependencies

## Infrastructure Overview

For comprehensive infrastructure analysis, server mapping, and cross-service recommendations, see:
- **[../services.md](../services.md)** - Complete infrastructure overview and analysis
- **[../servers.md](../servers.md)** - Server inventory and resource allocation

---

*Last updated: August 24, 2025*  
*Performance period: July 24 - August 23, 2025 (30 days)*  
*Generated using Claude Code with AppSignal MCP integration*