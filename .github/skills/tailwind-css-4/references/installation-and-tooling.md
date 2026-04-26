# Installation And Tooling

Sources used: Tailwind CSS docs for installation with Vite, PostCSS, Tailwind CLI, and editor setup.

## Core Build Model
- Tailwind CSS scans HTML files, JavaScript components, and other templates for class names.
- Tailwind generates the corresponding styles and writes them to a static CSS file.
- The docs describe Tailwind CSS as fast, flexible, reliable, and zero-runtime.

## Vite Plugin
The docs describe installing Tailwind CSS as a Vite plugin as the most seamless way to integrate with frameworks like Laravel, SvelteKit, React Router, Nuxt, and SolidJS.

```bash
npm create vite@latest my-project
cd my-project
npm install tailwindcss @tailwindcss/vite
```

```ts
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```

```css
@import "tailwindcss";
```

```bash
npm run dev
```

The compiled CSS must be included in the document `<head>`. The Vite example links `/src/style.css` and uses `text-3xl font-bold underline` in HTML.

## PostCSS Plugin
The docs describe installing Tailwind CSS as a PostCSS plugin as the most seamless way to integrate with frameworks like Next.js and Angular.

```bash
npm install tailwindcss @tailwindcss/postcss postcss
```

```js
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  },
}
```

```css
@import "tailwindcss";
```

```bash
npm run dev
```

The PostCSS example includes the compiled CSS in the `<head>` with `/dist/styles.css`.

## Tailwind CLI
The docs describe the Tailwind CLI as the simplest and fastest way to get running from scratch. The CLI is also available as a standalone executable for use without installing Node.js.

```bash
npm install tailwindcss @tailwindcss/cli
```

```css
@import "tailwindcss";
```

```bash
npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch
```

The CLI example links the compiled CSS file `./output.css` in `src/index.html`.

## Framework Guides
The installation pages direct users to Tailwind framework guides when setup differs across build tools or a project needs framework-specific instructions.

## Editor Syntax Support
- Tailwind CSS uses custom CSS syntax such as `@theme`, `@variant`, and `@source`.
- Editors that do not recognize these rules can show warnings or errors.
- The official Tailwind CSS IntelliSense extension for VS Code includes a dedicated Tailwind CSS language mode with support for Tailwind custom at-rules and functions.
- In strict editors, the docs say native CSS linting or validation may need to be disabled.

## VS Code IntelliSense
The official Tailwind CSS IntelliSense extension for Visual Studio Code provides:
- Autocomplete for utility classes, CSS functions, and directives.
- Linting for errors and potential bugs in CSS and markup.
- Hover previews that reveal complete CSS for utility classes.
- Syntax highlighting for Tailwind custom CSS syntax.

## Class Sorting With Prettier
- Tailwind maintains an official Prettier plugin for Tailwind CSS.
- The plugin automatically sorts classes using Tailwind's recommended class order.
- The docs state it works with custom Tailwind configurations and wherever Prettier works.

```html
<!-- Before -->
<button class="text-white px-4 sm:px-8 py-2 sm:py-3 bg-sky-700 hover:bg-sky-800">Submit</button>

<!-- After -->
<button class="bg-sky-700 px-4 py-2 text-white hover:bg-sky-800 sm:px-8 sm:py-3">Submit</button>
```

## Other Editor Notes
- Cursor supports VS Code extensions, so Tailwind CSS IntelliSense and the official Prettier plugin work there according to the docs.
- Zed has built-in support for Tailwind CSS autocompletions, linting, and hover previews, and integrates with Prettier.
- JetBrains IDEs such as WebStorm and PhpStorm include support for intelligent Tailwind CSS completions in HTML.