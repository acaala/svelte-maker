# Svelte Maker ⚡️

A lightning-fast, Symfony Artisan-style CLI tool for generating SvelteKit routes, configs, and server files from the terminal. 

Stop manually creating deeply nested folders and boilerplate files. Let Svelte Maker do it for you.

## Installation

Currently, Svelte Maker is available directly via GitHub.

**Global Install:**
```bash
npm install -g github:acaala/svelte-maker
```

**Local Project Install:**
```bash
npm install -D github:acaala/svelte-maker
```

---

## Usage

If installed globally, you can run Svelte Maker using `npx`:

```bash
npx svelte-maker <command> [arguments] [flags]
```

### Commands

#### `init` (Optional Setup)
Initializes Svelte Maker in your project by safely injecting a `make:route` alias into your `package.json` scripts. This allows you to use the familiar Laravel/Symfony syntax for all future commands.

**Syntax:**
```bash
npx svelte-maker init
```
*After running `init`, you can simply run: `npm run make:route <path>`*

#### `route`
Generates a new route directory along with its corresponding SvelteKit files (`+page.svelte`, `+page.ts`, and `+page.server.ts`).

**Syntax:**
```bash
npx svelte-maker route <path> [routeName] [options]
```
*(Or `npm run make:route <path> [routeName] [options]` if initialized)*

**Arguments:**
* `<path>` *(Required)*: The directory path inside `src/routes/` where the files should be created. Supports deep nesting (e.g., `admin/users/[id]`).
* `[routeName]` *(Optional)*: A unique name for your route. If provided, Svelte Maker will generate a `+page.ts` file exporting this config name.

**Options:**
* `-n`, `--no-server`: Skips generating the `+page.server.ts` file. Ideal for static or purely client-side pages.
* `-js`, `--javascript`: Generates standard JavaScript files (`.js`) and strips TypeScript types from the templates. Defaults to TypeScript.

---

## Examples

**1. Create a standard full-stack route (TS by default):**
```bash
npx svelte-maker route admin/dashboard
```
*Generates:*
* `src/routes/admin/dashboard/+page.svelte`
* `src/routes/admin/dashboard/+page.server.ts`

**2. Create a deeply nested route with a Config Name:**
```bash
npx svelte-maker route "admin/users/[id]/settings" user_settings
```
*(Note: Use quotes around paths with brackets `[]` to prevent terminal globbing errors!)*
*Generates:*
* `src/routes/admin/users/[id]/settings/+page.svelte`
* `src/routes/admin/users/[id]/settings/+page.ts` *(Contains `name: 'user_settings'`)*
* `src/routes/admin/users/[id]/settings/+page.server.ts`

**3. Create a frontend-only JavaScript route:**
```bash
npx svelte-maker route marketing/about -n -js
```
*Generates:*
* `src/routes/marketing/about/+page.svelte` *(Without `lang="ts"`)*

---

## License

MIT
