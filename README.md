<p align="center">
  <img src="docs/images/bughunter-banner.png" alt="BugHunter AI" width="800" />
</p>

<h1 align="center">BugHunter AI</h1>

<p align="center">
  <strong>Autonomous Bug Bounty Hunting Framework Powered by Claude Code + PAI</strong>
</p>

<p align="center">
  <em>20 specialized AI agents. State-machine orchestration. 51 skills. 13 expert agents. Zero human input required.</em>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> &bull;
  <a href="#full-setup-guide">Full Setup</a> &bull;
  <a href="#pai-superpowers">Superpowers</a> &bull;
  <a href="#architecture">Architecture</a> &bull;
  <a href="#agents">Agents</a> &bull;
  <a href="#sample-prompts">Prompts</a> &bull;
  <a href="#contributing">Contributing</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Opus_4-blueviolet?style=for-the-badge&logo=anthropic" alt="Claude Code" />
  <img src="https://img.shields.io/badge/PAI-v3.0-blue?style=for-the-badge" alt="PAI v3.0" />
  <img src="https://img.shields.io/badge/Agents-20-orange?style=for-the-badge" alt="20 Agents" />
  <img src="https://img.shields.io/badge/Skills-51-green?style=for-the-badge" alt="51 Skills" />
  <img src="https://img.shields.io/badge/TypeScript-Bun-black?style=for-the-badge&logo=bun" alt="Bun" />
  <img src="https://img.shields.io/badge/Burp_Suite-MCP-red?style=for-the-badge" alt="Burp MCP" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="MIT License" />
</p>

---

## What is BugHunter AI?

BugHunter AI is an **autonomous bug bounty hunting framework** that turns [Claude Code](https://docs.anthropic.com/en/docs/claude-code) into an elite security researcher. Built on top of the **PAI (Personal AI Infrastructure)** system, it combines 20 specialized vulnerability agents, 51 skills, 13 expert AI agents, 20 lifecycle hooks, and a full offensive security toolchain into a single command:

```bash
# That's it. One command. Autonomous hunting.
hunt https://app.example.com
```

**What happens next:**
1. A state machine initializes and tracks 10 phases of the hunt
2. Credentials are loaded from an encrypted vault (never inline)
3. The app is profiled — flows mapped, tech stack fingerprinted, trust boundaries identified
4. Hypothesis-driven agents deploy in parallel — each with a specific attack theory
5. Findings are reported in real-time with CVSS scoring
6. A professional bug bounty report is generated automatically

---

## Why BugHunter AI?

| Manual Bug Bounty | BugHunter AI |
|---|---|
| Hours of recon before first payload | Autonomous recon → profiling → attack in minutes |
| Forget where you left off between sessions | State machine checkpoints every phase — `--resume` anytime |
| Credentials in plaintext notes | Encrypted vault with 1Password integration |
| Run same tools blindly on every target | Hypothesis-driven: agents attack WHERE the AppProfile says bugs live |
| Test one thing at a time | 5 agents run in parallel, findings shared in real-time |
| Miss AI/LLM vulnerabilities | Dedicated LLMSecurityAgent with OWASP LLM Top 10 |
| Medium findings silently dropped | Mediums archived for attack chain correlation |
| No memory between hunts | Cross-session learning — gets smarter with every engagement |
| Single tool / single domain | 51 skills covering web, mobile, API, cloud, network, binary, AI |

---

## The Full Stack: PAI + Superpowers + BugHunter

BugHunter AI is not just a skill — it's part of a **complete offensive security infrastructure**. Here's what you get when you install the full setup:

### PAI (Personal AI Infrastructure) v3.0

The foundation layer. PAI is a general problem-solving system that provides:

- **The Algorithm (v1.5.0)** — 7-phase structured reasoning (OBSERVE → THINK → PLAN → BUILD → EXECUTE → VERIFY → LEARN)
- **51 Skills** — Specialized capabilities from security to content creation
- **13 Expert Agents** — Architect, Engineer, Pentester, Researcher variants, QA Tester, and more
- **20 Lifecycle Hooks** — Automated security validation, session management, algorithm tracking
- **Cross-Session Memory** — Persistent learning across conversations
- **Voice System** — ElevenLabs TTS integration with custom AI personality
- **Multi-Channel Notifications** — ntfy, Discord, Twilio alerts for long tasks and findings

### Superpowers Plugin

Claude Code's official `superpowers` plugin adds enhanced capabilities:

- Extended tool access and MCP server integration
- Advanced agent orchestration with team mode
- Enhanced permission management

### Security Skill Stack (16 Skills)

| Skill | Coverage |
|-------|----------|
| **BugBountyFramework** | Autonomous 10-phase hunt orchestration |
| **WebAssessment** | OWASP WSTG v5, OWASP Top 10 |
| **SecurityHub** | Master security command center with intelligent skill routing |
| **OffensiveSecurityOrchestrator** | Kill chain tracking, adaptive methodology |
| **APISecurityTesting** | REST, GraphQL, gRPC, BOLA, BFLA, mass assignment |
| **MobileSecurity** | OWASP MASTG v2, Frida, Objection, MobSF |
| **NetworkSecurity** | AD attacks, BloodHound, Kerberoasting, pivoting |
| **CloudSecurity** | AWS/Azure/GCP, IAM escalation, Pacu, ScoutSuite |
| **ExploitDev** | Heap exploitation, ROP chains, safe-linking bypass |
| **ReverseEngineering** | Ghidra, radare2, binary analysis |
| **MalwareAnalysis** | Static/dynamic analysis, YARA, IOC extraction |
| **PromptInjection** | OWASP LLM Top 10, MITRE ATLAS |
| **VulnResearch** | CVE development, AFL++ fuzzing, CodeQL |
| **SASTOrchestration** | Semgrep, CodeQL, custom rules, taint tracking |
| **SCASecurity** | SBOM, supply chain, dependency confusion |
| **ThreatModeling** | STRIDE, PASTA, attack trees |
| **Recon** | Subdomain enum, asset discovery, Shodan |
| **RedTeam** | 32-agent adversarial analysis |

### Expert Agent Army (13 Agents)

| Agent | Specialty |
|-------|-----------|
| **Pentester** | Offensive security specialist — vulnerability assessment, exploitation |
| **Engineer** | Elite principal engineer — TDD, strategic planning |
| **Architect** | System design — constitutional principles, feature specs |
| **Algorithm** | PAI Algorithm expert — ISC creation and evolution |
| **Designer** | UX/UI specialist — Figma, shadcn/ui |
| **Artist** | Visual content — Flux, GPT-Image-1, prompt engineering |
| **QATester** | Browser-automation validation — Gate 4 completion gates |
| **Intern** | 176-IQ generalist — multi-faceted problem solving |
| **ClaudeResearcher** | Multi-query academic research via Claude WebSearch |
| **CodexResearcher** | Technical archaeology — O3, GPT-5-Codex consultation |
| **GeminiResearcher** | Multi-perspective research via Google Gemini |
| **GrokResearcher** | Contrarian analysis via xAI Grok |
| **PerplexityResearcher** | Investigative journalism via Perplexity |

### MCP Servers (3 Core + 5 Recommended)

**Core (Pre-configured):**
| Server | Purpose |
|--------|---------|
| **Burp Suite MCP** | Proxy traffic analysis, scope sync, Collaborator, HAR export |
| **Filesystem MCP** | Direct file system access |
| **GitHub MCP** | Repository operations, PR management |

**Recommended Security MCPs:**
| Server | Purpose | Install |
|--------|---------|---------|
| **Shodan** | Internet asset search | `npm install -g @shodan/mcp-server` |
| **VirusTotal** | Malware/IOC analysis | `npx -y @virustotal/mcp-server` |
| **CVE/NVD** | Vulnerability database | Custom Python server |
| **Nuclei** | Vulnerability scanning | Custom Node server |
| **GitHub Security Advisory** | CVE tracking | Via GitHub MCP |

### Plugins (4 Active)

| Plugin | Purpose |
|--------|---------|
| **superpowers** | Enhanced Claude Code capabilities |
| **claude-mem** | Persistent cross-session memory |
| **swift-lsp** | Swift language server protocol |
| **ui-ux-pro-max** | Advanced UI/UX design capabilities |

### Lifecycle Hooks (20 Hooks)

| Hook | Trigger | Purpose |
|------|---------|---------|
| **SecurityValidator** | Pre: Bash, Edit, Write, Read | Validates all tool calls for security |
| **VoiceGate** | Pre: Bash | Voice notification gate |
| **AgentExecutionGuard** | Pre: Task | Guards agent execution |
| **SkillGuard** | Pre: Skill | Validates skill invocations |
| **SetQuestionTab** | Pre: AskUserQuestion | Terminal tab management |
| **AlgorithmTracker** | Post: Bash, Task* | Tracks algorithm phase progression |
| **QuestionAnswered** | Post: AskUserQuestion | Tracks Q&A flow |
| **WorkCompletionLearning** | SessionEnd | Captures learnings from work |
| **SessionSummary** | SessionEnd | Generates session summaries |
| **RelationshipMemory** | SessionEnd | Builds relationship context |
| **UpdateCounts** | SessionEnd | Updates system statistics |
| **IntegrityCheck** | SessionEnd | Validates system integrity |
| **RatingCapture** | UserPromptSubmit | Captures quality ratings |
| **AutoWorkCreation** | UserPromptSubmit | Auto-creates work tracking |
| **UpdateTabTitle** | UserPromptSubmit | Dynamic terminal tab titles |
| **SessionAutoName** | UserPromptSubmit | Auto-names sessions |
| **StartupGreeting** | SessionStart | Displays PAI banner |
| **LoadContext** | SessionStart | Loads session context |
| **CheckVersion** | SessionStart | Version checks |
| **StopOrchestrator** | Stop | Clean shutdown handling |

---

## Architecture

```mermaid
flowchart TB
    subgraph Input["User Input"]
        A["hunt target.com"]
        B["hunt --config target.json"]
        C["hunt --apk app.apk"]
    end

    subgraph PAI["PAI Infrastructure (v3.0)"]
        direction TB
        ALG["The Algorithm (7 phases)"]
        SK["51 Skills"]
        HK["20 Hooks"]
        MEM["Cross-Session Memory"]
        VOICE["Voice System"]
    end

    subgraph Orchestrator["Hunt Orchestrator (State Machine)"]
        direction TB
        P0["Phase 0: INIT"]
        P1["Phase 1: MEMORY_LOAD"]
        P2["Phase 2: TARGET_INGEST"]
        P3["Phase 3: APP_UNDERSTANDING"]
        P4["Phase 4: RECON"]
        P5["Phase 5: AGENT_DEPLOY"]
        P6["Phase 6: DYNAMIC_TEST"]
        P7["Phase 7: VULN_ASSESS"]
        P8["Phase 8: LEARNING"]
        P9["Phase 9: REPORT"]

        P0 --> P1 --> P2 --> P3 --> P4 --> P5 --> P6 --> P7 --> P8 --> P9
    end

    subgraph Tools["Tool Layer"]
        V["Credential Vault"]
        AU["Auth Manager"]
        BB["Burp Bridge"]
        PW["Playwright Harness"]
        AP["Appium Harness"]
    end

    subgraph MCPs["MCP Servers"]
        BURP["Burp Suite MCP"]
        FS["Filesystem MCP"]
        GH["GitHub MCP"]
        SH["Shodan MCP"]
        VT["VirusTotal MCP"]
    end

    subgraph Agents["Agent Army (Parallel)"]
        direction LR
        AG1["XSSAgent"]
        AG2["SQLiAgent"]
        AG3["SSRFAgent"]
        AG4["IDORAgent"]
        AG5["AuthAgent"]
        AG6["LLMSecurityAgent"]
        AG7["APIAgent"]
        AG8["MobileAgent"]
        AG9["...12 more"]
    end

    subgraph SecuritySkills["Security Skills (16)"]
        direction LR
        SS1["WebAssessment"]
        SS2["SecurityHub"]
        SS3["APISecurityTesting"]
        SS4["PromptInjection"]
        SS5["...12 more"]
    end

    subgraph Output["Output"]
        R["Bug Bounty Report"]
        F["Real-time Findings"]
        D["Live Dashboard"]
        N["Notifications (ntfy/Discord/SMS)"]
    end

    Input --> PAI
    PAI --> Orchestrator
    P2 --> V
    P3 --> AU
    P3 --> BB
    P4 --> SecuritySkills
    P5 --> Agents
    P6 --> PW
    P6 --> AP
    Agents --> MCPs
    Agents --> F
    P9 --> R
    Orchestrator --> D
    F --> N

    style PAI fill:#1e3a5f,stroke:#3b82f6,color:#fff
    style Orchestrator fill:#1a1a2e,stroke:#e94560,color:#fff
    style Agents fill:#0f3460,stroke:#e94560,color:#fff
    style Tools fill:#16213e,stroke:#0f3460,color:#fff
    style MCPs fill:#1a1a3e,stroke:#00d2ff,color:#fff
    style SecuritySkills fill:#2d1b69,stroke:#8b5cf6,color:#fff
    style Input fill:#533483,stroke:#e94560,color:#fff
    style Output fill:#0f3460,stroke:#00d2ff,color:#fff
```

---

## Quick Start

For the minimal BugHunter-only install:

```bash
git clone https://github.com/h4ckologic/bughunter-ai.git
cd bughunter-ai
./install.sh
```

For the **full setup with PAI, Superpowers, and all security skills**, see the [Full Setup Guide](SETUP.md).

---

## Full Setup Guide

See **[SETUP.md](SETUP.md)** for the complete, step-by-step guide to replicate the full infrastructure:

1. Install prerequisites (Claude Code, Bun, Go tools, Burp Suite)
2. Install PAI v3.0 (the foundation)
3. Configure your identity (DA + Principal)
4. Install plugins (Superpowers, claude-mem, ui-ux-pro-max)
5. Configure MCP servers (Burp, Filesystem, GitHub)
6. Install BugHunter AI skill
7. Set up optional security MCPs (Shodan, VirusTotal, NVD)
8. Configure notifications (ntfy, Discord, Twilio)
9. Verify the installation

---

## Hunt Modes

| Mode | CVSS Threshold | Finding Target | Best For |
|------|----------------|----------------|----------|
| `bounty` (default) | >= 8.0 | 10 | Bug bounty programs — only critical/high findings |
| `pentest` | >= 4.0 | 20 | Penetration tests — comprehensive coverage |
| `comprehensive` | >= 0.0 | 50 | Full security audits — everything documented |

```bash
hunt https://target.com                       # bounty mode (default)
hunt https://target.com --mode pentest        # pentest mode
hunt https://target.com --mode comprehensive  # comprehensive mode
```

---

## Agents

BugHunter deploys **20 specialized agents**, each an expert in one vulnerability class:

| Agent | Focus | Key Techniques |
|-------|-------|----------------|
| **AppReviewAgent** | Application understanding | Flow mapping, tech fingerprinting, trust boundary analysis |
| **LLMSecurityAgent** | AI/LLM vulnerabilities | OWASP LLM Top 10, prompt injection, RAG poisoning |
| **XSSAgent** | Cross-site scripting | Reflected, stored, DOM-based, mutation XSS |
| **SQLiAgent** | SQL injection | Union, blind, time-based, second-order SQLi |
| **SSRFAgent** | Server-side request forgery | Cloud metadata, internal services, protocol smuggling |
| **IDORAgent** | Insecure direct object refs | Horizontal/vertical privilege escalation, UUID prediction |
| **AuthAgent** | Authentication bypass | JWT attacks, session fixation, OAuth flaws, MFA bypass |
| **APIAgent** | API security | BOLA, mass assignment, rate limiting, GraphQL introspection |
| **CORSAgent** | CORS misconfiguration | Origin reflection, null origin, wildcard subdomains |
| **FileUploadAgent** | File upload attacks | Content-type bypass, polyglot files, path traversal |
| **XXEAgent** | XML external entities | Blind XXE, OOB data exfiltration, SSRF via XXE |
| **RCEAgent** | Remote code execution | Command injection, SSTI, deserialization, SSRF→RCE |
| **BusinessLogicAgent** | Business logic flaws | Race conditions, price manipulation, workflow bypass |
| **MobileAgent** | Android/iOS security | SSL pinning bypass, exported components, insecure storage |
| **WindowsAgent** | Windows/AD attacks | Kerberoasting, NTLM relay, privilege escalation |
| **ReconAgent** | Reconnaissance | Subdomain enum, port scanning, tech fingerprinting |
| **ReverseEngineeringAgent** | Binary analysis | Static analysis, dynamic analysis, vulnerability identification |
| **ExploitDevAgent** | Exploit development | PoC creation, payload crafting, reliability testing |
| **DesktopAppAgent** | Desktop app security | Electron, .NET, Java app testing |
| **LLMAgent** | Legacy LLM testing | Basic prompt testing (superseded by LLMSecurityAgent) |

### How Agents Work

Agents don't blindly scan. They receive **specific hypotheses** from the AppProfile:

```
Traditional scanning:          BugHunter AI:
"Run sqlmap on all URLs"   →   "The /api/v1/reports?filter= parameter
                                is passed into a PostgreSQL ORDER BY
                                clause — test time-based blind SQLi HERE"
```

This means **90% less noise** and **10x faster confirmation**.

---

## Tool Chain

| Tool | File | Purpose |
|------|------|---------|
| **Hunt Orchestrator** | `Tools/hunt-orchestrator.ts` | State machine — phase tracking, checkpointing, resume, dashboard |
| **Credential Vault** | `Tools/credential-vault.ts` | Encrypted credential storage, 1Password, env vars, auto-redact |
| **Auth Manager** | `Tools/auth-manager.ts` | B2C/OAuth/SAML automation, session persistence, health checks |
| **Burp Bridge** | `Tools/burp-bridge.ts` | Burp Suite REST API bridge — scope sync, HAR export, Collaborator |
| **Playwright Harness** | `Tools/playwright-harness.ts` | Browser automation — crawling, AppProfile, DOM testing |
| **Appium Harness** | `Tools/appium-harness.ts` | Mobile app testing — Android/iOS through proxy |

---

## Sample Prompts

### Your First Hunt

```
hunt https://app.example.com
```

### Hunt with Stored Credentials

```
Store credentials for example-corp: username admin@test.com, password SecureP@ss123

hunt https://app.example.com --creds vault:example-corp
```

### Pentest Mode (Find More)

```
hunt https://staging.example.com --mode pentest
```

### Hunt an AI Application

```
hunt https://ai-chatbot.example.com --mode pentest

Focus on AI-specific vulnerabilities:
- Extract the system prompt
- Test cross-user data access
- Try prompt injection (direct and indirect)
- Test RAG poisoning via document upload
```

### Resume a Hunt

```
hunt https://app.example.com --resume
```

### Full Power Hunt

```
hunt https://app.example.com using username test@example.com and password TestPass123

Use all available tools, skills, workflows, and MCPs.
Use Playwright and Burp MCPs to perform dynamic analysis.
Map the entire application attack surface.
Understand the application before attacking.
Find 10 high-severity vulnerabilities.
Don't stop until done.
```

### Use Security Skills Directly

```
# Run a web assessment using the WebAssessment skill
/WebAssessment https://target.com

# Use the SecurityHub for guided methodology
/SecurityHub start assessment on https://target.com

# Run OSINT reconnaissance
/Recon https://target.com --deep

# Test LLM/AI security
/PromptInjection https://ai-app.com
```

See [examples/sample-prompts.md](examples/sample-prompts.md) for more.

---

## Live Dashboard

Check hunt progress anytime:

```
hunt https://target.com --status
```

```
======================================================================
  HUNT STATUS: https://app.example.com
  Mode: BOUNTY | Elapsed: 45m | Findings: 3
  Min CVSS: 8.0 | Target: 10 findings
======================================================================
  [OK] INIT                  2s
  [OK] MEMORY_LOAD           1s
  [OK] TARGET_INGEST         3s
  [OK] APP_UNDERSTANDING     120s     (2 findings)
  [>>] RECON                 running...
  [  ] AGENT_DEPLOY
  [  ] DYNAMIC_TEST
  [  ] VULN_ASSESS
  [  ] LEARNING
  [  ] REPORT

  FINDINGS:
    F-001 [critical] SSRF: Webhook URL fetches AWS metadata
    F-002 [high] IDOR: Access other users' expense reports
    F-003 [high] XSS: Stored XSS in admin notification panel
======================================================================
```

---

## Directory Structure

```
# BugHunter AI Skill (installed to ~/.claude/skills/)
~/.claude/skills/BugBountyFramework/
├── SKILL.md                     # Main skill definition (v2.0)
├── Agents/                      # 20 specialized vulnerability agents
│   ├── AppReviewAgent.md
│   ├── LLMSecurityAgent.md
│   ├── XSSAgent.md
│   ├── SQLiAgent.md
│   ├── SSRFAgent.md
│   ├── IDORAgent.md
│   ├── AuthAgent.md
│   ├── APIAgent.md
│   ├── CORSAgent.md
│   ├── FileUploadAgent.md
│   ├── XXEAgent.md
│   ├── RCEAgent.md
│   ├── BusinessLogicAgent.md
│   ├── MobileAgent.md
│   ├── WindowsAgent.md
│   ├── ReconAgent.md
│   ├── ReverseEngineeringAgent.md
│   ├── ExploitDevAgent.md
│   ├── DesktopAppAgent.md
│   └── LLMAgent.md
├── Tools/                       # TypeScript tools (Bun runtime)
│   ├── hunt-orchestrator.ts
│   ├── credential-vault.ts
│   ├── auth-manager.ts
│   ├── burp-bridge.ts
│   ├── playwright-harness.ts
│   └── appium-harness.ts
├── Templates/
│   ├── BugReport.md
│   └── TargetConfig.md
└── Wordlists/

# PAI Infrastructure (the foundation)
~/.claude/
├── settings.json                # Central config (identity, hooks, permissions, plugins)
├── CLAUDE.md                    # Entry point
├── .mcp.json                    # MCP server configuration
├── skills/                      # 51 skills
│   ├── PAI/                     # Core PAI system
│   ├── BugBountyFramework/      # This project
│   ├── WebAssessment/           # OWASP WSTG v5
│   ├── SecurityHub/             # Security command center
│   ├── OffensiveSecurityOrchestrator/
│   ├── APISecurityTesting/
│   ├── MobileSecurity/
│   ├── NetworkSecurity/
│   ├── CloudSecurity/
│   ├── ExploitDev/
│   ├── ReverseEngineering/
│   ├── MalwareAnalysis/
│   ├── PromptInjection/
│   ├── VulnResearch/
│   ├── SASTOrchestration/
│   ├── SCASecurity/
│   ├── ThreatModeling/
│   ├── Recon/
│   ├── RedTeam/
│   ├── OSINT/
│   ├── Research/                # Multi-engine research
│   ├── Browser/                 # Browser automation
│   ├── Fabric/                  # 240+ prompt patterns
│   └── ...35 more
├── agents/                      # 13 expert agent definitions
│   ├── Pentester.md
│   ├── Engineer.md
│   ├── Architect.md
│   └── ...10 more
├── hooks/                       # 20 lifecycle hooks
│   ├── SecurityValidator.hook.ts
│   ├── AlgorithmTracker.hook.ts
│   ├── LoadContext.hook.ts
│   ├── handlers/                # 7 hook handlers
│   └── lib/                     # 12 shared libraries
├── mcps/                        # Custom MCP servers
│   └── burp-mcp/
├── VoiceServer/                 # ElevenLabs TTS integration
└── MEMORY/                      # Persistent memory system
    ├── BugBounty/
    │   ├── Sessions/
    │   ├── Findings/
    │   ├── PatternDB/
    │   ├── LearningLogs/
    │   ├── TargetProfiles/
    │   └── Vault/
    ├── LEARNING/
    ├── SECURITY/
    ├── STATE/
    ├── WORK/
    └── VOICE/
```

---

## How It Differs from Other Tools

| Feature | BugHunter AI | Nuclei/Burp Scanner | Manual Testing |
|---------|-------------|---------------------|----------------|
| **Intelligence** | Understands the app first, then attacks | Signature matching | Human expertise |
| **Context** | Remembers across sessions | Stateless | Notes/memory |
| **Hypothesis-driven** | Tests specific theories | Tests everything | Depends on researcher |
| **AI/LLM testing** | First-class OWASP LLM Top 10 | Not supported | Rare expertise |
| **Parallel agents** | 5 specialized agents simultaneously | Single scanner | One person |
| **State machine** | Checkpoints, resume, never loses progress | Run from scratch | Bookmarks/notes |
| **Credential security** | Encrypted vault + 1Password | Config files | Plaintext notes |
| **Multi-domain** | Web + Mobile + API + Cloud + Network + Binary | Single domain | Limited scope |
| **Algorithm** | 7-phase structured reasoning (PAI) | None | Informal methodology |
| **Skills ecosystem** | 51 skills, 16 security-focused | Plugin-based | Tool-dependent |

---

## Responsible Use

This framework is designed for **authorized security testing only**:

- Only test applications you have **written permission** to test
- Bug bounty programs with **clearly defined scope**
- Penetration tests with **signed engagement letters**
- Your own applications in **staging/development environments**

**BugHunter AI enforces scope:** The framework includes hard scope enforcement that blocks testing out-of-scope targets. Configure your scope before hunting.

The maintainers are not responsible for misuse. Always follow your program's rules of engagement.

---

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Ideas for contributions:**
- New specialized agents (e.g., GraphQLAgent, WebSocketAgent)
- Additional auth strategy templates
- Better wordlists
- Integration with more MCP servers
- New security skills
- Improved report templates
- Bug fixes and documentation

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

## Acknowledgements

- **[Anthropic](https://anthropic.com)** — Claude Code, the AI engine behind everything
- **[Daniel Miessler / PAI](https://github.com/danielmiessler/PAI)** — Personal AI Infrastructure v3.0 — the foundation layer providing the Algorithm (v1.5.0), 51 skills, 13 expert agents, 20 lifecycle hooks, cross-session memory, and the structured reasoning framework that makes autonomous hunting possible
- **[Claude Code Superpowers](https://github.com/anthropics/claude-code)** — Official Claude Code plugin enabling enhanced tool access, advanced agent orchestration with team mode, and extended MCP server integration that powers parallel agent deployment
- **[claude-mem](https://github.com/thedotmack/claude-mem)** — Persistent cross-session memory plugin that enables BugHunter's learning system to remember techniques, patterns, and findings across hunts
- **[PortSwigger](https://portswigger.net)** — Burp Suite integration via custom MCP bridge
- **[ProjectDiscovery](https://projectdiscovery.io)** — Nuclei, httpx, subfinder, naabu — the recon backbone
- **[Playwright](https://playwright.dev)** — Browser automation for dynamic testing and app profiling
- **[Bun](https://bun.sh)** — TypeScript runtime powering all tools and hooks
- **[ElevenLabs](https://elevenlabs.io)** — Voice synthesis for the PAI notification and voice system
- **[ntfy](https://ntfy.sh)** — Push notifications for long-running hunts

---

<p align="center">
  <strong>Built with Claude Code + PAI by <a href="https://github.com/h4ckologic">h4ckologic</a></strong>
</p>

<p align="center">
  <em>If BugHunter AI helps you find bugs, give it a star!</em>
</p>
