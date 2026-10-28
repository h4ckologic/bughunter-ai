# BugHunter AI — Complete Setup Guide

This guide walks you through replicating the **full BugHunter AI infrastructure** — including PAI (Personal AI Infrastructure), Superpowers, security skills, MCP servers, hooks, agents, and the voice system. Follow every step in order.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Install PAI (Personal AI Infrastructure)](#2-install-pai-personal-ai-infrastructure)
3. [Configure Your Identity](#3-configure-your-identity)
4. [Install Plugins](#4-install-plugins)
5. [Configure MCP Servers](#5-configure-mcp-servers)
6. [Install BugHunter AI](#6-install-bughunter-ai)
7. [Install Security Recon Tools](#7-install-security-recon-tools)
8. [Configure Burp Suite](#8-configure-burp-suite)
9. [Optional Intelligence Sources](#9-optional-intelligence-sources)
10. [Configure Notifications](#10-configure-notifications)
11. [Configure the Voice System](#11-configure-the-voice-system)
12. [Verify the Installation](#12-verify-the-installation)
13. [Configuration Reference](#13-configuration-reference)
14. [Troubleshooting](#14-troubleshooting)

---

## 1. Prerequisites

Install these tools before proceeding.

### Required

| Tool | Install | Purpose |
|------|---------|---------|
| **Claude Code** | `npm install -g @anthropic-ai/claude-code` | The AI engine (requires Anthropic API key) |
| **Bun** | `curl -fsSL https://bun.sh/install \| bash` | TypeScript runtime for all PAI tools and hooks |
| **Node.js 18+** | `brew install node` or [nodejs.org](https://nodejs.org) | For MCP servers (npx) |
| **Git** | Pre-installed on macOS / `sudo apt install git` | Version control |

### Recommended

| Tool | Install | Purpose |
|------|---------|---------|
| **Burp Suite** | [portswigger.net/burp](https://portswigger.net/burp) | Proxy & traffic analysis |
| **Playwright** | `bun add playwright && bunx playwright install chromium` | Browser automation |
| **Go 1.21+** | [go.dev/dl](https://go.dev/dl/) | Recon toolchain (subfinder, httpx, nuclei, etc.) |
| **Python 3.11+** | `brew install python@3.11` | For sqlmap, custom MCPs |
| **1Password CLI** | `brew install 1password-cli` | Credential vault integration |
| **Kitty Terminal** | `brew install --cask kitty` | Terminal with tab state support |
| **GitHub CLI** | `brew install gh` | GitHub operations |

### Optional (Mobile Testing)

| Tool | Install | Purpose |
|------|---------|---------|
| **Android SDK** | [developer.android.com](https://developer.android.com/studio) | Android app testing |
| **Appium** | `npm install -g appium` | Mobile automation |
| **Frida** | `pip install frida-tools` | Runtime instrumentation |
| **Objection** | `pip install objection` | Mobile exploration |

Verify required tools:

```bash
claude --version && bun --version && node --version && git --version
```

---

## 2. Install PAI (Personal AI Infrastructure)

PAI is the foundation layer that provides the Algorithm, skills, hooks, agents, and memory system.

```bash
# Clone the PAI repository
git clone https://github.com/danielmiessler/PAI.git
cd PAI

# Run the installer (interactive wizard)
./install.sh
```

The installer will:
- Copy skills to `~/.claude/skills/`
- Set up hooks in `~/.claude/hooks/`
- Create agent definitions in `~/.claude/agents/`
- Initialize the memory system at `~/.claude/MEMORY/`
- Configure `~/.claude/settings.json`
- Set up the voice server at `~/.claude/VoiceServer/`

### Verify PAI Installation

```bash
# Check skills installed
ls ~/.claude/skills/ | wc -l
# Expected: 50+ directories

# Check hooks installed
ls ~/.claude/hooks/*.hook.ts | wc -l
# Expected: 20 hook files

# Check agents installed
ls ~/.claude/agents/*.md | wc -l
# Expected: 13 agent files

# Check settings.json exists
cat ~/.claude/settings.json | head -5
```

### What PAI Gives You

After installation, you have:

| Component | Count | Description |
|-----------|-------|-------------|
| **Skills** | 51 | Specialized capabilities (security, research, content, etc.) |
| **Hooks** | 20 | Lifecycle automation (security validation, session management) |
| **Agents** | 13 | Expert AI agents (Pentester, Engineer, Architect, Researchers) |
| **Tools** | 40+ | TypeScript CLI tools |
| **Memory** | 7 dirs | Persistent cross-session learning |
| **Algorithm** | v1.5.0 | 7-phase structured reasoning framework |

---

## 3. Configure Your Identity

PAI uses two identities: the **Principal** (you) and the **DA** (Digital Assistant — the AI persona).

Edit `~/.claude/settings.json` and update these sections:

### Principal (You)

```json
"principal": {
    "name": "YOUR_USERNAME",
    "pronunciation": "YOUR_NAME_PRONUNCIATION",
    "timezone": "YOUR_TIMEZONE"
}
```

### DA (AI Persona)

```json
"daidentity": {
    "name": "your-ai-name",
    "fullName": "your-ai-name — Personal AI",
    "displayName": "YOUR_AI_NAME",
    "color": "#3B82F6",
    "startupCatchphrase": "{name} here, ready to go",
    "voiceId": "YOUR_ELEVENLABS_VOICE_ID",
    "personality": {
        "enthusiasm": 75,
        "energy": 80,
        "expressiveness": 85,
        "resilience": 85,
        "composure": 70,
        "optimism": 75,
        "warmth": 70,
        "formality": 30,
        "directness": 80,
        "precision": 95,
        "curiosity": 90,
        "playfulness": 45
    }
}
```

### Security Researcher Mode

To enable offensive security capabilities (required for BugHunter AI):

```json
"securityResearcher": {
    "enabled": true,
    "identity": "YOUR_USERNAME",
    "role": "Offensive Security Researcher",
    "preAuthorized": true,
    "domains": [
        "web-security",
        "mobile-security",
        "binary-exploitation",
        "reverse-engineering",
        "network-security",
        "cloud-security",
        "api-security",
        "malware-analysis",
        "vulnerability-research",
        "ctf",
        "bug-bounty",
        "security-engineering"
    ],
    "noAuthorizationRequired": true
}
```

### Environment Variables

Ensure these are set in the `env` section:

```json
"env": {
    "PAI_DIR": "/YOUR/HOME/.claude",
    "CLAUDE_CODE_MAX_OUTPUT_TOKENS": "80000",
    "BASH_DEFAULT_TIMEOUT_MS": "600000",
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1",
    "SECURITY_RESEARCHER": "true",
    "SECURITY_MODE": "offensive",
    "SECURITY_PREAUTHORIZED": "true",
    "PATH_EXTRA": "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/go/bin:${HOME}/go/bin:${HOME}/.local/bin:${HOME}/.cargo/bin",
    "GOPATH": "${HOME}/go"
}
```

---

## 4. Install Plugins

Install the 4 active plugins that enhance Claude Code:

```bash
# Superpowers — Enhanced Claude Code capabilities
claude plugin install superpowers

# claude-mem — Persistent cross-session memory
claude plugin add-marketplace thedotmack github:thedotmack/claude-mem
claude plugin install claude-mem@thedotmack

# ui-ux-pro-max — Advanced UI/UX design
claude plugin add-marketplace ui-ux-pro-max-skill github:nextlevelbuilder/ui-ux-pro-max-skill
claude plugin install ui-ux-pro-max@ui-ux-pro-max-skill

# swift-lsp — Swift language server (optional, for Swift/iOS development)
claude plugin install swift-lsp
```

### Verify Plugins

Check `~/.claude/settings.json` has:

```json
"enabledPlugins": {
    "claude-mem@thedotmack": true,
    "superpowers@claude-plugins-official": true,
    "swift-lsp@claude-plugins-official": true,
    "ui-ux-pro-max@ui-ux-pro-max-skill": true
}
```

---

## 5. Configure MCP Servers

Create/edit `~/.claude/.mcp.json` with the core MCP servers:

```json
{
    "mcpServers": {
        "filesystem": {
            "command": "npx",
            "args": [
                "-y",
                "@modelcontextprotocol/server-filesystem",
                "/YOUR/HOME/Projects",
                "/YOUR/HOME/.claude/MEMORY/BugBounty",
                "/tmp"
            ]
        },
        "github": {
            "command": "npx",
            "args": [
                "-y",
                "@modelcontextprotocol/server-github"
            ],
            "env": {
                "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_TOKEN}"
            }
        }
    }
}
```

Replace `/YOUR/HOME` with your actual home directory path.

> **Scope the filesystem server deliberately.** It is reachable by every agent in a
> hunt, and hunts read untrusted attacker-controlled text (responses, JS bundles,
> scraped pages). Granting it your whole home directory puts `~/.claude/.env` —
> which holds every API key below — one prompt injection away from being read. Grant
> only the directories a hunt needs, and add more only when something actually fails.

### Set Environment Variables

Add these to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
# GitHub
export GITHUB_TOKEN="ghp_your_github_token"

# Burp Suite REST API key — read by the hunt workflows' curl calls
# (see Workflows/W_HUNT_MOBILE.md). burp-bridge.ts does not read it; that tool
# takes --api-url / --proxy-url flags instead.
export BURP_API_KEY="your_burp_api_key"
```

### Enable MCP Servers in Settings

Ensure `settings.json` has:

```json
"enableAllProjectMcpServers": true
```

---

## 6. Install BugHunter AI

```bash
# Clone the BugHunter AI repo
git clone https://github.com/h4ckologic/bughunter-ai.git
cd bughunter-ai

# Run the installer
./install.sh
```

### What the Installer Does

1. Copies `skills/BugBountyFramework/` to `~/.claude/skills/BugBountyFramework/`
2. Creates memory directories at `~/.claude/MEMORY/BugBounty/`
3. Initializes the pattern database and technique logs
4. Makes tools executable

### Manual Installation (Alternative)

```bash
# Copy skill
cp -r skills/BugBountyFramework ~/.claude/skills/BugBountyFramework

# Create memory directories
mkdir -p ~/.claude/MEMORY/BugBounty/{Findings,LearningLogs,PatternDB,TargetProfiles,Sessions,Vault}

# Initialize pattern database
echo "# Master Patterns" > ~/.claude/MEMORY/BugBounty/PatternDB/master-patterns.md
echo "# Effective Techniques" > ~/.claude/MEMORY/BugBounty/LearningLogs/effective-techniques.md

# Make tools executable
chmod +x ~/.claude/skills/BugBountyFramework/Tools/*.ts
```

### Verify BugHunter AI

```bash
# Check skill installed
ls ~/.claude/skills/BugBountyFramework/SKILL.md

# Check agents installed (should be 28)
ls ~/.claude/skills/BugBountyFramework/Agents/ | wc -l

# Check tools installed (should be 6)
ls ~/.claude/skills/BugBountyFramework/Tools/ | wc -l

# Check memory directories
ls ~/.claude/MEMORY/BugBounty/
```

---

## 7. Install Security Recon Tools

These Go-based tools power the reconnaissance phase:

```bash
# Ensure Go is installed
go version

# Install recon tools
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install github.com/projectdiscovery/httpx/cmd/httpx@latest
go install github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
go install github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
go install github.com/tomnomnom/assetfinder@latest
go install github.com/tomnomnom/waybackurls@latest
go install github.com/tomnomnom/unfurl@latest
go install github.com/lc/gau/v2/cmd/gau@latest
go install github.com/ffuf/ffuf/v2@latest
go install github.com/sensepost/gowitness@latest

# Install sqlmap
pip install sqlmap
# or
brew install sqlmap

# Verify installation
subfinder -version && httpx -version && nuclei -version && ffuf -version
```

---

## 8. Configure Burp Suite

BugHunter AI integrates with Burp Suite through `Tools/burp-bridge.ts`, a Bun CLI that
calls Burp's REST API directly. It is not an MCP server and needs no entry in
`.mcp.json` — agents invoke it as a command.

### Enable Burp REST API

1. Open Burp Suite
2. Go to **Settings → Suite → REST API**
3. Enable the REST API on port **1337**
4. Note your API key

### Verify Burp Connection

The bridge ships with the skill (Step 6 installs it); there is nothing extra to set up.

```bash
# Start Burp Suite first, then:
cd ~/.claude/skills/BugBountyFramework/Tools
bun burp-bridge.ts --health
```

Expected output: `Burp Suite REST API is healthy`

If you proxy through something other than Burp, point the bridge at it:

```bash
bun burp-bridge.ts --health --api-url http://127.0.0.1:1337/v0.1 --proxy-url http://127.0.0.1:8080
```

---

## 9. Optional Intelligence Sources

These are extra intelligence sources you may want. **None of them ship with this
repo, and none are required** — a hunt runs without them. Read this section as a
wish list, not as install steps.

> **Verify a package exists before you add it.** Earlier versions of this guide
> named `@shodan/mcp-server` and `@virustotal/mcp-server`; neither is published on
> npm (both return 404 from the registry), so the install lines below were dead.
> Check first:
>
> ```bash
> npm view <package-name> version   # 404 means it does not exist
> ```
>
> If you find a maintained third-party MCP for one of these, treat it the way you
> would treat any dependency in an offensive toolchain: read its source before you
> give it an API key.

### Shodan (Internet Asset Search)

No official Shodan MCP server exists. Shodan's own REST API works fine from a
`Bash` call, which is how the recon agents already use it.

```bash
export SHODAN_API_KEY="your_shodan_api_key"
curl -s "https://api.shodan.io/shodan/host/search?key=$SHODAN_API_KEY&query=ssl:example.com"
```

### VirusTotal (Malware/IOC Analysis)

Same situation — use the v3 REST API directly.

```bash
export VIRUSTOTAL_API_KEY="your_vt_api_key"
curl -s -H "x-apikey: $VIRUSTOTAL_API_KEY" "https://www.virustotal.com/api/v3/domains/example.com"
```

### CVE/NVD (Vulnerability Database)

```bash
export NVD_API_KEY="your_nvd_api_key"
curl -s -H "apiKey: $NVD_API_KEY" \
  "https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=struts"
```

### Nuclei (Vulnerability Scanner)

Nuclei is a CLI and the agents call it as one — Step 7 installs it. There is no
MCP wrapper in this repo.

---

## 10. Configure Notifications

PAI supports multi-channel notifications for long-running hunts.

### ntfy (Mobile Push Notifications)

1. Install the [ntfy app](https://ntfy.sh/) on your phone
2. Choose a topic name (keep it secret — anyone with the name can send)

```bash
export NTFY_TOPIC="your-secret-topic-name"
```

### Discord (Webhook Notifications)

1. Create a webhook in your Discord server (Server Settings → Integrations → Webhooks)
2. Copy the webhook URL

```bash
export DISCORD_WEBHOOK="https://discord.com/api/webhooks/..."
```

### Twilio (SMS Notifications)

```bash
export TWILIO_TO_NUMBER="+1234567890"
export TWILIO_FROM_NUMBER="+0987654321"
export TWILIO_ACCOUNT_SID="your_sid"
export TWILIO_AUTH_TOKEN="your_token"
```

### Configure Routing in settings.json

```json
"notifications": {
    "ntfy": {
        "enabled": true,
        "topic": "${NTFY_TOPIC}",
        "server": "ntfy.sh"
    },
    "discord": {
        "enabled": true,
        "webhook": "${DISCORD_WEBHOOK}"
    },
    "twilio": {
        "enabled": true,
        "toNumber": "${TWILIO_TO_NUMBER}"
    },
    "thresholds": {
        "longTaskMinutes": 5
    },
    "routing": {
        "taskComplete": [],
        "longTask": ["ntfy"],
        "backgroundAgent": ["ntfy"],
        "error": ["ntfy", "discord"],
        "security": ["ntfy", "discord"]
    }
}
```

---

## 11. Configure the Voice System

PAI includes an ElevenLabs-powered voice server for TTS notifications.

### Get an ElevenLabs Voice ID

1. Sign up at [elevenlabs.io](https://elevenlabs.io)
2. Choose or clone a voice
3. Copy the Voice ID

### Configure Voice in settings.json

```json
"daidentity": {
    "voiceId": "YOUR_ELEVENLABS_VOICE_ID",
    "voices": {
        "main": {
            "voiceId": "YOUR_ELEVENLABS_VOICE_ID",
            "stability": 0.35,
            "similarityBoost": 0.8,
            "style": 0.9,
            "speed": 1.1
        }
    }
}
```

### Start the Voice Server

```bash
export ELEVENLABS_API_KEY="your_elevenlabs_api_key"

cd ~/.claude/VoiceServer
./start.sh
```

The voice server runs at `http://localhost:8888` and provides spoken notifications during hunts.

---

## 12. Verify the Installation

Run this checklist to confirm everything is working:

```bash
echo "=== Core Tools ==="
claude --version
bun --version
node --version
go version

echo ""
echo "=== PAI Installation ==="
echo "Skills: $(ls ~/.claude/skills/ | wc -l | tr -d ' ')"
echo "Hooks: $(ls ~/.claude/hooks/*.hook.ts 2>/dev/null | wc -l | tr -d ' ')"
echo "Agents: $(ls ~/.claude/agents/*.md 2>/dev/null | wc -l | tr -d ' ')"
echo "PAI SKILL.md: $(test -f ~/.claude/skills/PAI/SKILL.md && echo 'OK' || echo 'MISSING')"

echo ""
echo "=== BugHunter AI ==="
echo "Skill: $(test -f ~/.claude/skills/BugBountyFramework/SKILL.md && echo 'OK' || echo 'MISSING')"
echo "Agents: $(ls ~/.claude/skills/BugBountyFramework/Agents/ | wc -l | tr -d ' ')"
echo "Tools: $(ls ~/.claude/skills/BugBountyFramework/Tools/ | wc -l | tr -d ' ')"
echo "Memory: $(test -d ~/.claude/MEMORY/BugBounty && echo 'OK' || echo 'MISSING')"

echo ""
echo "=== MCP Servers ==="
echo "MCP Config: $(test -f ~/.claude/.mcp.json && echo 'OK' || echo 'MISSING')"

echo ""
echo "=== Plugins ==="
cat ~/.claude/settings.json | grep -A5 '"enabledPlugins"' 2>/dev/null | head -7

echo ""
echo "=== Recon Tools ==="
for tool in subfinder httpx nuclei ffuf sqlmap; do
    command -v $tool >/dev/null 2>&1 && echo "$tool: OK" || echo "$tool: MISSING"
done

echo ""
echo "=== Optional ==="
command -v op >/dev/null 2>&1 && echo "1Password CLI: OK" || echo "1Password CLI: not installed"
curl -s http://localhost:8888/health >/dev/null 2>&1 && echo "Voice Server: OK" || echo "Voice Server: not running"
curl -s http://127.0.0.1:1337/v0.1/ >/dev/null 2>&1 && echo "Burp Suite: OK" || echo "Burp Suite: not running"
```

### Expected Output

```
=== Core Tools ===
claude: X.X.X
bun: X.X.X
node: vXX.X.X
go: go1.XX.X

=== PAI Installation ===
Skills: 51+
Hooks: 20
Agents: 13
PAI SKILL.md: OK

=== BugHunter AI ===
Skill: OK
Agents: 28
Tools: 6
Memory: OK

=== MCP Servers ===
MCP Config: OK

=== Plugins ===
superpowers: true
claude-mem: true
ui-ux-pro-max: true
swift-lsp: true

=== Recon Tools ===
subfinder: OK
httpx: OK
nuclei: OK
ffuf: OK
sqlmap: OK
```

### Test with Claude Code

```bash
# Start Claude Code
claude

# Test BugHunter AI is loaded
# Type: hunt --help

# Test a hunt against a test target
# Type: hunt https://your-authorized-target.com
```

---

## 13. Configuration Reference

### Complete Environment Variables

Add all of these to `~/.zshrc` or `~/.bashrc`:

```bash
# === Required ===
export ANTHROPIC_API_KEY="sk-ant-..."          # Claude API key

# === MCP Servers ===
export GITHUB_TOKEN="ghp_..."                   # GitHub Personal Access Token
export BURP_API_KEY="your_burp_api_key"         # Burp Suite REST API key

# === Notifications (Optional) ===
export NTFY_TOPIC="your-secret-topic"           # ntfy.sh push notifications
export DISCORD_WEBHOOK="https://discord.com/api/webhooks/..."
export TWILIO_TO_NUMBER="+1234567890"
export TWILIO_FROM_NUMBER="+0987654321"
export TWILIO_ACCOUNT_SID="your_sid"
export TWILIO_AUTH_TOKEN="your_token"

# === Optional Security MCPs ===
export SHODAN_API_KEY="your_shodan_key"
export VIRUSTOTAL_API_KEY="your_vt_key"
export NVD_API_KEY="your_nvd_key"

# === Voice System (Optional) ===
export ELEVENLABS_API_KEY="your_elevenlabs_key"

# === Go Path ===
export GOPATH="${HOME}/go"
export PATH="${PATH}:${GOPATH}/bin"
```

### Files Checklist

| File | Required | Purpose |
|------|----------|---------|
| `~/.claude/settings.json` | Yes | Central PAI configuration |
| `~/.claude/CLAUDE.md` | Yes | Entry point |
| `~/.claude/.mcp.json` | Yes | MCP server configuration |
| `~/.claude/skills/PAI/SKILL.md` | Yes | PAI core skill |
| `~/.claude/skills/BugBountyFramework/SKILL.md` | Yes | BugHunter AI skill |
| `~/.claude/hooks/*.hook.ts` | Yes | Lifecycle hooks |
| `~/.claude/hooks/handlers/*.ts` | Yes | Hook handlers |
| `~/.claude/hooks/lib/*.ts` | Yes | Shared hook libraries |
| `~/.claude/agents/*.md` | Yes | Agent definitions |
| `~/.claude/MEMORY/BugBounty/` | Yes | Hunt memory |
| `~/.claude/VoiceServer/` | Optional | TTS voice system |
| `~/.claude/skills/BugBountyFramework/Tools/burp-bridge.ts` | Optional | Burp Suite REST API client (CLI, not an MCP) |

### Security Skills Included with PAI

These 16 security skills are installed automatically with PAI:

| Skill | Invocation |
|-------|------------|
| BugBountyFramework | `hunt <target>` |
| WebAssessment | `/WebAssessment` |
| SecurityHub | `/SecurityHub` |
| OffensiveSecurityOrchestrator | `/OffensiveSecurityOrchestrator` |
| APISecurityTesting | `/APISecurityTesting` |
| MobileSecurity | `/MobileSecurity` |
| NetworkSecurity | `/NetworkSecurity` |
| CloudSecurity | `/CloudSecurity` |
| ExploitDev | `/ExploitDev` |
| ReverseEngineering | `/ReverseEngineering` |
| MalwareAnalysis | `/MalwareAnalysis` |
| PromptInjection | `/PromptInjection` |
| VulnResearch | `/VulnResearch` |
| SASTOrchestration | `/SASTOrchestration` |
| SCASecurity | `/SCASecurity` |
| ThreatModeling | `/ThreatModeling` |
| Recon | `/Recon` |
| RedTeam | `/RedTeam` |

---

## 14. Troubleshooting

### "Skill not found" when typing `hunt`

```bash
# Verify the skill is installed
ls ~/.claude/skills/BugBountyFramework/SKILL.md

# If missing, reinstall
cd bughunter-ai
cp -r skills/BugBountyFramework ~/.claude/skills/BugBountyFramework
```

### Hooks not firing

```bash
# Check hooks are in settings.json
cat ~/.claude/settings.json | grep -c "hook.ts"
# Expected: 20+

# Verify hook files exist
ls ~/.claude/hooks/*.hook.ts

# Check bun can run them
bun ~/.claude/hooks/SecurityValidator.hook.ts --help
```

### Burp REST API not reachable

```bash
# Is Burp running?
curl -s http://127.0.0.1:1337/v0.1/
# Should return JSON, not connection refused

# Check Burp REST API is enabled:
# Burp → Settings → Suite → REST API → Enable on port 1337

# Check BURP_API_KEY is set (the workflows' curl calls need it)
echo $BURP_API_KEY
```

A listening port 8080 with nothing on 1337 usually means your proxy is running but
Burp's REST API is off — or that you are proxying through something else (Caido,
mitmproxy), which has no REST API on 1337 at all.

### MCP servers not loading

```bash
# Verify .mcp.json syntax
cat ~/.claude/.mcp.json | python3 -m json.tool

# Check enableAllProjectMcpServers in settings.json
cat ~/.claude/settings.json | grep enableAllProjectMcpServers
# Should be: true
```

### Plugins not working

```bash
# List installed plugins
claude plugin list

# Reinstall if needed
claude plugin install superpowers
```

### Voice server not responding

```bash
# Check if running
curl -s http://localhost:8888/health

# Start it
cd ~/.claude/VoiceServer
./start.sh

# Check logs
cat ~/.claude/VoiceServer/voice-server.log
```

### Memory directories missing

```bash
# Recreate
mkdir -p ~/.claude/MEMORY/BugBounty/{Findings,LearningLogs,PatternDB,TargetProfiles,Sessions,Vault}
echo "# Master Patterns" > ~/.claude/MEMORY/BugBounty/PatternDB/master-patterns.md
echo "# Effective Techniques" > ~/.claude/MEMORY/BugBounty/LearningLogs/effective-techniques.md
```

### Agent teams not working

```bash
# Verify experimental flag is set
cat ~/.claude/settings.json | grep EXPERIMENTAL_AGENT_TEAMS
# Should show: "1"

# Check teammateMode
cat ~/.claude/settings.json | grep teammateMode
# Should show: "in-process"
```

---

## Quick Reference Card

```
# Start hunting
claude
> hunt https://target.com

# Hunt modes
> hunt https://target.com --mode bounty          # CVSS >= 8.0, 10 findings
> hunt https://target.com --mode pentest         # CVSS >= 4.0, 20 findings
> hunt https://target.com --mode comprehensive   # All findings

# Store credentials
> Store creds for my-target: username admin, password P@ss

# Resume a hunt
> hunt https://target.com --resume

# Check progress
> hunt https://target.com --status

# Use security skills directly
> /SecurityHub                    # Master security command center
> /WebAssessment https://target   # OWASP WSTG v5 assessment
> /Recon target.com               # Reconnaissance
> /PromptInjection https://ai-app # LLM security testing
```

---

<p align="center">
  <strong>Built with Claude Code + PAI by <a href="https://github.com/h4ckologic">h4ckologic</a></strong>
</p>
