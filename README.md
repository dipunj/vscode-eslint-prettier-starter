# vscode-eslint-prettier-starter

Setting up eslint and prettier with vscode is quite time consuming, and extremely repetitive process. After doing this over and over again for more than 7 projects. I gave up, and decided to create this repository, which can be used as a starter for you JS/TS projects.

## Step by Step process

1. Clone this repository
2. Install eslint (dbaeumer.vscode-eslint) extension on vscode – the only extension you need to auto format your JS/TS code.
3. Ensure to enable the eslint extension (globally / workspace ? - your choice).
4. Put your code only in subdirectories (eg. frontend, backend etc.)
5. An example .eslintrc.json configuration is already present in the project by the name of `.eslintrc.json.example`, use that as a reference and create your own by:
    3.1. running npx eslint --init
    3.2. Delete the example eslintrc once you have a working `.eslintrc.json`


## .vscode/settings.json

The configuration lines which matter for our purpose:

```jsonc
// asks prettier to format the file 
// will not do imports but will fix whitespace, and semicolon use.
"editor.formatOnSave": true,

// issues "eslint --fix" command when a file is saved
// will autoimport missing imports, but will not fix semicolons
"editor.codeActionsOnSave": {
	"source.fixAll.eslint": true
},
// shows eslint icon on the status bar (bottom right)
"eslint.alwaysShowStatus": true,
```


## .eslintrc.json

This file is super important. It is strongly advised to use the command `npx eslint --init`. This will create an eslintrc file for you and install the dependencies required as well.

### root: true

- eslint uses an upwards directory search to find a config to use to format the file. By setting root: true, we tell eslint that this is the last place to look for a config.
- You can create an eslint config file for each subdirectory (eg backend, frontend) by issuing npx eslint --init command in the subdirectory, this way you can generate different code style configs for different subdirectories.
- Don't set root: true in the eslint config present in the subdirectories. This will allow eslint to use the eslint config of the parent directory, as a fallback for rules not defined in eslint configs of child directories.

### rules

- You can set a lot of rules for eslint, but to ensure that prettier and eslint don't conflict with each other, we use prettier as a plugin for eslint.

Steps: 
    1. install `eslint-plugin-prettier` and `eslint-config-prettier` as devDependencies for the root package.json
    2. ensure that the eslint config looks like:

```json
// ... other properties
"extends": [
    ...,
    "prettier"       // ensure that prettier is the last plugin in this array
],
// ... other properties
"plugins": ["prettier"],
// ... other properties
"rules": {
    // ... other rules
    "prettier/prettier": [
		"error"
    ],
    // ... other rules
}
 ```

### dependencies

- when using typescript, ensure that "@typescript-eslint/parser" and "@typescript-eslint/plugin" are installed as dev dependencies in the topmost package.json, and the value of "parser" field is set to "@typescript-eslint/parser" in the eslint config file.
- Ensure that `eslint-config-prettier` and `` are installed as dev dependencies, for prettier to work.



