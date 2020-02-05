# vue-webpack-bootstrap

A demo to create one project with vue, webpack and bootstrap without using jQuery.

## Build Setup

``` bash
# clone 
git clone https://github.com/smile-yan/vue-webpack-bootstrap-electron.git
cd vue-webpack-bootstrap-electron

# install dependencies
cnpm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

Make sure that you have installed electron.
```bash
cnpm install electron 
electron --version
```

Then you could test electron
```bash
electron dist
```

Package .exe File
```bash
npm run build
npm run pack:win
```

## How to create 
First of all, make sure that you have installed node.js(version>=8.0).

Then clone this project. (Or you can do as this repository [vue-webpack-bootstrap](https://github.com/smile-yan/vue-webpack-bootstrap))

```bash
# clone vue-webpack-bootstrap
git clone https://github.com/smile-yan/vue-webpack-bootstrap my-electron-project

# install electron and check
cnpm install electron -g
electron --version
```

Then create 'dist' folder and add two important file in dist.
`package.json` 
```json
{
  "name": "electron-quick-start",
  "version": "1.0.0",
  "description": "A minimal Electron application",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  },
  "repository": "https://github.com/electron/electron-quick-start",
  "keywords": [
    "Electron",
    "quick",
    "start",
    "tutorial",
    "demo"
  ],
  "author": "GitHub",
  "license": "CC0-1.0",
  "devDependencies": {
    "electron": "^8.0.0"
  },
  "build": {
    "appId": "cn.smile-yan.my-redis-desktop-manager",
    "productName": "MyRedisDesktopManager",
    "artifactName": "${productName}.${version}.${ext}",
    "copyright": "Copyright © 2019 myredis.cn",
    "asar": true,
    "directories": {
      "output": "build-apps",
      "buildResources": "./"
    },
    "electronVersion": "4.1.0",
    "files": [
      "!static/js/*.map",
      "!static/css/*.map"
    ],
    "win": {
      "icon": "icons/myredis.ico",
      "target": [
        "nsis"
      ]
    },
    "nsis": {
      "allowToChangeInstallationDirectory": true,
      "oneClick": false,
      "menuCategory": true,
      "allowElevation": false
    },
    "linux": {
      "icon": "icons/",
      "category": "Utility",
      "target": [
        "AppImage"
      ]
    },
    "mac": {
      "icon": "icons/myredis.ico",
      "type": "development",
      "category": "public.app-category.developer-tools",
      "target": [
        "dmg"
      ]
    }
  }
}
```

`main.js`
```javascript
// Modules to control application life and create native browser window
const {app, BrowserWindow} = require('electron')
const path = require('path')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow

function createWindow () {
  // Create the browser window.
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    },
    autoHideMenuBar: true,
    icon: `${__dirname}/icons/myredis.ico`,
  })

  // and load the index.html of the app.
  mainWindow.loadFile('index.html')

  // Open the DevTools.
  // mainWindow.webContents.openDevTools()

  // Emitted when the window is closed.
  mainWindow.on('closed', function () {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    mainWindow = null
  })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', function () {
  // On macOS it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== 'darwin') app.quit()
})

app.on('activate', function () {
  // On macOS it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (mainWindow === null) createWindow()
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

Finally, edit file `config/index.js` and find `assetsPublicPath: './'` 
Fix it as `assetsPublicPath: './'`

All job have been done !

> Smileyan
> 2020.2.5
