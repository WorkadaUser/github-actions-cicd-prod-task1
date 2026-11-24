# Python Inventory Management — GitHub Actions CI/CD

A production-style Python application demonstrating automated testing, dependency caching, package building, and versioned releases using GitHub Actions.

## Features

- Inventory management with product additions and stock removal
- Stock quantity tracking and inventory valuation
- Input validation and error handling
- Automated unit testing with pytest
- Multi-version Python testing
- Dependency caching for faster CI execution
- Automated Python package builds
- GitHub Releases triggered by version tags

## Project Structure

```text
.github/workflows/
  ci.yml                 # Continuous Integration
  release.yml            # Automated GitHub Releases
src/inventory_app/
  __init__.py
  inventory.py           # Inventory management logic
tests/
  test_inventory.py      # Unit tests
pyproject.toml           # Package configuration
README.md                # Project documentation
```

## Requirements

- Python 3.11 or newer
- pip
- Git

## Installation

Clone the repository:

```bash
git clone https://github.com/WorkadaUser/github-actions-cicd-prod-task1.git
cd github-actions-cicd-prod-task1
```

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the application and test dependencies:

```bash
python -m pip install -e ".[test]"
```

## Running Unit Tests

```bash
python -m pytest -v
```

The project includes 11 automated tests covering inventory operations, input validation, insufficient stock, and inventory valuation.

## CI Pipeline

Workflow: `.github/workflows/ci.yml`

The pipeline runs automatically on pushes to `main`, pushes to `feature/**` branches, and pull requests targeting `main`.

### Pipeline Stages

1. Checkout the repository.
2. Run tests using a matrix of Python 3.11, 3.12, and 3.13.
3. Cache pip dependencies to improve execution efficiency.
4. Build Python wheel and source distributions after successful testing.
5. Upload downloadable build artifacts to GitHub Actions.

## Release Pipeline

Workflow: `.github/workflows/release.yml`

The release pipeline runs when a version tag matching `v*.*.*` is pushed.

### Release Process

1. Checkout the tagged source code.
2. Set up Python and install dependencies.
3. Run automated unit tests.
4. Build wheel and source distributions.
5. Validate that the Git tag matches the version in `pyproject.toml`.
6. Publish a GitHub Release with downloadable distribution files.

### Creating a New Release

Update the version in `pyproject.toml`, commit the change, and merge it into `main`.

Then create and push a matching tag:

```bash
git switch main
git pull --ff-only origin main
git tag -a v1.0.1 -m "Release version 1.0.1"
git push origin v1.0.1
```

The release workflow will validate the tag and publish the package automatically.

## Build Locally

```bash
python -m pip install build
python -m build
```

Generated distributions are written to the `dist/` directory.

## Validation Results

Initial release: `v1.0.0`

- 11 unit tests passed locally.
- CI testing passed on Python 3.11, 3.12, and 3.13.
- Wheel and source distributions built successfully.
- GitHub Actions build artifacts uploaded successfully.
- Automated GitHub Release v1.0.0 published successfully.

## Security and Permissions

The CI workflow uses read-only repository permissions.

The release job uses `contents: write` only for publishing GitHub Releases.

No production credentials or customer data are required.

## License

MIT License.
