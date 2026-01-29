# Project Brief: Ansible Role for Dotfiles Management

## WHY

This Ansible role is designed to manage dotfiles on a Linux, macOS and BSD systems. It provides a flexible and efficient way to deploy and update dotfiles across multiple hosts in a idempotent manner.

## What

* **TECHNOLOGY STACK:** Ansible, YAML, Python, Linux, macOS, BSD, Git
* **KEY DIRECTORIES:**
  * `files` : Contains static files for deployment
  * `templates` : Contains Jinja2 templates for dynamic content
  * `tasks` : Contains tasks for deployment and update
  * `vars` : Contains variables for configuration
  * `meta` : Contains metadata for the role
  * `handlers` : Contains handlers for notifications
  * `defaults` : Contains default variables for the role
* **Naming Conventions:**
  * YAML files should use `.yml` or `.yaml` extension
  * Variable names should be snake_case

## HOW (Rules and Guidelines)

### Mandatory Rules
*   **Idempotency:** All tasks MUST be idempotent. Re-running the playbook should not cause changes unless necessary.
*   **Error Handling:** Implement robust error handling using `block`, `rescue`, and `always` patterns where appropriate.
*   **Dotfile Handling:** Ensure dotfiles are managed correctly, including permissions and ownership. The variable for dotfiles should be able to access a source file/directory and target file/directory.
*   **Best Practices:** Follow established Ansible best practices, including Fully Qualified Collection Names (FQCN) for modules (e.g., `ansible.builtin.ping`).
*   **Testing:** After generating any code, run the format and check scripts locally (`ansible-lint` and `yamllint`) to verify syntax and quality. 

### Useful Commands (Slash Commands for Claude Code)
*   `/run-lint`: Runs `ansible-lint` on the project.
