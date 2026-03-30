# Commitish

A simple, lightweight commitizen-like tool for creating standardized Git commit messages following the [Conventional Commits](https://www.conventionalcommits.org/) format.

![](https://i.imgur.com/aZdFjsa.gif)

## 📖 Overview

Commitish streamlines your Git workflow by helping you craft well-formatted commit messages without needing to remember the conventional commits syntax. It provides an interactive interface to select commit types, add scopes, and include detailed descriptions when needed.

## ✨ Features

- Interactive commit type selection using fuzzy search
- Support for all standard conventional commit types
- Optional scoping of commits
- Optional multi-line commit body
- Breaking changes notation
- Verification of Git repository and staged changes

## 🔧 Dependencies

- [fzf](https://github.com/junegunn/fzf) - Command-line fuzzy finder
- Git

## 🚀 Installation

1. Download the scripts:

```bash
curl -o /usr/local/bin/commitish https://raw.githubusercontent.com/victor141516/commitish/refs/heads/master/commitish
curl -o /usr/local/bin/commitish-ai https://raw.githubusercontent.com/victor141516/commitish/refs/heads/master/commitish-ai
```

2. Make the scripts executable:

```bash
chmod +x /usr/local/bin/commitish /usr/local/bin/commitish-ai
```

3. Source the script in your shell configuration file (`.bashrc`, `.zshrc`, etc.):

```bash
echo 'source /usr/local/bin/commitish' >> ~/.zshrc
```

4. For AI features, set your OpenAI API key:

```bash
echo 'export OPENAI_API_KEY=your_api_key' >> ~/.zshrc
```

### ZSH Tab Completion

For ZSH shell autocomplete support:

1. Download the completion file:

```bash
curl -o ./_commitish https://raw.githubusercontent.com/victor141516/commitish/refs/heads/master/_commitish
```

2. Move it to your ZSH functions directory:

```bash
chmod +x ./_commitish
sudo cp ./_commitish /usr/local/share/zsh/site-functions/_commitish
```

3. Restart your shell or run:

```bash
autoload -U _commitish
```

## 📋 Usage

Basic usage:

```bash
commitish
```

This will prompt you to:

1. Select a commit type (feat, fix, docs, etc.)
2. Optionally provide a scope
3. Enter a commit message
4. Optionally specify breaking changes

### Examples

Start with a specific commit type:

```bash
commitish fix  # Pre-selects the "fix" type
```

Include a multi-line commit body:

```bash
commitish -b
```

Combine type and body flag:

```bash
commitish feat -b
```

### Options

```
-h, --help     Show the help message and exit
-b, --body     Include a commit body (multi-line description)
--no-verify    Skip git hooks (passes --no-verify to git commit)
--ai           Use AI to suggest commit details (requires OPENAI_API_KEY)
```

### AI Integration

The `--ai` option uses OpenAI to suggest commit type, scope, message, and body based on your staged changes.

**Requirements:**

- `OPENAI_API_KEY` environment variable set with your OpenAI API key
- `jq` installed (for JSON parsing)

**Setup:**

```bash
export OPENAI_API_KEY=your_api_key_here
```

**How it works:**

1. Analyzes your staged changes (git diff --cached)
2. Reviews your last 5 commits to understand your commit style
3. If you typically use scopes (e.g., `feat(api):`), it will suggest scopes
4. Makes parallel API calls to get suggestions for type, scope, message, and body
5. Prepopulates the interactive prompts with suggestions (you can accept or modify)

**Example:**

```bash
commitish --ai  # Get AI suggestions and interactively review/modify them
```

### Commit Types

| Type     | Description                                                   |
| -------- | ------------------------------------------------------------- |
| feat     | A new feature                                                 |
| fix      | A bug fix                                                     |
| docs     | Documentation only changes                                    |
| style    | Changes that do not affect the meaning of the code            |
| refactor | A code change that neither fixes a bug nor adds a feature     |
| perf     | A code change that improves performance                       |
| test     | Adding missing tests or correcting existing tests             |
| build    | Changes that affect the build system or external dependencies |
| ci       | Changes to CI configuration files and scripts                 |
| chore    | Other changes that don't modify src or test files             |
| revert   | Reverts a previous commit                                     |

## 🤝 Contributing

Contributions are welcome! Feel free to:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `commitish` 😉
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📜 License

[MIT License](LICENSE)

## 🙏 Acknowledgements

- [Conventional Commits](https://www.conventionalcommits.org/) for the commit message specification
- [commitizen](https://github.com/commitizen/cz-cli) for inspiration
