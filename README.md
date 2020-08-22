<div align="center">
<img alt="Electron Elm Crossover Banner" src="https://raw.githubusercontent.com/soulehshaikh99/assets/master/create-electron-framework-app/readme/svg/Electron_Elm.svg" width="550" />
</div>
<br />
The boilerplate code to get started creating Cross-platform Desktop Apps with Electron and Elm JS as front-end technology.
<br />
<br />
<div align="center">

[![forthebadge](http://forthebadge.com/images/badges/built-by-developers.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/makes-people-smile.svg)](http://forthebadge.com)<br />

[![forthebadge](http://forthebadge.com/images/badges/uses-html.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/uses-css.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/uses-js.svg)](http://forthebadge.com)

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

</div>

## ✒️ Overview

The aim of this project is to provide Web Developers using `elm` the power to create cross-platform desktop apps using `electron`.

#### 🧐 What packages does the project use?

**`electron`** enables you to create desktop applications with pure JavaScript by providing a runtime with rich native (operating system) APIs. You could see it as a variant of the Node.js runtime that is focused on desktop applications instead of web servers.

**`electron-builder`** is used as a complete solution to package and build a ready for distribution (supports Numerous target formats) Electron app with "auto update" support out of the box.

**`electron-serve`** is used for Static file serving for Electron apps.

**`elm`** is a delightful language with features like No Runtime Exceptions, Great Performance, Enforced Semantic Versioning, Small Assets and Javascript Interoperability.

**`concurrently`** is used to run multiple commands concurrently.

**`wait-on`** is used as it can wait for sockets, and http(s) resources to become available.
<br />

## 🚀 Getting Started

**Note:** If you wish to use npm over yarn then modify package.json by replacing `yarn` with `npm` in `electron-dev` and `preelectron-pack` scripts.
But I strongly recommend using <em>yarn</em> as it is a better choice when compared to <em>npm</em>.

### 🤓 Use this boilerplate

```bash
# Clone the Project

# Install create-elm-app as global dependency.
$ yarn global add create-elm-app
# npm -g i create-elm-app

# Use degit scaffolding tool
$ npx degit soulehshaikh99/create-elm-electron-app create-elm-electron-app
# or GitHub CLI Users
$ gh repo clone https://github.com/soulehshaikh99/create-elm-electron-app.git
# or Normal Git Users
$ git clone https://github.com/soulehshaikh99/create-elm-electron-app.git

# Switch location to the cloned directory
$ cd create-elm-electron-app

# Install dependencies
$ yarn # or npm install

# Run your app
$ yarn electron-dev # or npm run electron-dev

# Package Your App
$ yarn electron-pack # or npm run electron-pack
```

### 💫 Create this boilerplate from scratch (Manual Setup)

#### 1) Create an Elm project using scaffolding tool create-elm-app.

```bash
$ yarn create elm-app create-elm-electron-app
# npx create-elm-app create-elm-electron-app
```

#### 2) Change Directory

```bash
$ cd create-elm-electron-app
```

#### 3) Initialize project with your favorite package manager

```bash
# set entry point to main.js
$ yarn init # or npm init
```

#### 4) Install Development Dependencies

```bash
$ yarn add --dev electron electron-builder wait-on concurrently
# npm i -D electron electron-builder wait-on concurrently
```

#### 5) Install Production Dependency

```bash
$ yarn add electron-serve # or npm i electron-serve
```

#### 6) Your dependencies should look something like this

```json
"dependencies": {
  "electron-serve": "^1.0.0"
},
"devDependencies": {
  "concurrently": "^5.3.0",
  "electron": "^9.2.1",
  "electron-builder": "^22.8.0",
  "wait-on": "^5.2.0"
}
```

#### 7) Download the app icon

[favicon.png](https://raw.githubusercontent.com/soulehshaikh99/assets/master/framework-icons/elm/favicon.png) and place it in the public directory.

#### 8) Create .env file

```bash
# Windows Users
$ fsutil file createnew .env 0
# notepad .env

# Linux and macOS Users
$ touch .env
```

#### 9) Paste this in .env file

```bash
# As `create-elm-app` is based on `create-react-app` we can configure things.
# This suppresses auto-opening `localhost:3000` on the browser
BROWSER=none
```

#### 10) Create main.js file (serves as entry point for Electron App's Main Process)

```bash
# Windows Users
$ fsutil file createnew main.js 0
# notepad main.js 

# Linux and macOS Users
$ touch main.js
```

#### 11) Paste the below code in main.js file

```js
// Modules to control application life and create native browser window
const { app, BrowserWindow } = require("electron");
const path = require("path");
const serve = require("electron-serve");
const loadURL = serve({ directory: "build" });

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow;

function isDev() {
  return !app.isPackaged;
}

function createWindow() {
  // Create the browser window.
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
    // Use this in development mode.
    icon: isDev()
      ? path.join(process.cwd(), "public/favicon.png")
      : path.join(__dirname, "build/favicon.png"),
    // Use this in production mode.
    // icon: path.join(__dirname, 'build/favicon.png'),
    show: false,
  });

  // This block of code is intended for development purpose only.
  // Delete this entire block of code when you are ready to package the application.
  if (isDev()) {
    mainWindow.loadURL("http://localhost:3000/");
  } else {
    //Do not delete this statement, Use this piece of code when packaging app for production environment
    loadURL(mainWindow);
  }

  // Uncomment the following line of code when app is ready to be packaged.
  // loadURL(mainWindow);

  // Open the DevTools and also disable Electron Security Warning.
  // process.env['ELECTRON_DISABLE_SECURITY_WARNINGS'] = true;
  // mainWindow.webContents.openDevTools();

  // Emitted when the window is closed.
  mainWindow.on("closed", function () {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    mainWindow = null;
  });

  // Emitted when the window is ready to be shown
  // This helps in showing the window gracefully.
  mainWindow.once("ready-to-show", () => {
    mainWindow.show();
  });
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on("ready", createWindow);

// Quit when all windows are closed.
app.on("window-all-closed", function () {
  // On macOS it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== "darwin") app.quit();
});

app.on("activate", function () {
  // On macOS it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (mainWindow === null) createWindow();
});

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

#### 12) Add scripts

```bash
"scripts": {
  "start": "elm-app start",
  "build": "elm-app build",
  "test": "elm-app test",
  "eject": "elm-app eject",
  "electron": "wait-on http://localhost:3000 && electron .",
  "electron-dev": "concurrently \"yarn start\" \"yarn electron\"",
  "preelectron-pack": "yarn build",
  "electron-pack": "electron-builder"
}
```

#### 11) Add the following configuration in `package.json`

**Note:** build configuration is used by electron-builder, modify it if you wish to add more packaging and native distribution options for different OS Platforms.

```bash
"main": "main.js", # please verify entry point is set to main.js 
"build": {
  "icon": "public/favicon.png",
  "productName": "Elm and Electron App",
  "files": [
    "build/**/*",
    "main.js"
  ],
  "win": {},  # Windows Specific Configuration
  "linux": {},  # Linux Specific Configuration
  "mac": {}  # MacOs Specific Configuration
},
```

#### 12) Test drive your app

```bash
# Run your app
$ yarn electron-dev # or npm run electron-dev

# Package Your App
$ yarn electron-pack # or npm run electron-pack
```

### 💯 Result

<div align="center">
<img alt="Electron Elm Window Screeenshot" src="https://raw.githubusercontent.com/soulehshaikh99/assets/master/create-electron-framework-app/readme/png/create-elm-electron-app.png" />
</div>

<h3>😍 Made with ❤️ from Souleh</h3>

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)
<br/>

<h3>📋 License: </h3>
Licensed under the <a href="https://github.com/soulehshaikh99/create-elm-electron-app/blob/master/LICENSE">MIT License</a>.
