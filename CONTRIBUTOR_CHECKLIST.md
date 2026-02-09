# Contributor Checklist for OpenAI Skills

Use this checklist when creating, modifying, or submitting skills to the repository.

## Before You Start

- [ ] Fork the repository on GitHub
- [ ] Clone your fork locally
- [ ] Create a new branch: `git checkout -b add-my-skill`
- [ ] Read `SETUP_GUIDE.md` for environment setup
- [ ] Read `contributing.md` for contribution guidelines

## Skill Design Phase

### Understanding Your Skill
- [ ] Define what your skill does (one primary function)
- [ ] Identify when it should be used (specific triggers/contexts)  
- [ ] Think of 3-5 concrete usage examples
- [ ] Determine if it needs scripts, references, or assets
- [ ] Check if a similar skill already exists

### Planning Resources
- [ ] Decide what scripts are needed (deterministic operations only)
- [ ] Identify reference documentation required
- [ ] Plan what assets (templates, icons, etc.) are needed
- [ ] Define naming convention (lowercase, hyphens only)

### Naming Your Skill
- [ ] Name is lowercase letters, digits, and hyphens only
- [ ] Name is under 64 characters
- [ ] Name is descriptive of the action (verb-led when possible)
- [ ] Consider namespacing by tool (e.g., `gh-*` for GitHub skills)

## Skill Implementation Phase

### Setting Up the Skill
- [ ] Create skill directory: `skills/.curated/my-skill/`
- [ ] Run `python scripts/init_skill.py my-skill --path skills/.curated` (or manually create)
- [ ] Create `agents/openai.yaml` with UI metadata
- [ ] Create `scripts/` directory if needed
- [ ] Create `references/` directory if needed
- [ ] Create `assets/` directory if needed (for templates, icons, etc.)

### Writing SKILL.md

#### Frontmatter
- [ ] `name`: Skill name (required)
- [ ] `description`: Clear, comprehensive description including when to use (required)
- [ ] Optional `metadata` fields properly formatted

#### Body Content
- [ ] Starts with clear purpose statement
- [ ] Includes "When to use" guidance upfront
- [ ] Divided into logical sections with headers
- [ ] Uses imperative/infinitive form throughout
- [ ] Maximum ~500 lines (split large skills into multiple files)
- [ ] Each step has clear input/output
- [ ] Error cases are explicitly handled
- [ ] Examples are realistic and runnable

#### Workflow Design Pattern (see references/workflows.md)
- [ ] Sequential steps are numbered clearly
- [ ] Each step specifies Input → Action → Output
- [ ] Edge cases and error paths are documented
- [ ] Recovery steps are provided for failures
- [ ] Branching logic uses explicit if/then statements
- [ ] Loop structures clearly define what repeats

#### Output Quality Standards (see references/output-patterns.md)
- [ ] If skill produces output, format is specified
- [ ] Examples of good output are provided
- [ ] Validation criteria are documented
- [ ] Quality levels are defined if applicable
- [ ] Error conditions are handled

### Creating Resources

#### Scripts (if needed)
- [ ] Each script has a clear purpose
- [ ] Scripts handle errors gracefully
- [ ] Scripts are tested and working
- [ ] Scripts include docstrings/comments
- [ ] Scripts are referenced from SKILL.md
- [ ] Scripts specify their dependencies

#### References (if needed)
- [ ] Reference files have clear purpose
- [ ] Complex references (>100 lines) have table of contents
- [ ] All references are linked from SKILL.md main body
- [ ] References avoid duplication (not repeated in SKILL.md)
- [ ] References are focused and focused on one topic

#### Assets (if needed)
- [ ] Assets are organized in `assets/` directory
- [ ] Asset files have clear naming
- [ ] Icons follow size guidelines (if UI metadata specifies)
- [ ] Templates are complete and functional
- [ ] All assets are referenced in SKILL.md or agents/openai.yaml

### UI Configuration (agents/openai.yaml)
- [ ] `display_name`: Human-readable name
- [ ] `short_description`: Brief (one sentence) description
- [ ] `icon_large`: Path to icon file (if provided)
- [ ] `brand_color`: Hex color code (if desired)
- [ ] `default_prompt`: Optional suggested usage prompt
- [ ] All paths point to actual files in the skill directory

### Licensing
- [ ] Include `LICENSE.txt` file in skill directory
- [ ] License is open source (Apache 2.0, MIT, similar)
- [ ] License text is complete and correct
- [ ] License is compatible with repository licensing

## Testing and Validation Phase

### Syntax and Structure
- [ ] Run validator: `python skills/.system/skill-creator/scripts/quick_validate.py skills/.curated/my-skill`
- [ ] Validator passes with no errors
- [ ] YAML frontmatter is correctly formatted
- [ ] Name follows naming conventions

### Content Review
- [ ] SKILL.md reads clearly and logically
- [ ] All references exist and are linked
- [ ] All scripts are included and runnable
- [ ] No broken links or references
- [ ] Examples are realistic and complete

### Script Testing (if applicable)
- [ ] Run each script independently
- [ ] Script handles missing dependencies gracefully
- [ ] Script output matches documentation
- [ ] Error conditions are handled
- [ ] Output format matches specification in SKILL.md

### Cross-Platform Testing (if applicable)
- [ ] Test on Windows (especially for path handling)
- [ ] Test on macOS/Linux
- [ ] Scripts work across platforms (or document platform requirements)

### Real-World Testing
- [ ] Try using the skill in actual scenarios
- [ ] Verify skill description matches actual behavior
- [ ] Check if triggering criteria are accurate
- [ ] Ensure edge cases are handled
- [ ] Test with different input scenarios

## Documentation Phase

### README/Notes
- [ ] Do NOT add README.md (see SKILL.md instead)
- [ ] Do NOT add INSTALLATION_GUIDE.md (use SKILL.md)
- [ ] Do NOT add CHANGELOG.md (use Git history)
- [ ] Keep only essential files (SKILL.md + resources)

### Comments and Clarity
- [ ] Code is well-commented if included
- [ ] Technical terms are explained
- [ ] Examples show intended use cases
- [ ] Screenshots/diagrams included where helpful (in assets/)

## Submission Phase

### Local Format Check
- [ ] All files use UTF-8 encoding
- [ ] Line endings are LF (Unix) — configure Git: `git config --global core.autocrlf input`
- [ ] No trailing whitespace
- [ ] Consistent indentation (spaces, not tabs)

### Git Preparation
- [ ] Create feature branch with descriptive name
- [ ] Stage only skill files: `git add skills/.curated/my-skill/`
- [ ] Commit with clear message: `git commit -m "Add my-skill: description"`
- [ ] Push to your fork: `git push origin add-my-skill`
- [ ] Review commits before pushing

### Pull Request
- [ ] Title is clear and descriptive
- [ ] Description explains what the skill does
- [ ] Description explains use cases
- [ ] Link related issues if applicable
- [ ] Mention if collaborating with others
- [ ] Request review from maintainers

### Review Response
- [ ] Address reviewer feedback promptly
- [ ] Implement suggested improvements
- [ ] Test changes again if making modifications
- [ ] Respond to all comments
- [ ] Mark conversations as resolved when done

## Post-Submission

### After Merge
- [ ] Skill is in the main repository
- [ ] You become a contributor to the project
- [ ] Consider helping review other PRs
- [ ] Share your skill in the community
- [ ] Monitor for issues or feedback

### Maintenance
- [ ] Update skill if Codex capabilities change
- [ ] Fix bugs reported by users
- [ ] Improve documentation based on feedback
- [ ] Consider adding features based on user requests

## Additional Resources

### When to Ask for Help
- Questions about skill design: Use GitHub Discussions
- Stuck on implementation: Check existing similar skills
- Encoding issues: See SETUP_GUIDE.md troubleshooting
- Security concerns: Email security@openai.com

### Reference Files in Skill Creator
- `references/workflows.md` - Workflow design patterns
- `references/output-patterns.md` - Output specifications
- `references/openai_yaml.md` - UI configuration details

### External Resources
- [Agent Skills Open Standard](https://agentskills.io)
- [OpenAI Codex Docs](https://developers.openai.com/codex/skills)
- [Contributing Guidelines](contributing.md)

---

## Troubleshooting Issues

### Validator Says "Name is invalid"
- Use only lowercase letters, digits, hyphens
- Don't start/end with hyphen
- Don't use consecutive hyphens
- Keep under 64 characters

### Scripts Not Working
- Verify script has proper shebang: `#!/usr/bin/env python3`
- Test script independently before including
- Ensure all dependencies are specified
- Check for platform-specific issues

### Encoding Errors When Validating
- Ensure SKILL.md is saved as UTF-8
- Use `git config core.autocrlf input` to normalize line endings
- Re-save file in UTF-8 encoding in your editor

### Skill Not Appearing in Codex
- Verify it's in correct directory (`skills/.curated/`)
- Run validator to ensure it's valid
- Restart Codex after adding
- Check skill description matches trigger intent

### References Not Linking
- References must be in `references/` subdirectory
- Links from SKILL.md must be relative paths
- File extensions included in links (.md, .py, etc.)
- All referenced files must exist

---

**Last Updated:** February 7, 2026

Use this checklist to ensure quality contributions to the OpenAI Skills project!
