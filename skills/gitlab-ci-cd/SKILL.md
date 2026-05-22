---
name: gitlab-ci-cd
description: GitLab CI/CD pipeline setup, enforcement, and debugging for infrastructure-as-code and app delivery. Use for scaffolding, enforcing, or troubleshooting GitLab pipelines in regulated or production environments.
---

# GitLab CI/CD Skill

Automate, enforce, and debug GitLab CI/CD pipelines for infrastructure-as-code and application delivery. This skill encodes the conventions, quality gates, and compliance patterns required for robust, auditable pipelines in regulated environments.

## When to Use
- Scaffolding a new GitLab CI/CD pipeline for any project
- Enforcing output/log formatting, image proxying, and variable management
- Adding or updating quality gates (validation, scan, test, apply)
- Debugging or reviewing pipeline failures
- Ensuring compliance with organizational or regulatory standards

## Workflow

1. **Plan First**
   - For any non-trivial change (3+ steps), write a plan before editing pipeline files.
   - Use `CLAUDE.md` and repo AGENTS.md for conventions.
2. **Validation Stage**
   - Validate configuration files exist and are non-empty (e.g., `runthese.properties`).
   - Fail early with clear, color-coded DEVOPS-prefixed messages.
3. **Scan Stage**
   - Run security, lint, and compliance scans (e.g., secrets, tflint, checkov).
   - Block promotion if any scan fails.
4. **Test/Plan Stage**
   - Run build/tests or `terraform plan` as appropriate.
   - Ensure all dependencies are satisfied before apply.
5. **Apply/Deploy Stage**
   - Apply changes only after all gates pass.
   - Use `when: manual` for production applies.
6. **Image Management**
   - All images must use a proxy and version variable from `runner-container-tags.yml`.
   - Never hardcode image versions or pull from public registries directly.
7. **Output Formatting**
   - All logs use DEVOPS-prefixed, color-coded messages (see standards doc).
   - No emojis or icons in output.
8. **Variable Management**
   - Check SHIP Templates before adding new variables.
   - Use uppercase and context-appropriate prefixes.
9. **Error Handling**
   - Exit with code 1 on validation or scan failures.
   - Provide actionable, sample-based error messages.
10. **Documentation & Handoff**
    - Document pipeline logic and changes in README or handoff notes.
    - Use SBAR format for session handoff if needed.

## Quality Criteria
- All jobs use proxy images and version variables
- All output is DEVOPS-prefixed, color-coded, and emoji-free
- Validation, scan, test, and apply stages are present and ordered
- No hardcoded secrets or public image pulls
- All new variables checked against SHIP Templates
- Manual gate for production applies
- Handoff notes use SBAR format

## Example Prompts
- "Set up a new GitLab CI pipeline for a Terraform project."
- "Add a validation stage to check runthese.properties is present and non-empty."
- "Enforce proxy image usage in all jobs."
- "Debug why the apply stage is blocked in this pipeline."
- "Document the pipeline structure and quality gates."

## Related Skills
- `ci-cd` (general CI/CD patterns)
- `terraform-skill` (for Terraform-specific logic)
- `provider-test-patterns` (for provider acceptance tests)
- `agent-customization` (for customizing agent behavior)

## Completion Checklist
- [ ] Plan written for non-trivial changes
- [ ] All jobs use proxy images and version variables
- [ ] Output formatting follows standards
- [ ] Validation, scan, test, apply stages present
- [ ] No hardcoded secrets or public image pulls
- [ ] New variables checked against SHIP Templates
- [ ] Manual gate for production applies
- [ ] Handoff notes (if needed) use SBAR format
