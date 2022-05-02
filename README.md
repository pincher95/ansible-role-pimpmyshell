# Ansible Role: PimpMyShell
NOTE:
  - MacOS and Freebsd support under development.
  - oh-my-posh under development.

[![CI](https://github.com/pincher95/ansible-role-pimpmyshell/workflows/CI/badge.svg?branch=main&event=push)](https://github.com/pincher95/ansible-role-pimpmyshell/actions?query=workflow%3ABuild) [![Ansible Galaxy](https://img.shields.io/badge/galaxy-pincher95.pimpmyshell-brightgreen)](https://galaxy.ansible.com/pincher95/pimpmyshell/)

Installs zsh, oh-my-zsh/oh-my-posh, fzf, exa, bat, fd, powerline10k on MacOS, Ubuntu/Debian, Redhat/Centos/Alma/Rocky, FreeBSD and configures packages, .zshrc and aliases according to supplied variables.

## Requirements

None.

## Operating Systems

The role tested the following operating systems:

- `Ubuntu 18.04, 20.04`
- `Debian 11`
- `CentOS 8`
- `AlmaLinux/RockyLinux`
- `Red Hat Enterprise Linux 8`

Untested operating systems:

- `MacOS`
- `FreeBSD`
- `CentOS 7`

## Role Variables

| Variable                  | Default   | Comments (type)                                                                                                                                                                                                                 |
| :---                      | :---      | :---                                                                                                                                                                                                                            |
| `enable_zsh_plugins`      | true      | Enable zsh plugins from [zsh-users](https://github.com/zsh-users) repo.                                                                                                                                                         |
| `zsh_plugins`             | []        | List of zsh plugins [zsh-users](https://github.com/zsh-users) repo.                                                                                                                                                             |
| `enable_bat`              | true      | Enable `bat`, a `cat` clone with syntax highlighting and Git integration, installing latest version from [bat](https://github.com/sharkdp/bat).                                                                                 |
| `enable_exa`              | true      | Enable `exa`, a modern replacement for `ls`, installing latest version from [exa](https://github.com/ogham/exa).                                                                                                                |
| `enable_fd`               | true      | Enable `fd` While it does not aim to support all of find's powerful functionality, it provides sensible (opinionated) defaults for a majority of use cases, installing latest version from [fd](https://github.com/sharkdp/fd). |
| `enable_fzf`              | true      | Enable `fzf`, fzf is a general-purpose command-line fuzzy finder, installing latest version from [fzf](https://github.com/junegunn/fzf).                                                                                        |
| `enable_zsh_powerline10k` | true      | Enable `enable_zsh_powerline10k`, Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience., installing latest version from [Powerlevel10k](https://github.com/romkatv/powerlevel10k).  |
| `prompt_renderer`         | oh-my-zsh | Choose prompt rendener available `oh-my-zsh`(https://ohmyz.sh/) or `oh-my-posh`(https://ohmyposh.dev/).                                                                                                                         |
| `upgrade_os`              | fasle     | Upgrade OS before installation.                                                                                                                                                                                                 |
| `apps_source`             | package   | For Debian, Darwin and FreeBSD extra cli application can be installed via package manager. RedHat flavor will always use git as source                                                                                                |
| `fzf_env_config`          | string    | Block of fzf key binding and configurations.                                                                                                                                                                                    |


Available variables are listed below, along with default values (see [`defaults/main.yml`](defaults/main.yml)):

    zsh_plugins:
      - zsh-autosuggestions
      - zsh-syntax-highlighting
      - zsh-completions
      - zsh-history-substring-search

Example zsh plugins.

    fzf_env_config: |
      # Setting for fzf
      export FZF_DEFAULT_COMMAND='{{ "fd --type f --hidden --follow" if enable_fd | default(true) else "find . -type f" }}'
      export FZF_DEFAULT_OPTS='--height 100% --multi --layout=reverse-list --inline-info'
      # To apply the command to CTRL-T as well
      export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
      export FZF_CTRL_T_OPTS="--preview '{{ "bat --color=always --line-range :500 {}" if enable_bat | default(true) else "less {}" }}'"

Example of fzf block key bunding and configurations.

## Dependencies
  For MacOS the following role and collection recommended:
  - [elliotweiser.osx-command-line-tools](https://github.com/elliotweiser/ansible-osx-command-line-tools)
  - [geerlingguy.homebrew](https://github.com/geerlingguy/ansible-collection-mac/tree/master/roles/homebrew)

## Example Playbook

```sh
ansible-playbook -i inventory -u user -k -K --become-user root --become-method su test.yml
```
Example run for user `user`

```yml
    ---
    - hosts: all
      connection: local
      vars:
        prompt_renderer: "oh-my-zsh"
        zsh_plugins:
          - zsh-autosuggestions
          - zsh-syntax-highlighting
          - zsh-completions
          - zsh-history-substring-search
      tasks:
        - name: "Include pincher95.pimpmyshell"
          ansible.builtin.include_role:
            name: "pincher95.pimpmyshell"
```

See the `tests/test.yml` directory for an example of running this role over
Ansible's `local` connection.

## License

[MIT](https://spdx.org/licenses/MIT.html)

## Author Information

This role was created in 2022 by [Yuri Tsuprun](https://github.com/pincher95)

#### Maintainer(s)

- [Yuri Tsuprun](https://github.com/pincher95)
