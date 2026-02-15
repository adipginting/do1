# Changelog: v3.1 (VPS Edition)

## Release Date
February 2025

## Major Changes

### 🆕 VPS-First Infrastructure Approach

**What Changed:**
- Added complete VPS deployment path as primary recommendation
- Self-hosted infrastructure (PostgreSQL, MinIO, MLflow, Prometheus, Grafana)
- Constraint-driven learning philosophy
- Linux systems administration integrated throughout

**Why:**
- Managed cloud hides the complexity that builds systems thinking
- VPS forces confrontation with CPU limits, memory pressure, disk I/O
- Predictable flat costs ($10/month) vs. surprise cloud bills
- Real operational experience with systemd, Nginx, Linux networking

### 📊 Dual-Path Support

**VPS Edition (🔧):**
- $10/month flat cost
- Self-hosted everything
- Linux mastery required
- Systems thinking focus
- Manual ops → deeper understanding

**Cloud Edition (☁️):**
- Variable costs (free tier initially)
- Managed services (GCP/AWS)
- Platform knowledge focus
- Industry-standard tooling
- Auto-scaling abstractions

Both paths are fully documented with path-specific markers throughout.

### 🔧 New VPS-Specific Content

#### Phase 0 Additions
- Complete VPS provisioning guide (Hetzner/DigitalOcean/Vultr)
- Initial server setup (Docker, Nginx, SSL, firewall)
- Docker Compose stack with all services
- Systemd service management
- DNS and Let's Encrypt configuration

#### Phase 1B Additions
- VPS-specific scaling challenges
- OOM killer debugging
- Disk space management
- PostgreSQL tuning for limited RAM
- File descriptor limits
- Nginx connection limits
- htop/iotop/iostat monitoring

#### Phase 3 Additions
- Linux process management
- Log rotation strategies
- Swap space configuration
- Resource constraint documentation

#### Phase 4 Additions
- VPS vs Cloud cost comparison
- Fixed vs variable cost models
- Infrastructure scaling decision points
- $10/month flat cost economics

### 📚 New Resources Section

**VPS Learning Materials:**
- Linux command line tutorials
- Docker & systemd guides
- Nginx & reverse proxy configuration
- PostgreSQL administration
- System monitoring tools
- Self-hosting community links

**VPS Provider Comparison:**
- Hetzner, DigitalOcean, Vultr, Linode, OVH
- Cost, location, and feature comparison
- Recommendations by use case

### ✨ Enhanced Content

#### Architecture Diagrams
- Separate VPS and Cloud architecture flows
- Self-hosted service topology
- Nginx reverse proxy configuration

#### Cost Analysis
- VPS: Flat $10/month predictable costs
- Cloud: Variable costs with projections
- Break-even analysis (100K vs 1M requests)
- Infrastructure upgrade decision points

#### Bottleneck Examples
- OOM killer scenarios (VPS-specific)
- Disk exhaustion fixes (VPS-specific)
- Memory management strategies
- Cloud vs VPS failure modes

#### Code Examples
- Dual storage path support (MinIO/GCS)
- Environment-aware configuration
- VPS monitoring scripts
- Linux system checks

### 🎯 Philosophy Updates

**Added "Constraint Builds Taste" Theme:**
- Emphasized learning through resource limits
- Real-world ops experience vs abstractions
- 2 AM debugging as teaching tool
- Systems thinking over platform knowledge

**Infrastructure Decision Framework:**
- When to choose VPS vs Cloud
- Trade-offs explicitly documented
- Cost/learning/time considerations
- ADR requirement for infrastructure choices

## Minor Changes

### Formatting Improvements
- Fixed all markdown code blocks
- Consistent table formatting (15+ tables)
- Proper heading hierarchy throughout
- Added horizontal rules between sections
- Checkbox formatting for all deliverables
- Path-specific emoji markers (🔧/☁️)

### Content Reorganization
- Infrastructure choice section at top
- VPS setup in Phase 0 (parallel to cloud)
- Path-specific sections throughout phases
- Consolidated resources section
- Dual first-actions checklists

### Documentation Updates
- ADR examples include VPS considerations
- Cost analysis for both paths
- Bottleneck fixes for both environments
- Scaling limits documented by platform

## Breaking Changes

**None** — v3.0 cloud-based approach is fully preserved as "Cloud Edition" path.

## Upgrade Path

**From v3.0:**
1. Decide: VPS or Cloud path
2. If VPS: Complete Phase 0 VPS setup
3. If Cloud: Continue as before
4. Follow path-specific instructions (marked with 🔧/☁️)
5. All phases support both paths

**For New Users:**
1. Read "Infrastructure Choice" section
2. Choose based on goals (learning depth vs industry tools)
3. Follow chosen path throughout

## Statistics

- **Total lines:** ~3,900 (up from 3,192)
- **New VPS content:** ~700 lines
- **Code examples added:** 20+
- **Tables formatted:** 15+
- **Resources added:** 25+
- **Path-specific sections:** 30+

## Success Metrics

**VPS Edition Goals:**
- Students confront real resource constraints
- Develop Linux systems administration skills
- Understand infrastructure cost trade-offs
- Build intuition through operational pain
- Learn what cloud abstractions hide

**Maintained from v3.0:**
- Taste development through building
- Architecture Decision Records
- Expert feedback calibration
- Community engagement
- Portfolio artifacts

## Next Steps

Users should:
1. Choose infrastructure path (VPS recommended for deeper learning)
2. Budget $10-15/month for VPS or plan for cloud free tier
3. Commit to 8-12 months of focused work
4. Join MLOps community for support
5. Start building immediately

## Credits

- **v3.1 VPS additions:** Integrated from constraint-first learning philosophy
- **v3.0 foundation:** Original curriculum structure
- **Community feedback:** Emphasized need for cost-conscious, systems-level learning

## License

Same as v3.0 — educational use, open source spirit.

---

**TL;DR:** v3.1 adds VPS-first infrastructure path emphasizing systems thinking through resource constraints, while preserving full cloud-based v3.0 path. Choose your adventure: deep systems learning ($10/month VPS) or industry-standard tools (cloud free tier).