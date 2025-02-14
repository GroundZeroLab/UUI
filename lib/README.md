# UUI

## Description

**UUI** (Unified User Interface) is a Svelte library designed to simplify and accelerate the creation of user interfaces. With UUI, you can easily build consistent, reusable UI components that seamlessly integrate into your Svelte projects. Whether you're building complex web apps or small projects, UUI offers a robust foundation to get started quickly.

## Features

- **Reusable Components**: A wide array of customizable, reusable Svelte components to streamline UI development.
- **Effortless Styling**: Easy-to-style components that fit your design language, making your UI look polished and consistent.
- **Real-time Development**: Quickly set up a development server with hot-reloading to preview changes instantly.
- **Lightweight and Fast**: Built with performance in mind, leveraging Svelte's compiled nature for highly optimized code.

## Installation

To get started, install UUI with your preferred package manager:

```bash
bun install @gzlab/uui
# OR
pnpm add @gzlab/uui
# OR
yarn add @gzlab/uui
# OR
npm install @gzlab/uui
```

## Getting Started

Once installed, you can start using UUI components in your Svelte project. Here’s a quick example:

### Basic Usage

```svelte
<script>
  import { Button } from '@uui/svelte/input/Button.svelte';
</script>

<Button onClick={() => alert('Button clicked!')}>Click Me!</Button>
```

This example demonstrates how easy it is to import and use a component from UUI. Customize it as needed to fit your design.

## Documentation

For full documentation and examples, visit the [official UUI docs](#) (link to be added). There you'll find detailed instructions for every component, configuration options, and customization guides.

## Development

If you'd like to contribute or modify UUI components, clone the repository and run the development server:

```bash
git clone https://github.com/GroundZeroLab/UUI
cd UUI/lib
bun dev  # OR pnpm dev / npm run dev
```

This will launch a development server, where you can see your changes in real-time.

## Build

To build the library for production or publishing:

```bash
bun build  # OR pnpm build / npm run build
```

This will compile your components, ready to be published on npm.

## License

UUI is licensed under the [MIT License](#). See the LICENSE file for more details.
