# Contributing to proj2md

Thank you for your interest in contributing to proj2md! We welcome all
contributions.

## How to Contribute

1. Fork the repository on GitHub.
2. Create your feature branch:
   ```bash
   git checkout -b feature/YourFeature
   ```
3. Commit your changes:
   ```bash
   git commit -m "type(scope): description"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/YourFeature
   ```
5. Open a pull request and describe your changes.

## Development Setup

Clone the repository and install dependencies:

```bash
git clone https://github.com/thibaud-perrin/proj2md.git
cd proj2md
pip install -e .
```

## Code Style

Follow ruff configuration present in the pyproject.toml

## Testing

Write tests under `tests/` using `pytest` and run:

```bash
pytest
```

## Continuous Integration

This project uses GitHub Actions for CI. Ensure your PR passes all checks before
requesting a review.

Thank you for making proj2md better!
