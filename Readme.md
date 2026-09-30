![header](.github/header.jpg)

# Gary's Claude AI Tools

My personal configuration for [Claude Code](https://claude.com/claude-code): global
guidelines, a set of development skills, and a status line script.

## Contents

| Path            | What it is                                                      |
| --------------- | --------------------------------------------------------------- |
| `CLAUDE.md`     | Global guidelines applied to every project                      |
| `skills/`       | Claude Code skills for languages, testing, headers, and commits |
| `statusline.pl` | Status line showing model, context, rate-limit usage, and cost  |

## Skills

| Skill               | Purpose                                                                            |
| ------------------- | ---------------------------------------------------------------------------------- |
| `applescript-skill` | Create, compile, run, and debug AppleScript, including System Events GUI scripting |
| `bash-skill`        | Create, run, and debug Bash scripts                                                |
| `cpp-skill`         | Modern, memory-safe, cross-platform C++ with CMake                                 |
| `file-header-skill` | Add or update language-appropriate file header comments                            |
| `git-commit-skill`  | Generate commit messages that follow project conventions                           |
| `perl-skill`        | Create, run, debug, and test Perl 5 scripts and modules                            |
| `python3-skill`     | Create, run, debug, and test Python 3 scripts and packages                         |
| `tdd-skill`         | Kent Beck–style red → green → refactor test-driven development                     |

## Required Utilities

The skills call these command-line tools. Tools marked optional are used only when they
are installed.

| Skill               | Required                                       | Optional                              |
| ------------------- | ---------------------------------------------- | ------------------------------------- |
| `applescript-skill` | `osascript`, `osacompile` (macOS)              |                                       |
| `bash-skill`        | `bash`, `shellcheck`, `bats-core`              | `bashdb`                              |
| `cpp-skill`         | C++23 compiler, `cmake`, `ctest`, `uncrustify` | `cppcheck`, `lldb`, `gdb`, `valgrind` |
| `file-header-skill` | none                                           |                                       |
| `git-commit-skill`  | `git`                                          |                                       |
| `perl-skill`        | `perl`, `prove`, `perltidy`                    | `perlcritic`                          |
| `python3-skill`     | `python3` (3.10+), `pytest`, `ruff`, `mypy`    |                                       |
| `tdd-skill`         | the test runner for your language              |                                       |

On macOS, install the tools with Homebrew and CPAN:

```sh
brew install swiftformat shellcheck bats-core bashdb cmake uncrustify cppcheck perltidy pytest ruff mypy
cpan Perl::Critic
```

## Status Line

`statusline.pl` reads Claude Code's status JSON from stdin and prints a single line:

- Model name
- Context window usage bar
- 5-hour session usage bar and reset time
- 7-day usage bar and reset date
- Session cost in USD

Bars are green below 60%, yellow below 85%, and red at 85% and above. It uses only core
Perl modules (`JSON::PP`, `POSIX`, `Scalar::Util`).

## Installation

```sh
mkdir -p ~/.claude/skills
cp -i CLAUDE.md ~/.claude/CLAUDE.md
cp -R -i skills/* ~/.claude/skills/
cp -i statusline.pl ~/.claude/statusline.pl
```

`-i` asks before overwriting an existing file, so a CLAUDE.md, skill, or status line
you have already customized is not replaced silently.

Then enable the status line in `~/.claude/settings.json`:

```json
"statusLine": {
  "type": "command",
  "command": "/usr/bin/env perl ~/.claude/statusline.pl"
}
```

## Contributing

See [CONTRIBUTING.md](.github/CONTRIBUTING.md) and the
[Code of Conduct](.github/CODE_OF_CONDUCT.md).

## License

MIT — see [LICENSE.md](LICENSE.md).
