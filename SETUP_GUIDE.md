# Project Setup Guide for Contributors

This guide helps you set up the OpenAI Skills project on your PC for development and contribution.

## Project Overview

The OpenAI Skills repository contains a collection of modular AI skills that extend Codex capabilities. Skills are organized in three categories:

- **System skills** (`.system/`) - Built-in skills bundled with Codex
- **Curated skills** (`.curated/`) - Production-ready skills maintained by OpenAI
- **Experimental skills** (`.experimental/`) - Community and experimental skills

## Prerequisites

- Python 3.8 or later (Python 3.13 recommended)
- Git
- A text editor or IDE (VS Code recommended)
- Administrator access for installing dependencies

## Quick Start Setup

### 1. Clone the Repository

```bash
git clone https://github.com/openai/skills.git
cd skills
```

### 2. Set Up Python Environment

On Windows with Python installed:

```powershell
# Create virtual environment
python -m venv .venv

# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Install dependencies
pip install PyYAML
```

On macOS/Linux:

```bash
# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
source .venv/bin/activate

# Install dependencies
pip install PyYAML
```

### 3. Validate Skills

All skills in this repository are automatically validated when pushed. You can validate locally:

```bash
# Validate a specific skill
python skills/.system/skill-creator/scripts/quick_validate.py skills/.curated/pdf

# Validate all curated skills
for skill in skills/.curated/*/; do
    python skills/.system/skill-creator/scripts/quick_validate.py "$skill"
done
```

On Windows PowerShell:

```powershell
Get-ChildItem 'skills\.curated' -Directory | ForEach-Object { 
    Write-Host "Validating $($_.Name)..."
    & '.\.venv\Scripts\python.exe' 'skills\.system\skill-creator\scripts\quick_validate.py' "skills\.curated\$($_.Name)" 
}
```

## Project Structure

```
skills/
├── contributing.md          # Contributing guidelines
├── README.md               # Project overview
├── .gitignore             # Git ignore rules
└── skills/
    ├── .system/           # System skills (skill-creator, skill-installer)
    │   ├── skill-creator/
    │   │   ├── SKILL.md
    │   │   ├── scripts/     # init_skill.py, generate_openai_yaml.py, quick_validate.py
    │   │   ├── references/  # Documentation guides (workflows.md, output-patterns.md, openai_yaml.md)
    │   │   └── agents/      # openai.yaml
    │   └── skill-installer/
    ├── .curated/          # Production-ready skills (30+ skills)
    │   ├── pdf/
    │   ├── gh-address-comments/
    │   ├── playwright/
    │   └── [other skills...]
    └── .experimental/     # Experimental/community skills
        ├── create-plan/
        └── [other exp skills...]
```

## Creating a New Skill

### Using the Skill Creator

```bash
# Activate virtual environment first
source .venv/bin/activate  # On macOS/Linux
.\.venv\Scripts\Activate.ps1  # On Windows

# Create a new skill
python skills/.system/skill-creator/scripts/init_skill.py my-skill --path skills/.curated
```

The script will create:
- `skills/.curated/my-skill/SKILL.md` - Skill metadata and instructions
- `skills/.curated/my-skill/agents/openai.yaml` - UI configuration
- Optional resource directories: `scripts/`, `references/`, `assets/`

### Skill Requirements

Every SKILL.md must include:

**Frontmatter (YAML):**
```yaml
---
name: skill-name
description: Clear description of what the skill does and when to use it
---
```

**Body (Markdown):**
- Clear instructions for the AI agent
- Step-by-step workflow
- Examples and best practices
- References to scripts, references, or assets

## Common Tasks

### Validate a Skill

```bash
python skills/.system/skill-creator/scripts/quick_validate.py skills/.curated/my-skill
```

### Generate UI Metadata

Update the `agents/openai.yaml` file with UI information:

```yaml
interface:
  display_name: "My Skill"
  short_description: "Brief description"
  icon_large: "./assets/icon.png"
  default_prompt: "Optional default way to use this skill"
```

### View Skill Documentation

Each skill is documented in its SKILL.md file. For complete skill creation guidelines:

```bash
# Read the skill-creator skill
cat skills/.system/skill-creator/SKILL.md

# Recommended reads from references/
cat skills/.system/skill-creator/references/workflows.md
cat skills/.system/skill-creator/references/output-patterns.md
cat skills/.system/skill-creator/references/openai_yaml.md
```

## Contributing a Skill

### Before You Submit

1. **Follow naming conventions**
   - Use lowercase letters, digits, and hyphens only
   - Namespace by tool when appropriate (e.g., `gh-address-comments`)
   - Maximum 64 characters

2. **Validate your skill**
   ```bash
   python skills/.system/skill-creator/scripts/quick_validate.py skills/.curated/my-skill
   ```

3. **Test your skill thoroughly**
   - Verify SKILL.md is clear and useful
   - Test any included scripts
   - Ensure references are complete

4. **Check license**
   - Include LICENSE.txt file in your skill directory
   - Recommended: Apache 2.0, MIT, or similar open licenses

### Submission Process

1. Fork the repository on GitHub
2. Create a new branch: `git checkout -b add-my-skill`
3. Add your skill to `skills/.curated/` or `skills/.experimental/`
4. Commit with clear message: `git commit -m "Add my-skill: brief description"`
5. Push and open a Pull Request
6. Address review feedback
7. Merge when approved

See [contributing.md](contributing.md) for detailed guidelines.

## Troubleshooting

### Python/Virtual Environment Issues

**Issue:** "ModuleNotFoundError: No module named 'yaml'"

**Solution:**
```bash
.\.venv\Scripts\Activate.ps1  # On Windows
python -m pip install PyYAML
```

### Encoding Issues When Validating

If you encounter UTF-8 encoding errors, ensure:
1. Skill SKILL.md files are saved as UTF-8
2. Python environment is properly configured
3. The validator script handles UTF-8 (✓ updated in recent fix)

### Skill Not Appearing in Codex

1. Verify skill is in correct directory:
   - System: `skills/.system/`
   - Curated: `skills/.curated/`
   - Experimental: `skills/.experimental/`

2. Restart Codex after adding skill
3. Run validator: `python skills/.system/skill-creator/scripts/quick_validate.py skills/.curated/your-skill`

## Related Resources

- [Agent Skills Open Standard](https://agentskills.io)
- [OpenAI Codex Documentation](https://developers.openai.com/codex/skills)
- [GitHub Repository](https://github.com/openai/skills)

## Support

- **Issues**: Open an issue on GitHub for bugs or questions
- **Discussions**: Use GitHub Discussions for feature requests and ideas
- **Security**: Email security@openai.com for security concerns

---

**Last Updated:** February 7, 2026
