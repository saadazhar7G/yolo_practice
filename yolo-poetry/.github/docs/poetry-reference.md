---
description: Poetry dependency management and virtual environment reference
applyTo: '**'
---

# Poetry Reference Guide

## Virtual Environment Management

### Configuration
```bash
# Set venv inside project (creates .venv folder)
poetry config virtualenvs.in-project true

# Check current config
poetry config --list
```

### Creating/Using Environments
```bash
# Create venv with specific Python version
poetry env use python3.10
poetry env use python3.11

# Get environment info
poetry env info
poetry env info --path

# List all environments
poetry env list

# Remove environment
poetry env remove python3.10
```

### Activation
```bash
# Poetry 2.0+ activation (get command first)
poetry env activate
# Then run the output: source /path/to/.venv/bin/activate

# Manual activation (if virtualenvs.in-project=true)
source .venv/bin/activate
deactivate  # to exit

# Run commands without activating (recommended)
poetry run python script.py
poetry run pytest
poetry run uvicorn main:app
```

## Dependency Management

### Adding Dependencies
```bash
# Add to main dependencies
poetry add package-name
poetry add ultralytics opencv-python-headless

# Add with version constraints
poetry add "fastapi>=0.100.0"
poetry add "pytest~=7.4"

# Add to development group
poetry add --group dev pytest pytest-cov black ruff
poetry add -D pytest  # shorthand

# Add optional dependencies
poetry add --optional redis
```

### Removing Dependencies
```bash
# Remove from main dependencies
poetry remove package-name

# Remove from dev group
poetry remove --group dev pytest
```

### Installing Dependencies
```bash
# Install all dependencies (from poetry.lock)
poetry install

# Install without dev dependencies
poetry install --without dev

# Install only specific groups
poetry install --only main
poetry install --with dev

# Update all dependencies
poetry update

# Update specific package
poetry update ultralytics
```

### Viewing Dependencies
```bash
# List all installed packages
poetry show

# Show dependency tree
poetry show --tree

# Show specific package info
poetry show ultralytics

# Show outdated packages
poetry show --outdated
```

## Project Management

### Creating Projects
```bash
# Create new project with structure
poetry new my-project

# Create project in existing folder
poetry init
```

### Lock File
```bash
# Generate/update poetry.lock
poetry lock

# Verify lock file is up to date
poetry lock --check
```

### Building & Publishing
```bash
# Build distribution packages
poetry build

# Publish to PyPI
poetry publish

# Build and publish
poetry publish --build
```

## Running Commands

### Basic Execution
```bash
# Run Python scripts
poetry run python script.py
poetry run python -m module_name

# Run installed CLI tools
poetry run pytest
poetry run black .
poetry run uvicorn app:main --reload
```

### Scripts (defined in pyproject.toml)
```toml
[tool.poetry.scripts]
train = "yolo_poetry.cli:train"
detect = "yolo_poetry.cli:detect"
```

```bash
# Run custom scripts
poetry run train
poetry run detect --image data/sample.jpg
```

## pyproject.toml Best Practices

### Basic Structure
```toml
[tool.poetry]
name = "yolo-poetry"
version = "0.1.0"
description = "YOLO object detection service"
authors = ["Your Name <email@example.com>"]
readme = "README.md"
packages = [{include = "yolo_poetry", from = "src"}]

[tool.poetry.dependencies]
python = "^3.10"
ultralytics = "^8.3.240"
opencv-python-headless = "^4.12.0"

[tool.poetry.group.dev.dependencies]
pytest = "^8.0.0"
pytest-cov = "^4.1.0"
black = "^24.0.0"
ruff = "^0.1.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

### Dependency Groups
```toml
[tool.poetry.group.test]
optional = false

[tool.poetry.group.test.dependencies]
pytest = "^8.0.0"
pytest-cov = "^4.1.0"

[tool.poetry.group.docs]
optional = true

[tool.poetry.group.docs.dependencies]
mkdocs = "^1.5.0"
```

### Version Constraints
```toml
# Caret (compatible, default): ^1.2.3 → >=1.2.3 <2.0.0
package = "^1.2.3"

# Tilde (patch updates): ~1.2.3 → >=1.2.3 <1.3.0
package = "~1.2.3"

# Exact version
package = "1.2.3"

# Range
package = ">=1.2.3,<2.0.0"

# Wildcard
package = "1.2.*"

# Multiple constraints
package = [
    {version = "^1.2", python = "^3.10"},
    {version = "^2.0", python = "^3.11"}
]
```

## Troubleshooting

### Common Issues
```bash
# Cache issues
poetry cache clear pypi --all

# Rebuild lock file
rm poetry.lock
poetry lock

# Force reinstall
poetry install --sync

# Check for configuration issues
poetry check

# Verbose output for debugging
poetry install -vvv
```

### Virtual Environment Not Found
```bash
# Recreate environment
poetry env remove python3.10
poetry env use python3.10
poetry install
```

### Dependency Conflicts
```bash
# See why package is required
poetry show --tree | grep package-name

# Update resolver
poetry update --lock

# Force resolution
poetry add package-name --lock
```

## Useful Tips

### Performance
- Use `poetry install --no-root` for CI/CD if you don't need the project installed
- Use `poetry export -f requirements.txt` to generate requirements.txt for Docker
- Enable parallel installation: `poetry config installer.parallel true`

### Security
- Regularly update dependencies: `poetry update`
- Check for vulnerabilities: `poetry show --outdated`
- Pin critical dependencies to specific versions

### Team Collaboration
- Always commit `poetry.lock` to version control
- Document Python version requirements in README
- Use `poetry install --sync` to match exact lock file state
- Consider using `poetry check` in CI/CD pipelines

## Quick Reference

| Task | Command |
|------|---------|
| Add package | `poetry add package-name` |
| Add dev package | `poetry add -D package-name` |
| Install all deps | `poetry install` |
| Update all deps | `poetry update` |
| Run script | `poetry run python script.py` |
| Run tests | `poetry run pytest` |
| Activate venv | `poetry env activate` (then run output) |
| Show packages | `poetry show` |
| Check config | `poetry config --list` |
| Build project | `poetry build` |

## Additional Resources

- Official Documentation: https://python-poetry.org/docs/
- CLI Reference: https://python-poetry.org/docs/cli/
- Configuration: https://python-poetry.org/docs/configuration/
- Managing Environments: https://python-poetry.org/docs/managing-environments/
