# Ansible Role: PimpMyShell
[![CI](https://github.com/pincher95/ansible-role-pimpmyshell/workflows/Build/badge.svg?branch=main&event=push)](https://github.com/pincher95/ansible-role-pimpmyshell/actions?query=workflow%3ABuild)

Installs zsh, oh-my-zsh/oh-my-posh, fzf, exa, bat, fd, powerline10k on MacOS, Ubuntu/Debian, Redhat/Centos/Alma/Rocky, FreeBSD and configures packages, .zshrc and aliases according to supplied variables.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see [`defaults/main.yml`](defaults/main.yml)):

    enable_zsh_plugins: true

Enable zsh plugins from [zsh-users](https://github.com/zsh-users) repo.

    zsh_plugins:
      - zsh-autosuggestions
      - zsh-syntax-highlighting
      - zsh-completions
      - zsh-history-substring-search

Example zsh plugins.

    enable_bat: true

Enable `bat`, a `cat` clone with syntax highlighting and Git integration, install latest version from [bat](https://github.com/sharkdp/bat).

    enable_exa: true

Enable `exa`, a modern replacement for `ls`, install latest version from [exa](https://github.com/ogham/exa).

    enable_fd: true

Enable `fd` is a program to find entries in your filesystem. It is a simple, fast and user-friendly alternative to find. While it does not aim to support all of find's powerful functionality, it provides sensible (opinionated) defaults for a majority of use cases, install latest version from [fd](https://github.com/sharkdp/fd).

    enable_fzf: true

Enable `fzf`, fzf is a general-purpose command-line fuzzy finder, install latest version from [fzf](https://github.com/junegunn/fzf).

    fzf_env_config: |
      # Setting for fzf
      export FZF_DEFAULT_COMMAND='fd --type f --hidden --follow'
      export FZF_DEFAULT_OPTS='--height 100% --multi --layout=reverse-list --inline-info'
      # To apply the command to CTRL-T as well
      export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"
      export FZF_CTRL_T_OPTS="--preview '{{ "bat --color=always --line-range :500 {}" if enable_bat else "less {}" }}'"

Customize fzf key bunding and options.

    enable_zsh_powerline10k: true

Enable `enable_zsh_powerline10k`, Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience., install latest version from [Powerlevel10k](https://github.com/romkatv/powerlevel10k).

    prompt_renderer: "oh-my-zsh"

Choose prompt rendener available `oh-my-zsh` or `oh-my-posh`.

    upgrade_os: false

Upgrade OS before installation.

## Dependencies

  - [elliotweiser.osx-command-line-tools][dep-osx-clt-role]

## Example Playbook

    - hosts: localhost
      vars:
        prompt_renderer: "oh-my-zsh"
        zsh_plugins:
          - zsh-autosuggestions
          - zsh-syntax-highlighting        
      roles:
        - pincher95.pimpmyshell

See the `tests/local-testing` directory for an example of running this role over
Ansible's `local` connection. See also:
[Mac Development Ansible Playbook][mac-dev-playbook].

## License

[MIT][link-license]

## Author Information

This role was created in 2022 by [Yuri Tsuprun]

#### Maintainer(s)

- [Yuri Tsuprun](https://github.com/pincher95)
