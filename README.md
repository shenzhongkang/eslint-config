<h1 align="center">@shenzhongkang/eslint-config</h1>
<p align="center">My shared ESLint & Prettier configuration for projects</p>
<hr />

## Features

The config includes these plugins by default:

- [import](https://github.com/benmosher/eslint-plugin-import)
- [jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y)
- [prettier](https://github.com/prettier/eslint-plugin-prettier)
- [react](https://github.com/yannickcr/eslint-plugin-react)
- [react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
- [@typescript-eslint/eslint-plugin](https://github.com/typescript-eslint/typescript-eslint)
- eslint-plugin-node

## Breaking Changes

- Uses `@babel/eslint-parser` instead of `babel-eslint` from `v2.6.1` (See [migration guide](https://git.io/JtPOV))
- Uses Eslint v7 from v2.x.x (See [migration guide](https://git.io/JtPOo))
- Dropped usage `eslint-config-airbnb` in favour of `@shenzhongkang/eslint-config-airbnb`

## Installation

```
# npm
npx install-peerdeps @shenzhongkang/eslint-config --dev

# yarn
npx install-peerdeps @shenzhongkang/eslint-config --dev --yarn
```

This will install the required `peerDependencies` for eslint

Note: Due to [this bug](https://github.com/eslint/eslint/issues/3458), you
need to have all the associated plugins installed as `devDependencies` to make things work.

## Usage

Add extends of the preferred base config to your `.eslintrc.json`:

```json
{
	"extends": ["@shenzhongkang/eslint-config"],
	"rules": {
		// your overrides
	}
}
```

## Other configs

This config also exposes `react`, `node`, and `typescript` configs that I use often.

### TypeScript

To use the ts configuration, install the `TypeScript` compiler:

```
# npm
npm install typescript --save-dev

# yarn
yarn add --dev typescript
```

`.eslintrc.json:`

```json
{
	"extends": ["@shenzhongkang/eslint-config/typescript"],
	"parserOptions": {
		"project": "./tsconfig.json"
	},
	"rules": {
		// your overrides
	}
}
```

### Node.js

It is to be used in combination with the base config (recommended)

`.eslintrc.json:`

```json
{
	"extends": [
		"@abhijithvijayan/eslint-config", // or "@abhijithvijayan/eslint-config/typescript",
		"@abhijithvijayan/eslint-config/node"
	],
	"parserOptions": {
		// Uncomment both if you are using typescript with node
		// "project": "./tsconfig.json",
		// "sourceType": "module" // https://github.com/mysticatea/eslint-plugin-node#-configs
	},
	"rules": {
		// Uncomment if you are using typescript with node(ES Modules)
		// "node/no-unsupported-features/es-syntax": ["error", {
		//   "ignores": ["modules"]
		// }],
		// your other overrides
	}
}
```

### React

It is to be used in combination with the base config (recommended)

`.eslintrc.json:`

```json
{
	"extends": [
		"@shenzhongkang/eslint-config", // or "@shenzhongkang/eslint-config/typescript",
		"@shenzhongkang/eslint-config/react"
	],
	"parserOptions": {
		// Uncomment if you are using typescript configuration
		// "project": "./tsconfig.json"
	},
	"rules": {
		// your overrides
	}
}
```

#### With Create React App

Open your `package.json` and replace `"extends": "react-app"` with above config or remove `extends` entry and create a separate `.eslintrc.json` file(recommended)

### Optional

- To lint your files, you can add the following scripts to your `package.json`:

  ```json
  "scripts": {
      // other scripts
      "lint": "eslint . --ext .js,.ts,.tsx",
      "lint:fix": "eslint . --ext .js,.ts,.tsx --fix"
  },
  ```

- Add a `.eslintignore` file with my defaults

  ```
  node_modules
  dist            # typescript default output directory
  .yarn
  .pnp.js

  # other directories to skip linting
  ```

<hr />

## Override

If you'd like to override `eslint` or `prettier` settings, you can add the rules in your `.eslintrc.json` file.

The ESLint rules go directly under `"rules"` while prettier options go under `"prettier/prettier"`.

Note: overriding `prettier` rules(trailing comma, single quote, etc) require including all existing rules as well.

```json
{
	"extends": ["@shenzhongkang/eslint-config"],
	"rules": {
		"no-console": "off",
		"react/jsx-props-no-spreading": "off",
		"prettier/prettier": [
			"error",
			{
				"bracketSpacing": true,
				"jsxBracketSameLine": false,
				"printWidth": 120,
				"semi": true,
				"singleQuote": true,
				"tabWidth": 4,
				"trailingComma": "all",
				"useTabs": false,
				"proseWrap": "always"
			}
		]
	}
}
```

## With VS Code

To show lint errors in your editor, you'll need to configure your editor.

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Install the [Prettier package](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
3. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:

   ```json
   "editor.formatOnSave": true,
   "[javascript]": {
     "editor.formatOnSave": false
   },
   "[javascriptreact]": {
     "editor.formatOnSave": false
   },
   "[typescript]": {
     "editor.formatOnSave": false
   },
   "[typescriptreact]": {
     "editor.formatOnSave": false
   },
   "editor.codeActionsOnSave": {
       "source.fixAll": true,
       "source.fixAll.eslint": false
   },
   "prettier.disableLanguages": ["javascript", "javascriptreact", "typescript", "typescriptreact"],
   ```

## Bugs

Please file an issue [here](https://github.com/shenzhongkang/eslint-config/issues/new) for bugs, missing documentation, or unexpected behavior.

## Credits

This was initially a fork of [@abhijithvijayan/eslint-config](https://github.com/abhijithvijayan/eslint-config). Thanks abhijithvijayan.

## License

MIT © [Zhongkang Shen](https://shenzhongkang.github.io)
