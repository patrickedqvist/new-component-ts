<p>
  <img src="https://github.com/patrickedqvist/new-component-ts/blob/main/docs/logo@2x.png?raw=true" width="285" height="285" alt="new-component logo">
  <br>
  <a href="https://www.npmjs.org/package/new-component-ts"><img src="https://img.shields.io/npm/v/new-component.svg?style=flat" alt="npm"></a>
</p>

This is a typescript variant, forked of the great work by Josh W Comeau [https://github.com/joshwcomeau/new-component](https://github.com/joshwcomeau/new-component)

# `new-component-ts`

### Simple, customizable utility for adding new Typescript React components to your project.

<img src="https://github.com/patrickedqvist/new-component-ts/blob/main/docs/divider@2x.png?raw=true" width="888" height="100" role="presentation">

Anyone else sick of writing the same component boilerplate, over and over?

This project is a globally-installable CLI for adding new React components. It's dead simple to use, and requires no configuration, although it's easy to customize it to fit your project's coding style.

<br />

## Features

- Simple CLI interface for adding React components.
- Uses [Prettier](https://github.com/prettier/prettier) to stylistically match the existing project.
- Offers global config, which can be overridden on a project-by-project basis.
- Colourful terminal output!

<br />

## Quickstart

Install via NPM:

```bash
# Using Yarn:
$ yarn global add new-component

# or, using NPM
$ npm i -g new-component
```

`cd` into your project's directory, and try creating a new component:

<p>
  <img src="https://github.com/patrickedqvist/new-component-ts/blob/main/docs/demo.gif?raw=true" width="888" height="369" alt="demo of CLI functionality">
</p>

Your project will now have a new directory at `src/components/Button`. This directory has two files:

```tsx
// `Button/index.tsx`
export { default } from './Button';
```

```tsx
// `Button/Button.tsx`
import type { FC } from 'react';

interface Props {}

const Button: FC<Props> = () => {
  return (
    return <div />
  )
}

export default Button;
```

> This structure might appear odd to you, with an `index.tsx` that points to a named file. I've found this to be an optimal way to set up components; the `index.tsx` allows you to `import` from the directory (eg. `import Button from 'components/Button'`), while having `Button.tsx` means that you're never lost in a sea of `index.tsx` files in your editor.
>
> This structure is not currently configurable, but I'm happy to consider implementing alternatives!

<br />

## Configuration

Configuration can be done through 3 different ways:

- Creating a global `.new-component-config.json` in your home directory (`~/.new-component-config.json`).
- Creating a local `.new-component-config.json` in your project's root directory.
- Command-line arguments.

The resulting values are merged, with command-line values overwriting local values, and local values overwriting global ones.

<br />

## API Reference

### Type

Control the type of component created:

- `functional` for a stateless functional component (default).
- `class` for a traditional Component class,
- `pure-class` for a PureComponent class,

Legacy `createClass` components are not supported.

**Usage:**

Command line: `--type <value>` or `-t <value>`

JSON config: `{ "type": <value> }`
<br />

### Directory

Controls the desired directory for the created component. Defaults to `src/components`

**Usage:**

Command line: `--dir <value>` or `-d <value>`

JSON config: `{ "dir": <value> }`
<br />

### File Extension

Controls the file extension for the created components. Can be either `js` (default) or `jsx`.

**Usage:**

Command line: `--extension <value>` or `-x <value>`

JSON config: `{ "extension": <value> }`
<br />

### Prettier Config

Delegate settings to Prettier, so that your new component is formatted as you'd like. Defaults to Prettier defaults.

For a full list of options, see the [Prettier docs](https://github.com/prettier/prettier#options).

**Usage:**

Command line: N/A (Prettier config is only controllable through JSON)

JSON config: `{ "prettierConfig": { "key": "value" } }`
<br />

**Example:**

```js
{
  "prettierConfig": {
    "singleQuote": true,
    "semi": false,
  }
}
```

(Ideally, the plugin would consume your project's prettier settings automatically! But I haven't built this yet. PRs welcome!)

<br />

## Platform Support

This has only been tested in macOS. I think it'd work fine in linux, but I haven't tested it. Windows is a big question mark (would welcome contribution here!).

<br />

## Development

To get started with development:

- Check out this git repo locally, you will need to ensure you have Yarn installed globally.
- In the folder run `yarn install`
- Check that command runs `node ../new-component/src/index.js --help`
- Alternatively you can set up a symlink override by running `npm link` then `new-component --help`. Note: this will override any globally installed version of this package.
