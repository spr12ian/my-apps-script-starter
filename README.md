# Google Apps Script (GAS) Development as at 2020-05-01

This [GitHub repository](https://github.com/spr12ian/my-apps-script-starter/) puts together some info and examples on developing [GAS](https://developers.google.com/apps-script) projects locally, in a Bash shell, using the [VS Code](https://code.visualstudio.com/) editor.

My objective is to develop GAS overcoming two key limitations:

1. The default Script Editor provided by Google lacks many features found in modern editors.
2. Google's V8 GAS engine does not support [Javascript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules), and managing load order which is file order dependent is a real pain

[Clasp](https://developers.google.com/apps-script/guides/clasp) is a tool that lets you develop your GAS projects locally. Clasp is written in [Node.js](https://developer.mozilla.org/en-US/docs/Glossary/Node.js) and distributed via the [npm](https://www.npmjs.com/) tool.

Javascript modules are supported in Node.js

The initial version of this repository is based on the [Apps Script Starter](https://awesomeopensource.com/project/labnol/apps-script-starter) provided by [Amit Agarwal](https://www.labnol.org/about), including the useful **[step-by-step YouTube video tutorial](https://www.youtube.com/watch?v=KxdCIbeO4Uk)**.

## Build with Google Apps Script

You also need to install Node.js which includes the npm package manager.

### Getting Started

**1.** Clone the repository and install npm dependencies and [utilities](TOOLS.md).

```
git clone https://github.com/labnol/apps-script-starter my-project
cd my-project
npm install
```

**2.** Log in to Google clasp and authorize using your Google account.

``` sh
npx clasp login
```

**3.** Create a new Google Script bound to a Google Sheet (or set the type as standalone to create a standalone script in your Google Drive)

```
npx clasp create --type sheets --title "My Apps Script Project" --rootDir ./dist
```

**4.** Include the necessary [OAuth Scopes](./scopes.md) in the [appsscript.json](./appsscript.json) file

1. Deploy the project (development)

```
npm run deploy
```

The `dist` directory contains the bundled code that is pushed to Google Apps Script.

**6.** Deploy the project (production mode)

```
npm run deploy:prod
```

#### Enable JavaScript v8 Runtime

Inside the Google Apps Script editor, select View > Show project manifest to open the `appsscript.json` manifest file in the editor. Add a new `runtimeVersion` field and set the value to `V8`. Save your script.

#### Development vs Production mode

In production mode, the function names and variable names are shrinked and the output code is auto-minified. The production flag is not recommended for testing and debugging the Apps Script code.

### The .claspignore file

The `.claspignore` file allows you to specify file and directories that you do not wish to not upload to your Google Apps Script project via `clasp push`.

The default `.claspignore` file in the Apps Script Starter kit will push all the JS and HTML inside the `rootDir` folder and ignore all the other files.

## Using Git with Google Apps Script

Create a new repository in Github and make a note of the URL of the new repository. Next, open the terminal and run the above commands to push your Apps Script project to Github.

``` sh
# Remove all Git tracking from the project
rm -rf .git
# Initialise the local directory as a Git repository
git init
# Add files to the local repository staging area
git add .
# Commit staged files to the local repository
git commit -m "Initial commit"
# Configure remote repository
git remote add origin https://
# Push changes to remote
git push -u origin master
```
