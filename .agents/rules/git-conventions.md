# Git Commit Conventions

All commits in this repository must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification in English.

## Format
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Types
- `feat`: A new feature (e.g., `feat(api): add recipe controller`)
- `fix`: A bug fix (e.g., `fix(api): correct validation logic`)
- `docs`: Documentation changes (e.g., `docs: update api endpoints in readme`)
- `style`: Formatting or code style changes (no production code behavior change)
- `refactor`: Refactoring code that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding or correcting tests
- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to CI/CD configuration files and scripts
- `chore`: Maintenance tasks, repo setup, git config, etc.

## Guidelines
- Write messages in English.
- Use the imperative mood in the description ("add", not "added" or "adds").
- Keep descriptions concise, in lowercase, and without a trailing period.
