# ansible-role-dotfiles

Ansible role for managing dotfiles. Clones a git repository and deploys files as symlinks, copies, or templates to their target locations.

Supports Linux, macOS, and BSD systems.

## Requirements

- Ansible 2.14 or later
- Git installed on the target host

## Role Variables

### Repository settings

| Variable | Default | Description |
|---|---|---|
| `dotfiles_repo` | `""` | Git repository URL (required) |
| `dotfiles_repo_version` | `"main"` | Branch, tag, or commit to checkout |
| `dotfiles_repo_dest` | `~/.dotfiles` | Local path to clone the repository |
| `dotfiles_repo_accept_hostkey` | `true` | Accept SSH host keys when cloning |

### Deployment defaults

| Variable | Default | Description |
|---|---|---|
| `dotfiles_dest_base` | `$HOME` | Base path for relative destinations |
| `dotfiles_state` | `"link"` | Default deploy method: `link`, `copy`, or `template` |
| `dotfiles_owner` | `ansible_user_id` | Default file owner |
| `dotfiles_group` | `ansible_user_gid` | Default file group |
| `dotfiles_mode` | `"0644"` | Default file mode |
| `dotfiles_dir_mode` | `"0755"` | Mode for auto-created parent directories |

### Dotfile entries

`dotfiles_files` is a list of entries to deploy. Each entry requires `src` and `dest`.

| Key | Required | Description |
|---|---|---|
| `src` | yes | Source path relative to `dotfiles_repo_dest`. Supports glob patterns. |
| `dest` | yes | Destination path relative to `dotfiles_dest_base`, or an absolute path. |
| `state` | no | Override `dotfiles_state` for this entry |
| `owner` | no | Override `dotfiles_owner` for this entry |
| `group` | no | Override `dotfiles_group` for this entry |
| `mode` | no | Override `dotfiles_mode` for this entry |

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: ansible-role-dotfiles
      vars:
        dotfiles_repo: "https://github.com/user/dotfiles.git"
        dotfiles_repo_version: "main"
        dotfiles_files:
          - src: "gitconfig"
            dest: ".gitconfig"
          - src: "config/nvim"
            dest: ".config/nvim"
            state: "link"
          - src: "bashrc"
            dest: ".bashrc"
            state: "copy"
          - src: "bin/*.sh"
            dest: "bin"
```

### Glob patterns

When `src` contains a glob pattern (e.g. `bin/*.sh`), all matching files are found and deployed individually to the `dest` directory. For example, if the repo contains `bin/backup.sh` and `bin/setup.sh`, the entry above deploys both to `~/bin/backup.sh` and `~/bin/setup.sh`.

## License

MIT
