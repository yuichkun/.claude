---
name: create-skill
description: Interactively create a new Claude Code Skill. Supports Personal Skills and Project Skills. Use when the user says "create a skill", "make a new skill", or similar.
allowed-tools: Read, Write, Glob, Bash
---

# Skill Creator - Create a New Claude Code Skill

This Skill helps you create a new Claude Code Skill interactively. It supports both Personal Skills and Project Skills.

## Execution Steps

### 1. Collect Basic Information (Interactive)

Use the AskUserQuestion tool to collect the following information:

**Question 1: Skill Location**
- Personal Skills (`~/.claude/skills/`) - Available across all projects
- Project Skills (`.claude/skills/`) - Available only in the current project

**Question 2: Basic Skill Information**
- Skill name (lowercase letters, numbers, hyphens only, max 64 characters)
  - Examples: `test-runner`, `code-reviewer`, `doc-generator`
- Brief description (1-2 sentences, max 1024 characters)
  - What does the Skill do?
  - When should it be used? (include trigger keywords)
  - Example: "Runs project tests and analyzes results. Use when the user says 'run tests', 'test this', or similar."

**Question 3: Tool Restrictions**
- Should tool usage be restricted?
  - No restrictions (default)
  - Read-only (Read, Grep, Glob)
  - File operations (Read, Write, Edit, Glob, Grep)
  - Custom (user specifies)

### 2. Validation

Validate the collected information:

1. **Name Format Check**
   - Contains only lowercase letters, numbers, and hyphens
   - Within 64 characters
   - No leading/trailing whitespace

2. **Duplicate Check**
   - For Personal Skills: check `~/.claude/skills/`
   - For Project Skills: check `.claude/skills/`
   - Ensure no directory with the same name exists

3. **Description Validity Check**
   - Description is not empty
   - Within 1024 characters
   - Contains specific, actionable content

If issues are found, ask the user for corrections.

### 3. Generate Template

Read `templates/skill-template.md` and generate a template with the collected information:

```yaml
---
name: [collected name]
description: [collected description]
[only if allowed-tools is specified]
allowed-tools: [tool list]
---

# [Skill Name]

[Description]

## Execution Steps

<!-- Describe detailed steps for this Skill here -->

1. First step
2. Next step
3. ...

## Important Notes

<!-- Describe important constraints or things to avoid -->

- Note 1
- Note 2

## Examples

<!-- Include usage examples if applicable -->

```

### 4. Save File

1. **Create Directory**
   - For Personal Skills: `mkdir -p ~/.claude/skills/[skill-name]`
   - For Project Skills: `mkdir -p .claude/skills/[skill-name]`

2. **Save SKILL.md**
   - Save the generated template
   - Personal: `~/.claude/skills/[skill-name]/SKILL.md`
   - Project: `.claude/skills/[skill-name]/SKILL.md`

3. **Confirmation Message**
   - Display the saved file path
   - Prompt the user to review the content

### 5. Suggest Next Steps

After creation, suggest the following:

1. **Fill in Detailed Steps**
   - Complete the "## Execution Steps" section
   - Write specific, actionable instructions

2. **Test the Skill**
   - Actually invoke the Skill to test it
   - Verify it works as expected

3. **Add Supporting Files (if needed)**
   - `reference.md` - Detailed reference documentation
   - `scripts/` - Helper scripts
   - `templates/` - Template files

## Best Practices

### How to Create Good Skills

1. **Stay Focused**
   - One Skill = one capability
   - "Fill PDF forms" is good, "Process documents" is too broad

2. **Be Specific in Description**
   - Include trigger keywords
   - Specify both "what it does" and "when to use it"
   - Bad example: "Processes data"
   - Good example: "Reads CSV files and calculates statistics. Use when the user says 'analyze CSV', 'get statistics', or similar."

3. **Write Clear Steps**
   - Describe step-by-step
   - Specify prerequisites and constraints
   - Include error handling

4. **Use Tool Restrictions Appropriately**
   - For read-only Skills, set `allowed-tools: Read, Grep, Glob`
   - Prevent unintended file modifications

### Common Issues and Solutions

1. **Skill Doesn't Trigger**
   - Make the description more specific
   - Add trigger keywords
   - Reconsider the Skill name

2. **YAML Errors**
   - Check for extra whitespace around `---`
   - Use spaces, not tabs, for indentation
   - Check for spelling mistakes in field names

3. **Permission Errors**
   - Ensure `allowed-tools` includes necessary tools
   - Check if sandbox restrictions are being violated

## References

- Official Documentation: https://docs.claude.com/en/docs/claude-code/skills.md
- See official docs for details on Skill types
- See `templates/skill-template.md` for template reference
