# Skills Bootstrap Flow

> **How developers get Skills and how new services access them**

[← Back to Diagrams Index](README.md) | [← Architecture](../02-ARCHITECTURE.md)

---

## Developer Onboarding with Skills

```mermaid
flowchart TD
    Start[New Developer Joins] --> Choice{Platform Choice?}
    
    Choice -->|Claude API| API1[Receive Workspace API Key]
    API1 --> API2[Add to Organization Workspace]
    API2 --> API3[Skills Auto-Available<br/>Loaded from Server]
    API3 --> Ready1[Ready to Use]
    
    Choice -->|Claude Code| FS1[Run Onboarding Script]
    FS1 --> FS2[git clone org-skills<br/>to ~/.claude/skills/]
    FS2 --> FS3[Configure Auto-Update<br/>Shell Profile]
    FS3 --> FS4[Install platform-cli]
    FS4 --> Ready2[Ready to Use]
    
    Ready1 --> First[Create First Service]
    Ready2 --> First
    
    First --> NewRepo[mkdir new-service<br/>cd new-service<br/>git init]
    NewRepo --> OpenIDE[Open in IDE/CLI]
    OpenIDE --> Request[Request: Create pipeline]
    Request --> ClaudeLoads[Claude Loads Skills<br/>from ~/.claude/skills/<br/>or API]
    ClaudeLoads --> Generate[Generate Artifacts]
    Generate --> WriteFiles[Write to Service Repo<br/>.cloudbuild/cloudbuild.yaml<br/>kubernetes/deployment.yaml]
    WriteFiles --> Commit[git commit & push]
    Commit --> Done[Service Ready]
    
    style API3 fill:#e1ffe1
    style Ready2 fill:#e1ffe1
    style Done fill:#e1ffe1
```

## Key Points

### Skills Location
**Skills remain in centralized location:**
- Claude API: Server-side (Anthropic's infrastructure)
- Claude Code: `~/.claude/skills/org-skills/`

**Service repos contain only generated artifacts:**
- `.cloudbuild/cloudbuild.yaml`
- `kubernetes/*.yaml`
- `.skills-metadata.json`

### Bootstrap Mechanism

**For Claude API:**
1. Platform team uploads Skills once
2. All workspace members have instant access
3. No per-developer setup required

**For Claude Code:**
1. Developer clones Skills repo to `~/.claude/skills/`
2. Configure auto-update (Git hooks or cron)
3. Skills available for all projects

### Creating New Service Repository

```
Developer Working Directory:
~/projects/payment-api/          ← New service repo

Skills Location:
~/.claude/skills/org-skills/     ← Centralized Skills

Claude Process:
1. Loads Skills from ~/.claude/skills/ (via bash)
2. Generates artifacts
3. Writes to ~/projects/payment-api/ (current directory)
4. Service repo contains ONLY generated files
```

### No Skills Duplication

**Important:** Skills are NEVER copied to service repositories
- Service repos stay clean
- Skills managed centrally
- Updates propagate from one location
- Re-generation always uses latest Skills

---

## Skills Update Flow

```mermaid
sequenceDiagram
    participant Platform as Platform Team
    participant Git as Skills Git Repo
    participant API as Claude API
    participant Dev as Developer
    
    Platform->>Git: Push Skill v2.1.0
    Git->>Git: CI/CD validates
    
    alt Distribution: Claude API
        Git->>API: Upload Skill v2.1.0
        API-->>Dev: Instantly available
        Dev->>API: Next request uses v2.1.0
    else Distribution: Filesystem
        Git->>Dev: Notification sent
        Dev->>Git: git pull in ~/.claude/skills/
        Git-->>Dev: Skills updated
    end
    
    Dev->>Dev: Use updated Skill
    Dev->>Dev: Generate new artifacts
```

---

[← Back to Diagrams Index](README.md) | [← Architecture](../02-ARCHITECTURE.md)
