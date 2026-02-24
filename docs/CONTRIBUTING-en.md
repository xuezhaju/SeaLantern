# Contribution Guide

Switch Language (Change Language)

[简体中文](CONTRIBUTING.md)

[English Version Doc (Current)](CONTRIBUTING-en.md)

Thank you for your interest in the Sea Lantern project! This document will help you understand how to contribute to the project.

## Development Environment Requirements

- **Node.js**: 20+
- **Rust**: 1.70+
- **pnpm**: 9.15.9 (It is recommended to use the package manager specified by the project)
- **Git**: Latest version

## Code Standards

### Rust Code Standards

1. **Formatting**

   ```bash
   # Must be run before committing
   cargo fmt --all
   ```

2. **Linting**

   ```bash
   # Must pass all clippy checks
   cargo clippy --workspace -- -D warnings
   ```

3. **Naming Conventions**
   - File names: Use `snake_case` (e.g., `server_manager.rs`)
   - Function names: Use `snake_case` (e.g., `get_server_list`)
   - Struct names: Use `PascalCase` (e.g., `ServerInstance`)
   - Constants: Use `SCREAMING_SNAKE_CASE` (e.g., `MAX_MEMORY`)

4. **Comment Standards**
   - Public APIs must have documentation comments (`///`)
   - Complex logic requires inline comments (`//`)
   - Avoid meaningless comments

5. **Error Handling**
   - Use `Result<T, String>` to return errors
   - Error messages should be clear and user-friendly
   - Avoid using `unwrap()`, prefer `?` or `unwrap_or`

### Frontend Code Standards

1. **Vue Components**
   - Component names use `PascalCase` (e.g., `ServerCard.vue`)
   - Use `<script setup>` syntax
   - Props and emits must have defined types

2. **TypeScript**
   - Enable strict mode
   - Avoid using `any`, prefer specific types
   - Interface names use `PascalCase`

3. **Styling**
   - Use CSS variables (`var(--sl-*)`)
   - Avoid hardcoding color values
   - Use scoped styles

4. **Formatting and Linting**

   ```bash
   # Format code
   pnpm run fmt

   # Check formatting
   pnpm run fmt:check

   # Lint check
   pnpm run lint

   # Auto-fix lint issues
   pnpm run lint:fix
   ```

5. **Variable Reference Checks**
   - Specify clear types when declaring variables
   - Avoid using `any`, use specific types
   - Specify generic types when using `ref<T>` or `reactive`

### UI Components and Icons

- **Prioritize using Headless UI (Vue v1) and on-demand icon libraries (like Lucide)**:
  - Headless UI (https://headlessui.com/v1/vue) provides unstyled, accessible interactive components (such as `Listbox`, `Disclosure`, `Dialog`). It is recommended to reuse them when complex interactions (popups, collapsible sections, accessible keyboard support) are needed, reducing manual DOM and keyboard/ARIA handling.
  - Use on-demand icon component libraries for icons (like Lucide: https://lucide.dev/icons/ or example icons like https://lucide.dev/icons/paint-roller?search=Palette). Avoid hardcoding a large number of `<svg>` paths or duplicating DOM within the project. On-demand imports help keep the bundle size small and improve maintainability.
  - Recommended practice: Use Headless UI's `Listbox` to replace custom dropdown/selectors; use Lucide's icon components (e.g., `Palette` / `Paint-roller`) to replace hardcoded icons.

  This reduces redundant DOM, unifies accessibility handling, and separates styling from behavior, making maintenance easier.

## Git Workflow

### Branch Naming

- `feature/function-name` - New feature
- `fix/issue-description` - Bug fix
- `chore/task-description` - Miscellaneous tasks
- `docs/documentation-description` - Documentation updates

### Commit Convention

Use Conventional Commits:

```
<type>: <short description>

<detailed description> (optional)

Co-Authored-By: contributor-name <email>
```

**Types**:

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation update
- `style`: Code formatting (no functional changes)
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `test`: Test-related
- `chore`: Build/toolchain related

**Examples**:

```
feat: add server backup feature

- Implement incremental backup
- Support automatic backup scheduling
- Add backup restoration function
```

### Pull Request Process

1. **Fork the project and create a branch**

   ```bash
   git checkout -b feature/your-feature
   ```

2. **Develop and commit**

   ```bash
   # Ensure code passes checks
   cargo fmt --all
   cargo clippy --workspace -- -D warnings
   pnpm run fmt
   pnpm run lint
   pnpm run build

   # Commit changes
   git add .
   git commit -m "feat: your feature description"
   ```

3. **Push and create a PR**

   ```bash
   git push origin feature/your-feature
   ```

4. **PR Title and Description**
   - Title should be concise and clear (max 70 characters)
   - Description should include:
     - Summary of changes
     - Testing methods
     - Related Issues (if any)

## Code Review Standards

### Mandatory Requirements

- ✅ Passes all CI checks
- ✅ Code formatting is correct (cargo fmt / oxfmt)
- ✅ No clippy warnings
- ✅ No oxlint warnings
- ✅ Functionality is complete and usable
- ✅ No obvious performance issues

### Recommended Requirements

- Appropriate comments are present
- Relevant tests are included (if applicable)
- Related documentation has been updated
- UI changes adhere to design specifications

## Frequently Asked Questions

### How to run the development environment?

```bash
pnpm install
pnpm run tauri dev
```

### How to build a release version?

```bash
pnpm run tauri build
```

### What if Clippy checks fail?

1. Check the specific warning messages
2. Run `cargo clippy --fix` for automatic fixes (for some issues)
3. Manually fix the remaining issues
4. If some warnings are unreasonable, use `#[allow(clippy::...)]` annotations

### What if formatting checks fail?

```bash
cargo fmt --all
```

## Getting Help

- Ask questions in the Issues section
- Contact the maintainers
- Review the project documentation

## Code of Conduct

- Respect all contributors
- Remain friendly and professional
- Accept constructive feedback
- Help new contributors

---

Thank you again for your contribution!
