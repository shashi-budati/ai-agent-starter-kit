---
name: eng-quality
description: Measure and track engineering quality of a product/service. Walks through a structured checklist covering access, documentation, coding standards, tooling, security, resilience, monitoring, and DORA outcomes. Generates and updates a status report. Use when someone asks to audit, review, or track the engineering health of a service.
---

# Engineering Quality Review

This skill audits the engineering quality of a service by walking through a structured checklist, recording where each aspect is measured, and producing or updating a status report.

## When to Use

- "Run an eng quality check on X"
- "How healthy is service Y?"
- "Update the quality status for our service"
- "What's missing from our engineering practices?"

---

## How to Run the Skill

### Step 1 — Identify the Service and Mode

Ask:
1. **Service name** — what are we reviewing?
2. **Mode**:
   - **Full review** — go through every category (first run or annual)
   - **Update** — revisit only items that were previously incomplete or unknown
   - **Spot check** — focus on one or two specific categories

If a prior status file exists (e.g. `eng-quality-<service>.md`), load it before starting so you can show current status and only prompt for changes.

---

### Step 2 — Walk the Checklist

For each item, ask two questions:
- **Status**: `Yes` / `No` / `Partial` / `Unknown`
- **Where**: URL, tool name, or a one-line description of where it lives or is tracked

Skip items the user marks as N/A. Group questions by category; don't ask one item at a time — batch each category into a single prompt so the conversation moves fast.

---

## Checklist Categories

### Access
| Item | Question to ask |
|------|----------------|
| Source control (e.g. GitLab/GitHub) | Do all engineers have access? Where? |
| Code quality tool (e.g. SonarQube) | Is it set up and accessible? |
| Observability platform (e.g. Grafana) | Who has access and where is the dashboard? |

### Developer Documentation
| Item | Question to ask |
|------|----------------|
| Public developer docs | URL? Up to date? |
| API reference (Postman / Swagger / Playground) | Where is it hosted? |
| Onboarding docs | Do they exist? Where? Time-to-productive estimate? |
| Internal runbooks | Where are they? (Notion / Confluence / repo) |
| API versioning policy | Documented? Enforced? |

### Coding Standards
| Item | Question to ask |
|------|----------------|
| Static types | Enforced in the language/linter? |
| Unit tests | Do they exist? Where do they run? |
| Coverage target | What % is the target? Current coverage? (e.g. from SonarQube) |
| TDD practice | Is it mandated or encouraged? |
| Semantic versioning | Is it followed for releases and packages? |

### Development Tooling
| Item | Question to ask |
|------|----------------|
| Pre-commit hooks | What checks run? Where configured? |
| Local debugging setup | Is there a documented way to debug locally? |
| Dependency updates (e.g. Dependabot) | Configured? PR frequency? |
| Sonar / quality gating | Does it block merges on failure? |
| Git workflow | Trunk-based / GitFlow / feature branches? Documented? |
| Changelog | Auto-generated or manual? Where? |

### Dependencies
| Item | Question to ask |
|------|----------------|
| Language version | What version? Is it current/supported? |
| Database version | What and which version? Managed or self-hosted? |
| Web framework | What and which version? |
| Base container image | What image and tag? Pinned? |
| Message queues | What queuing tech? |
| Queue encryption | At rest and in transit? |

### Planning & Documentation
| Item | Question to ask |
|------|----------------|
| Issue tracker (e.g. JIRA/Linear) | Board URL? Backlog healthy (< 200 open items)? |
| ADRs (Architecture Decision Records) | Do they exist? Where? |
| PRDs | Are features spec'd before build? Where? |
| Internal release notes | Published per release? Where? |
| External release notes / changelog | Published? Where? |
| Code review process | Documented? Average review SLA? |

### Release Tooling
| Item | Question to ask |
|------|----------------|
| CI pipeline | Platform? Does it run on every PR? |
| Merge approvals | Minimum approvers required? Enforced at repo level? |
| Deployment approvals | Required for prod? Who can approve? |
| Automated regression tests | Do they run in the merge pipeline? Pass rate? |
| Rollback strategy | Documented? Last tested when? |
| Golden image / immutable artifact | Do you build once and promote? |

### Environments
| Item | Question to ask |
|------|----------------|
| QA environment | Live? Who manages it? |
| Sandbox / staging environment | Live? Customer-accessible? |
| Production environment | Cloud provider and region(s)? |
| VPC / network isolation | Separate VPCs per env? |

### Security
| Item | Question to ask |
|------|----------------|
| Container image scanning (e.g. Trivy) | In CI? Blocks on critical CVEs? |
| SAST (e.g. Semgrep) | Configured? Blocking or advisory? |
| OWASP Top 10 | Last reviewed when? Any open findings? |
| Secrets management | What tool? (Vault / AWS Secrets Manager / etc.) |
| Config management | How are env-specific configs handled? |
| Payload encryption | In transit (TLS)? At rest? |

### Resilience
| Item | Question to ask |
|------|----------------|
| Global rate limits | Configured? What limit? |
| Per-client rate limits | Configured? |
| Tunable timeouts | Configurable without deploy? |
| Load testing | Last run when? What tool? |

### Monitoring & Alerting
| Item | Question to ask |
|------|----------------|
| Alerting | PagerDuty / Rootly / OpsGenie configured? |
| Metrics (e.g. Prometheus) | Scraped and dashboarded? |
| Status page (e.g. InStatus) | Public or internal? URL? |
| Error tracking (e.g. Sentry) | Configured? Who triages? |
| Distributed tracing | OpenTelemetry / Jaeger / Datadog? |
| On-call rotation | Defined? Documented schedule? |
| Post-mortem process | Template exists? Last one done when? |
| MTTD (mean time to detect) | Approximate? Is alerting fast enough? |

### Analytics
| Item | Question to ask |
|------|----------------|
| Business metrics dashboard | Exists? URL? Owner? |
| Engineering metrics dashboard | Exists? What's tracked? |
| Unit cost dashboard | Cost per request / transaction tracked? |
| Revenue attribution | Is eng spend tied to revenue impact? |

### Logging & SLOs
| Item | Question to ask |
|------|----------------|
| P90 / P99 latency | Current numbers? Where measured? |
| SLI (Service Level Indicator) | Defined? What is it based on? |
| SLO (Service Level Objective) | Target? Current attainment? |
| Error budget | Tracked? Remaining this quarter? |
| Integration tests | Exist? Run in CI or scheduled? |
| Smoke tests | Run post-deploy? |

### Outcomes (DORA + extras)
| Item | Question to ask |
|------|----------------|
| Deployment frequency | Deployments per week/month? |
| Lead time for changes | Commit to prod in how long on average? |
| Change failure rate | % of deployments causing incidents? |
| MTTR (mean time to recover) | Average recovery time from incidents? |
| MTBF (mean time between failures) | Approximate? |
| Cycle time | Ticket created to deployed — how long? |
| First time right | % of features shipped without a hotfix in 48h? |

---

### Step 3 — Generate the Status Report

After collecting answers, write a status report to `eng-quality-<service-name>.md` in the current directory (or update the existing one).

**Report format:**

```markdown
# Engineering Quality — <Service Name>
Last updated: <date>

## Summary
<2-3 sentence health assessment: what's strong, what's missing, top 3 priorities>

## Status by Category

### <Category>
| Item | Status | Where / Notes |
|------|--------|---------------|
| ... | ✅ Yes | ... |
| ... | ⚠️ Partial | ... |
| ... | ❌ No | ... |
| ... | ❓ Unknown | ... |

...

## P0 Actions
Items that are missing or unknown with highest impact:
- [ ] <item> — <why it matters>

## P1 Actions
- [ ] <item>

## Next Review
Suggested: <3 months from now>
```

---

### Step 4 — Periodic Update Flow

When run in **Update** mode:
1. Load the existing report file
2. List all ❌ and ❓ items grouped by category
3. Ask the user to go through only those — batch by category
4. Update statuses and refresh the "Last updated" date
5. Re-rank P0/P1 actions based on what's still missing

Keep the update session under 10 minutes. Do not re-ask about ✅ items unless the user requests it.

---

## Tips

- **Be direct**: batch all questions for a category into one message — don't ask one item at a time
- **Accept partial answers**: if the user says "I don't know", mark it ❓ and move on
- **Don't lecture**: just capture status; save recommendations for the P0/P1 action list
- **Infer where possible**: if the user says "we use GitLab CI", mark the pipeline item ✅ without a follow-up
- **Keep the report durable**: it should be readable by someone who wasn't in this conversation
