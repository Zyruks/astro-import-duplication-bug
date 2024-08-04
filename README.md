# Astro Import Duplication Bug Reproduction

This repository contains a minimal setup to reproduce the import duplication bug when using `organizeImports` in VSCode with Astro.

## Steps to Reproduce

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/Zyruks/astro-import-duplication-bug
   cd astro-import-duplication-bug
   ```

2. **Install Dependencies**:

   ```bash
   pnpm install
   ```

3. **Open the Project in VSCode**:

   ```bash
   code .
   ```

4. **Configure VSCode**:
   Ensure `organizeImports` is enabled in your VSCode settings:

   ```json
   {
     "editor.codeActionsOnSave": {
       "source.organizeImports": "explicit"
     }
   }
   ```

5. **Open the Example File**:
   Open `src/pages/index.astro` and observe the import statements.

6. **Save the File**:
   Save the file and observe the duplicated import statements.

## Expected Behavior

The import statements should not be duplicated upon saving the file.

## Actual Behavior

Import statements are duplicated upon saving the file, particularly when using import aliases from `tsconfig.json`.

## Environment

- OS: Windows 11 using WSL 2 with Ubuntu
- Astro version: v2.13.1 and v2.13.0
- VSCode extensions: astro-build.astro-vscode

## Additional Context

Disabling `organizeImports` resolves the issue temporarily. Please investigate potential conflicts between `organizeImports` and Astro's handling of import aliases.

## Configuration Files

- `tsconfig.json`:

  ```json
  {
    "exclude": ["./dist/"],
    "extends": "astro/tsconfigs/strict",
    "compilerOptions": {
      "baseUrl": "src",
      "strictNullChecks": true,
      "paths": {
        "@components": ["components"],
        "@layouts": ["layouts"]
      },
      "plugins": [
        {
          "name": "@astrojs/ts-plugin"
        }
      ]
    }
  }
  ```

- `.vscode/settings.json`:

  ```json
  {
    "editor.codeActionsOnSave": {
      "source.organizeImports": "explicit"
    }
  }
  ```

## Example File

- `src/pages/index.astro`:

  ```astro
  ---
  import { Layout } from '@layouts';
  import { Hero } from '@components';
  ---

  <Layout title="Kahop">
    <main>
      <Hero />
    </main>
  </Layout>
  ```
