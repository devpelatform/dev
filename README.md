# Pelatform Dev

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Bun](https://img.shields.io/badge/bun-1.3.3-black)](https://bun.sh)

A collection of utility packages for building modern SaaS applications. This monorepo contains reusable packages for email sending, storage management, and common utility functions.

## Packages

| Package                                  | Version                                                                                                         | Description                                                 |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| [@pelatform/email](./packages/email)     | [![npm](https://img.shields.io/npm/v/@pelatform/email.svg)](https://www.npmjs.com/package/@pelatform/email)     | Email templates and sending utilities (Resend, Nodemailer)  |
| [@pelatform/storage](./packages/storage) | [![npm](https://img.shields.io/npm/v/@pelatform/storage.svg)](https://www.npmjs.com/package/@pelatform/storage) | Unified storage interface (S3, Cloudinary, R2, MinIO, etc.) |
| [@pelatform/utils](./packages/utils)     | [![npm](https://img.shields.io/npm/v/@pelatform/utils.svg)](https://www.npmjs.com/package/@pelatform/utils)     | Common utility functions for SaaS applications              |

## Tech Stack

- **Package Manager**: Bun
- **Monorepo Tool**: Turborepo
- **Build Tool**: tsup
- **Linting/Formatting**: Biome
- **Language**: TypeScript

## Getting Started

### Prerequisites

- [Bun](https://bun.sh) 1.3.3 or higher
- Node.js 20 or higher

### Installation

```bash
# Clone the repository
git clone https://github.com/devpelatform/dev.git
cd dev

# Install dependencies
bun install
```

### Common Commands

```bash
# Development
bun dev                    # Run all packages in dev mode with watch
bun build                  # Build all packages
bun types:check            # Type-check all packages

# Linting and Formatting
bun lint                   # Lint code with Biome (auto-fix)
bun format                 # Format code with Biome
bun lint:format            # Lint and format together (includes unsafe fixes)

# Package Management
bun clean                  # Clean build outputs in all packages
bun clean:all              # Deep clean (remove .turbo, bun.lock, node_modules)
```

### Working on Individual Packages

```bash
# Navigate to a package
cd packages/email

# Run package commands
bun dev                    # Development mode with watch
bun build                  # Build the package
bun types:check            # Type-check the package
```

## Development Workflow

1. **Create a branch** for your changes
2. **Make your changes** in the appropriate package(s)
3. **Run tests** and type-check: `bun types:check`
4. **Format your code**: `bun lint:format`
5. **Commit your changes** following conventional commits
6. **Submit a pull request**

For detailed contribution guidelines, see [CONTRIBUTING.md](./CONTRIBUTING.md).

## Contributing

We welcome contributions! This project is community-driven and your help makes it better.

**Getting Started:**

- Read the [Contributing Guide](./CONTRIBUTING.md) for development setup and guidelines
- Check the [Code of Conduct](./CODE_OF_CONDUCT.md)
- Browse [open issues](https://github.com/devpelatform/dev/issues) or start a [discussion](https://github.com/devpelatform/dev/discussions)

## Security

If you discover a security vulnerability, please send an email to **pelatformdev@gmail.com**. All security vulnerabilities will be promptly addressed.

Do not report security issues through public GitHub issues.

## License

MIT License - see [LICENSE](./LICENSE) for details.

By contributing to Pelatform Dev, you agree that your contributions will be licensed under the MIT License.
