# Examples & Reference Implementations

> **Working examples of Skills, generated artifacts, and usage patterns**

[← Back to Overview](../README.md)

---

## Directory Structure

```
examples/
├── skills/                         # Example Skill implementations
│   ├── gcp-nodejs-cicd/           # Complete CI/CD Skill
│   │   ├── SKILL.md               # Main Skill file
│   │   ├── templates/             # Pipeline templates
│   │   ├── validators/            # Policy validators
│   │   └── README.md              # Skill documentation
│   └── security-scanning/         # Security scanning Skill
│       └── SKILL.md
├── generated-artifacts/            # Examples of generated output
│   ├── nodejs-service/
│   │   ├── cloudbuild.yaml        # Generated Cloud Build pipeline
│   │   └── kubernetes/            # Generated K8s manifests
│   └── angular-app/
│       ├── cloudbuild.yaml
│       └── kubernetes/
└── api-usage/                      # API integration examples
    ├── python-client.py
    ├── typescript-client.ts
    └── curl-examples.sh
```

---

## Skills Examples

### [gcp-nodejs-cicd](skills/gcp-nodejs-cicd/)
Complete working Skill for generating CI/CD pipelines for Node.js and Angular applications on GCP.

**Demonstrates:**
- Proper SKILL.md structure with YAML frontmatter
- Multi-level progressive disclosure
- Executable validators (OPA policies)
- Template-based generation
- Organizational context integration

**Use this as a template** when creating your own organizational Skills.

---

## Generated Artifacts Examples

### Node.js Service Pipeline
See `generated-artifacts/nodejs-service/` for:
- Complete Cloud Build YAML configuration
- Kubernetes deployment manifests
- Service, HPA, and Ingress configurations
- Documentation generated from templates

### Angular Application Pipeline
See `generated-artifacts/angular-app/` for:
- Angular-specific build configuration
- Static asset optimization
- Multi-environment deployment
- CDN integration patterns

---

## API Usage Examples

### Python Client
```python
# See api-usage/python-client.py
from anthropic import Anthropic

client = Anthropic(api_key="...")

# Generate pipeline using Skills
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    messages=[{
        "role": "user",
        "content": "Create CI/CD pipeline for Node.js payment service"
    }],
    tools=[{"type": "code_execution_2025-08-25"}],
    betas=["skills-2025-10-02"]
)
```

### TypeScript Client
```typescript
// See api-usage/typescript-client.ts
import Anthropic from '@anthropic-ai/sdk';

const client = new Anthropic({
  apiKey: process.env.CLAUDE_API_KEY,
});

// Skills automatically loaded and used
const message = await client.messages.create({
  model: 'claude-3-5-sonnet-20241022',
  messages: [{
    role: 'user',
    content: 'Generate deployment pipeline'
  }],
  tools: [{ type: 'code_execution_2025-08-25' }],
  betas: ['skills-2025-10-02']
});
```

### cURL Examples
```bash
# See api-usage/curl-examples.sh
curl https://api.anthropic.com/v1/messages \
  -H "anthropic-version: 2024-10-22" \
  -H "anthropic-beta: skills-2025-10-02,code-execution-2025-08-25" \
  -H "x-api-key: $CLAUDE_API_KEY" \
  -d '{
    "model": "claude-3-5-sonnet-20241022",
    "messages": [{
      "role": "user",
      "content": "Create pipeline for Node.js service"
    }],
    "tools": [{"type": "code_execution_2025-08-25"}]
  }'
```

---

## How to Use These Examples

### 1. Study the gcp-nodejs-cicd Skill
This is a complete, working Skill that demonstrates:
- Required YAML frontmatter structure
- Clear, actionable instructions for Claude
- Integration with organizational standards
- Validation rules and error handling
- Progressive disclosure with referenced files

### 2. Adapt to Your Organization
- Replace GCP-specific details with your cloud provider
- Update security requirements to match your policies
- Modify deployment strategies for your workflows
- Add your organizational context and standards

### 3. Test with Claude
```bash
# Clone this repo
git clone https://github.com/your-org/idp-gen-x-ai-skills.git

# Copy example Skill to your Skills directory
cp -r examples/skills/gcp-nodejs-cicd ~/.claude/skills/

# Test in Claude Code
# Open a Node.js project and ask:
# "Create a CI/CD pipeline for this service"
```

### 4. Iterate and Improve
- Monitor how Claude uses your Skills
- Gather feedback from developers
- Refine instructions based on actual usage
- Update templates with proven patterns

---

## Creating Your Own Skills

### Quick Start Template

```markdown
---
name: your-skill-name
description: Brief description of what this Skill does and when to use it. Include keywords that Claude should match on.
---

# Your Skill Name

## When to Use This Skill
[Clear triggers for Claude to activate this Skill]

## Organizational Context
[Your company's standards, policies, patterns]

## Instructions
[Step-by-step guidance for Claude]

## Validation Rules
[Policy-as-code checks before completing]

## Examples
[Reference implementations]

## Troubleshooting
[Common issues and solutions]
```

### Best Practices

1. **Be Specific in Description**
   - Include keywords Claude should match
   - Describe both what and when
   - Mention specific tools, frameworks, platforms

2. **Provide Organizational Context**
   - Company standards and policies
   - Approved tools and versions
   - Required compliance checks
   - Example patterns from your codebase

3. **Write Clear Instructions**
   - Step-by-step workflow
   - Explicit validation criteria
   - Error handling guidance
   - Link to additional resources

4. **Include Executable Code**
   - Validators for policy enforcement
   - Scripts for deterministic operations
   - Templates for consistent output
   - Test utilities

5. **Test Thoroughly**
   - Validate with multiple service types
   - Test edge cases
   - Security review
   - Pilot with real teams

---

## Additional Resources

- [Anthropic Skills Documentation](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [Skills Cookbook](https://github.com/anthropics/claude-cookbooks/tree/main/skills)
- [Skills Best Practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices)

---

[← Back to Overview](../README.md)
