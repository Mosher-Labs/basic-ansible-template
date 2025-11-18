# Mosher Labs Basic Ansible Template - Project Memory

This file contains persistent context for Claude Code sessions on this project.
It will be automatically loaded at the start of every session.

## Project Overview

This is a template repository for creating new Ansible projects. It provides
a standardized starting point with pre-configured tooling, workflows, and
Ansible best practices.

**Key Details:**

- **Purpose:** Template for Ansible playbooks and roles
- **CI/CD:** GitHub Actions with release workflow
- **Linting:** ansible-lint, yamllint, pre-commit hooks
- **Pattern:** Fork or use as template, then customize

## Repository Structure

```text
basic-ansible-template/
├── .github/workflows/     # CI/CD workflows
│   └── release.yml        # Semantic versioning & releases
├── roles/                 # Ansible roles (customize)
├── playbook.yml           # Main playbook (customize)
├── inventory.ini          # Inventory file (customize)
├── ansible.cfg            # Ansible configuration
├── .pre-commit-config.yaml
├── .ansible-lint          # Ansible linting rules
├── README.md
└── CLAUDE.md
```

## Using This Template

### Creating a New Ansible Project

1. **Use as template:** Click "Use this template" on GitHub
1. **Clone locally:** `git clone <your-new-repo>`
1. **Update README.md:** Replace template content with project description
1. **Customize playbook.yml:** Add your tasks and roles
1. **Update inventory.ini:** Add your target hosts
1. **Install pre-commit:** `pre-commit install`
1. **Create project CLAUDE.md:** Document Ansible-specific context

### Pre-configured Features

- **Release workflow:** Automatic semantic versioning
- **Pre-commit hooks:** ansible-lint, yamllint, markdown, commit messages
- **Ansible configuration:** Best practice defaults in `ansible.cfg`
- **Directory structure:** Standard Ansible layout

## Ansible Best Practices

### Writing Playbooks

- Use FQCN for modules (e.g., `ansible.builtin.command`)
- Avoid `ignore_errors: true` - use `failed_when` instead
- Prefix variables with role name
- Use meaningful task names
- Add tags for selective execution

### Testing Locally

```bash
# Check syntax
ansible-playbook --syntax-check playbook.yml

# Dry run
ansible-playbook --check playbook.yml

# Run with verbose output
ansible-playbook -vvv playbook.yml

# Run specific tags
ansible-playbook --tags "tag-name" playbook.yml
```

## Git Workflow

1. **Create feature branch:** `git checkout -b feature/description`
1. **Make changes** to playbooks, roles, or documentation
1. **ALWAYS run pre-commit BEFORE committing:** `pre-commit run --all-files`
   - Fix ALL errors (especially ansible-lint, yamllint, and markdown)
   - Do NOT commit with `--no-verify` unless absolutely necessary
1. **Commit with conventional format:** `git commit -m "type: description"`
1. **Push and create PR:** `gh pr create --title "feat: description"`
1. **Test changes:** If your changes reference shared workflows that were also updated,
   temporarily change the reference from `@main` to `@your-branch` to test, verify
   the PR passes, then change back to `@main` before merging
1. **Merge to main:** Automatic release created based on commits

**Commit Format:** Conventional Commits (enforced by pre-commit hook)

- `feat:` - New feature or role
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `chore:` - Maintenance
- `refactor:` - Code refactoring
- `test:` - Temporary test changes (like branch references)

## Pre-commit Hooks

**Installed hooks:**

- ansible-lint (Ansible best practices)
- YAML linting (yamllint)
- Markdown linting (markdownlint)
- Conventional commit format
- File hygiene (trailing whitespace, EOF, etc.)

**Setup:**

```bash
pre-commit install              # One-time setup
pre-commit run --all-files      # Run manually
pre-commit autoupdate           # Update hook versions
```

## Important Notes

### Code Quality Standards

**CRITICAL:** All code must adhere to linter rules from the start. Do NOT write
code that needs fixing after running pre-commit hooks.

**Ansible (ansible-lint):**

- Use FQCN for all modules
- Avoid `ignore_errors: true`
- Prefix variables with role name
- Use `failed_when` instead of ignoring errors
- Keep lines under 160 characters

**YAML (yamllint):**

- Maximum line length: 80 characters
- Use 2-space indentation
- No trailing whitespace
- Proper quoting for strings containing special characters

### When Working on This Repo

1. **Write linter-compliant code from the start** - Don't fix after the fact
1. **Test playbooks locally** before committing
1. **Run pre-commit hooks** BEFORE committing (fix all errors!)
1. **Use check mode** (`--check`) to verify changes
1. **Document roles** in role README files
1. **Test shared workflow changes** - Use branch references before merging

## References

- @README.md - Repository overview
- Shared Workflows: <https://github.com/Mosher-Labs/.github>
- Ansible Docs: <https://docs.ansible.com/>
- ansible-lint: <https://ansible.readthedocs.io/projects/lint/>

---

**Last Updated:** 2025-11-18

This file should be updated whenever:

- Project patterns change
- Important Ansible context is discovered
- Roles are added or modified
