# Manage Health Score

Naftiko capabilities for managing the project health score, modeled on LFX Insights & CNCF best practices. These capabilities automate the measurement, tracking, enforcement, and reporting of the four health score pillars.

---

## Capabilities

### Pillar Measurement (one per health score pillar)

| Capability | Pillar | Weight | What It Measures |
|------------|--------|--------|-----------------|
| [track-contributor-health.yml](track-contributor-health.yml) | Contributors | 30% | Total contributors, quarterly active, org diversity, retention, concentration risk |
| [track-popularity-metrics.yml](track-popularity-metrics.yml) | Popularity | 20% | GitHub stars, forks, traffic, LinkedIn followers |
| [track-development-activity.yml](track-development-activity.yml) | Development | 25% | PRs/month, issue resolution time, merge lead time, active days, releases |
| [audit-security-posture.yml](audit-security-posture.yml) | Security & Best Practices | 25% | SECURITY.md, LICENSE, CODEOWNERS, CODE_OF_CONDUCT.md, CONTRIBUTING.md, Dependabot, branch protection |

### Composite & Orchestration

| Capability | What It Does |
|------------|-------------|
| [compute-health-score.yml](compute-health-score.yml) | Orchestrates all four pillar capabilities to compute weighted overall score (0-100) |
| [report-health-score.yml](report-health-score.yml) | Computes score, writes Notion report page, posts Slack digest |
| [track-milestone-progress.yml](track-milestone-progress.yml) | Compares live metrics against quarterly targets from the roadmap |

### Actions & Enforcement

| Capability | What It Does |
|------------|-------------|
| [enforce-repo-standards.yml](enforce-repo-standards.yml) | Scans org for missing governance files and creates issues to add them |
| [manage-community-engagement.yml](manage-community-engagement.yml) | Tracks community growth signals and creates action items for engagement gaps |

---

## Services Consumed

These capabilities consume the following services (via shared adapters from the capabilities repo):

- **GitHub REST API** - Repos, contributors, commits, PRs, issues, releases, file contents, branch protection
- **GitHub GraphQL API** - Discussions
- **Notion REST API** - Health score reports, milestone targets, blog post tracking
- **Slack Web API** - Health score digests and notifications
- **LinkedIn REST API** - Organization follower count

---

## Health Score Framework

| Pillar | Weight | Metrics |
|--------|--------|---------|
| Contributors | 30% | Contributor dependency, org dependency, quarterly active, retention, total all-time |
| Popularity | 20% | Stars, forks, search visibility, adopters |
| Development | 25% | PRs/month, issue resolution, merge lead time, active days, release cadence |
| Security & Best Practices | 25% | OpenSSF badge, signed releases, dependency scanning, code review, security policy |

Target progression: ~6/100 (Q1 2026) -> 15 (Q2) -> 25 (Q3) -> 35 (Q4) -> 45 (Q1 2027) -> 50+ (CNCF Sandbox ready)
