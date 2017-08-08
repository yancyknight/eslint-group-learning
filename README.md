# eslint-group-learning

## Setup
First, install all local dependencies:

```
$ npm install
```

Install eslint globally:

```
$ npm install -g eslint
```

NOTE: If you don't install eslint globally, you can reference the local installation in all the following commands. Use `./node_modules/.bin/eslint` instead of just `eslint`.

## Run ESLint from command line
In project root, run:

```
$ eslint src/
```

This will lint all the files in the `src` directory. There is an error in file1.js:1, a missing semicolon. Run:

```
$ eslint src/ --fix
```

to automaticaly fix anything that can be fixed automatically, like missing semicolons. We see in the output that the missing semicolon errors went away.

## ESLint in Sublime Text
Follow the installation instructions here 

`https://packagecontrol.io/packages/ESLint`

 to install the ESLint plugin for Sublime Text 2 and 3. This plugin allows you to right click or use `Crtl + Alt + E` to run ESLint in your editor and show output there.

 ## ESLint in Visual Studio Code

 Install the ESLint plugin by Dirk Baeumer in the plugin bar. This plugin:
- Runs ESLint automatically on save
- Shows errors in the bottom left corner of the editor
- Underlines errors and warnings with red or green squiggles
- Gives you a light bulb with the option to auto fix some errors.

## ESLint git hooks

We have installed husky and lint-staged as dependencies. Husky will set up git hooks for us, and lint-staged will lint only files that have been staged in git. Using these two packages together, we can automatically lint any files before we commit and reject the commit if the linting fails.

We have changed some files when we ran `eslint --fix`, so let's try to commit.

```
$ git add src/file1.js
$ git commit -m "It's gonna break"
```

We see the eslint output and the message:

```
husky > pre-commit hook failed (add --no-verify to bypass)
```

If we really need to commit, we can run:

```
$ git commit -m --no-verify "It's gonna break, but go through anyway"
```
This option should be used sparingly, if ever.