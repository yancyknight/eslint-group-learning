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
This will lint all the files in the `src` directory. You should see this output:
```
/eslint-group-learning/src/file1.js
  1:17  error  Missing semicolon                           semi
  3:5   error  'hello' is assigned a value but never used  no-unused-vars
  5:5   error  'sup' is assigned a value but never used    no-unused-vars

/eslint-group-learning/src/file2.js
  1:17  error  Missing semicolon                           semi
  3:5   error  'hello' is assigned a value but never used  no-unused-vars
  5:5   error  'sup' is assigned a value but never used    no-unused-vars

✖ 6 problems (6 errors, 0 warnings)
  2 errors, 0 warnings potentially fixable with the `--fix` option.
```

 There are several errors, and a message that 2 errors are potentially fixable. Run:

```
$ eslint src/ --fix
```

to automaticaly fix anything that can be fixed automatically, like missing semicolons. We see in the output that the missing semicolon errors went away:

```
/eslint-group-learning/src/file1.js
  3:5  error  'hello' is assigned a value but never used  no-unused-vars
  5:5  error  'sup' is assigned a value but never used    no-unused-vars

/eslint-group-learning/src/file2.js
  3:5  error  'hello' is assigned a value but never used  no-unused-vars
  5:5  error  'sup' is assigned a value but never used    no-unused-vars

✖ 4 problems (4 errors, 0 warnings)
```

## ESLint with multiple config files

ESLint uses cascading config files. That means it starts in the current directory, and if it finds an ESLint config file, it will load the settings inside. It will then move up one directory and look again. If it finds another config, it will load any settings that wouldn't override settings from the first config. It will continue until it hits the root of the filesystem or a config file with the `"root": true` setting.

Looking at the `nested.js` file, we see that we are using double quotes and a console.log statement, which are both set to raise an error in our root settings folder. If we run

```
eslint nested_folder/
```

we don't see any output. That's because we're overriding the base settings in `nested_foler/.eslintrc.json`.

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