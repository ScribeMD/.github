# Contributing Guide

<!--TOC-->

- [Contributing Guide](#contributing-guide)
  - [Setup](#setup)
  - [Expectations](#expectations)
  - [Editors](#editors)

<!--TOC-->

## Setup

- [Install Docker](https://docs.docker.com/get-docker/).
- [Install asdf](https://asdf-vm.com/guide/getting-started.html) to
  automatically manage the versions of the needed programming languages and
  tools based on the contents of [`.tool-versions`](.tool-versions).
- Add the following to the bottom of your `~/.bashrc`:

  ```bash
  source ~/.asdf/asdf.sh
  source "$ASDF_DIR/completions/asdf.bash"
  ```

- Close and relaunch Ubuntu to source your `~/.bashrc`.
- [Install Python's build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment).
- If `.tool-versions` contains `ruby`,
  [install Ruby's build dependencies](https://github.com/rbenv/ruby-build/wiki#suggested-build-environment).
- Change directories to the root of this repository.
- Add the asdf plugin for all tools in [`.tool-versions`](.tool-versions) (e.g.,
  run `asdf plugin add nodejs` to install the Node.js plugin for asdf).
- Run `asdf install` to install all asdf-managed tools at the pinned versions.
- Run `poetry env use "$(asdf which python)"` to instruct Poetry to use the
  asdf-managed Python.
- Run `poetry install --sync` to install all Python dependencies.
- Run `poetry shell` to activate the Poetry virtual environment.
- Install all pre-commit hooks by running `pre-commit install --install-hooks`.
- Create a `~/.ssh/config` file with the following contents:

  ```ssh-config
  Host github.com
    AddKeysToAgent yes
    # This may need to be modified to match the path to your private key.
    IdentityFile ~/.ssh/id_ed25519
    # Prevent GitHub from timing out pushes since we run intense pre-push hooks.
    ServerAliveInterval 5
    ServerAliveCountMax 360
  ```

## Expectations

- If you are new to open source, welcome.
  [Here is a guide to getting started.](https://opensource.guide/how-to-contribute/)
- New features are generally welcome.
- For non-trivial issues, you may save yourself time by filing an issue first
  so we can discuss how best to address your proposal.
- Thoroughly review [`README.md`](README.md), and include any pertinent changes
  to the documentation in your change.
- The purpose of pre-commit hooks is to automate the trivial aspects of code
  review. Please address all issues found by pre-commit hooks that they don't
  fix automatically before opening a pull request. If you are stumped, please
  consult the documentation of the tool run by the failing hook. If you are
  still stumped, ask questions in an appropriate forum, such as
  [Stack Overflow](https://stackoverflow.com/), a tool-specific forum, or your
  work Slack if applicable. If you are still stumped, please open an issue
  explaining what you have tried so far.
- We use the Python-based
  [Commitizen](https://commitizen-tools.github.io/commitizen/), not to be
  confused with the Node.js-based
  [Commitizen](https://commitizen.github.io/cz-cli/). This helps to maintain a
  clear revision history. The
  [Test](.github/workflows/test.yaml) workflow automatically bumps
  the project version in [`pyproject.toml`](pyproject.toml), appends to
  [`CHANGELOG.md`](CHANGELOG.md), and tags versions.
  You can either write
  [Conventional Commits](https://www.conventionalcommits.org/) by hand or run
  `cz commit` from within the Poetry virtual environment for guidance.

## Editors

[VSCode](https://code.visualstudio.com/) is recommended as this repository
configures it to run many of our linters as you edit.

- When prompted, install the extensions recommended by the workspace.
- When prompted, select the Python interpreter from the virtual environment
  Poetry created for this repository.
