# Contributing

Thanks for helping. Anyone can open an issue or a pull request. Pairwise maintainers review and merge every change.

## Good contributions

- Fixes to the connection steps, for example when an assistant changes its settings screens.
- Steps for an assistant that is not listed yet, after you have connected it yourself.
- Improvements to a skill, or a new skill, checked against [docs/QUALITY_BAR.md](docs/QUALITY_BAR.md).

## How to contribute

1. Open an issue first for anything larger than a small fix, so we can agree on the approach.
2. Keep each pull request small: one fix, or one skill.
3. Follow the rules in [AGENTS.md](AGENTS.md). They apply to people and AI agents alike.
4. Use synthetic examples only. Never include real candidate, company or account data.

## Pull request descriptions

Everything in this repo is public, including pull request descriptions and commit messages. Use these sections:

- **Summary:** what the change does, in 1-2 sentences.
- **What changed:** the files or sections changed.
- **Why:** the reasons for the main choices, in product terms.
- **How to check:** steps any reader can repeat, for example `claude plugin validate .` or following a setup section.

Leave out anything a reader outside Pairwise cannot check or should not see: account details, real counts or names from Pairwise data, internal links, and private discussions.

## Security

Do not report security issues in a public issue or pull request. See [SECURITY.md](SECURITY.md).

## License

By contributing, you agree that your contribution is licensed under the [MIT License](LICENSE).
