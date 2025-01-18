# Project template

This is base project template that I want to use in new projects. Replace all text in this README to actual project
information.

## Installing

1. Merge these repo to new project.
2. Create and activate virtual environment:
    ```bash
    python -m venv .venv
    .venv\Scripts\activate.bat  # Windows
    source .venv/bin/activate  # Linux and MacOS
    ```
3. Install dependencies:
    ```bash
    pip install uv
    uv pip sync requirements.txt dev_requirements.txt
    ```
4. Install `pre-commit`:
    ```bash
    pre-commit install
    ```

## Usage

### Adding new dependencies

1. Install this package to your virtual environment to check that this package can be installed and know it's version:
   ```bash
   uv pip install package
   ```
2. Add new package to `pyproject.toml`. There are 2 places where you can add it depending on what this package is being
added for:
   - If it's adding new functionality to your project, then add it to `dependencies` list.
   - If it's using only for developing (linters, `pre-commit`, `pytest` and other developer's stuff), then add it to
   `project.optional-dependencies` section. There are already exists 3 list fields for package installer (`installer`),
   developer's tools (`dev_tools`) and tools for testing (`test_tools`).
3. Compile `requirements.txt` file with command:
   ```bash
   uv pip compile pyproject.toml -o requirements.txt
   ```
4. Also compile `dev_requirements.txt` file with command:
   ```bash
   uv pip compile pyproject.toml --all-extras -o dev_requirements.txt
   ```
5. Check that `requirements.txt` and `dev_requirements.txt` not conflicting with each other:
   ```bash
   uv pip sync requirements.txt dev_requirements.txt
   ```

Remember that `dev_requirements.txt` contain all packages of your project, and you **must compile it anyway even you
adding not developer's package**. In most cases developers must install dependencies from this file with one of these
commands:
```bash
pip install -r dev_requirements.txt
uv pip sync requirements.txt dev_requirements.txt
uv pip install -r pyproject.toml --all-extras
```

When you're building your project (in docker image for example), you must use `requirements.txt` file to install
dependencies that will really use in your project:

```bash
pip install -r requirements.txt
uv pip sync requirements.txt
uv pip install -r pyproject.toml
```

### Pre-commit hooks

When you install `pre-commit` package, every time when you will commit your changes it will be checked hooks `ruff` and
`mypy`. If they found errors in your code, they will show them and deny commit until you not fix them.

If you want to add new pre-commit hook or disable one of them, you can change `.pre-commit-config.yaml`. Also, you can
configure how they should run. Specific settings for `ruff` and `mypy` placed in `pyproject.toml`.

To run pre-commit hooks manually, use this command:

```bash
.git/hooks/pre-commit
```

## Roadmap

- [X] First step
- [X] Second step
- [ ] ???
- [ ] PROFIT!!!!111
