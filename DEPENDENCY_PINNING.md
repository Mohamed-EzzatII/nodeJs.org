Here’s a structured version of the **Dependency Pinning** policy for the Node.js Website:

---

# Dependency Pinning Policy

Based on initial discussions in [this thread](https://github.com/nodejs/nodejs.org/discussions/5491), we’ve adopted a strict strategy for managing npm dependencies within the Node.js Website. This approach aims to maintain stability and prevent build or runtime issues due to unexpected dependency updates, particularly from packages that may not adhere to semantic versioning.

## Purpose

Pinning dependencies ensures the website and build process remain stable, as dependencies stay fixed at a specific version. Dependabot will continue to provide security alerts when vulnerabilities arise in these dependencies, helping us address them promptly.

---

## Guidelines for Adding Dependencies

Consider the following recommendations when adding new dependencies:

1. **Dependency Categories:**
   - **`dependencies`:** Should include any packages that are essential to the build process or runtime functionality of the website.
     - Some non-code dependencies (e.g., `husky`, `lint-staged`) are required for setup scripts or Git hooks.
   - **`devDependencies`:** Should include any packages not invoked in the codebase, used solely in the development environment.
     - Examples: Type packages, utilities, tooling, and test frameworks such as `jest` or `storybook`.
   - **`peerDependencies`:** Should include any runtime dependencies that the website requires but doesn’t install directly.
     - Examples: `react`, `react-dom`.

2. **Dependency Pinning:**
   - **Exact Version (`--save-exact`):** Use this for CLI and tooling dependencies (e.g., `husky`, `prettier`, `jest`).
   - **`~` Version Range:** Use this for patch updates, particularly in development or testing dependencies where only bug fixes are required (e.g., `storybook`).
   - **`^` Version Range:** Use this for application dependencies where new features and bug fixes are desired (e.g., `react`, `next-intl`).
     - If not interested in the latest features, consider using `~` instead.
   - **Node.js-Specific Build Tools:** For dependencies in scripts or during the build process (not in application code), use `~` (e.g., `glob`, `@nodevu/core`).
   - **TypeScript Type Packages:** Follow the same semantic versioning as the corresponding package.

---

## Manual Dependency Updates

This policy aims to guide the management of dependencies thoughtfully, avoiding excess complexity and improving maintainability. To support this:

- **Avoid unnecessary dependencies**: Only add new dependencies when absolutely necessary.
- **Dependabot updates**: Let Dependabot manage dependency updates unless an immediate update is required due to breaking changes or if specific new features are needed.

### Exceptions for Manual Updates

1. **Node.js Version Updates**: Manual updates are allowed for the Node.js version defined in `.nvmrc`, along with the corresponding `@types/node` dependency, which should match the Node.js major version.
2. **Lockfile and Version Constraints**: Avoid manual `package-lock.json` and `package.json` changes in pull requests unless explicitly needed.

This strategy helps ensure that our dependencies are controlled, reducing maintenance challenges and improving the reliability of the Node.js Website.