# Electron-with-React-Template

## Git Set up (for Windows)

1. Install [latest Node LTS](https://nodejs.org/en/) on dev computer (if haven't).
2. Download this template or `git clone https://github.com/c-xyz/Electron-with-React-Template`
3. `cd Electron-with-React-Template`
4. `npm install`
5. `npm start` for dev environment and `npm run dist` for production environment.

## Manual Set up the template (for Windows)

### Dev environment

1. Install [latest Node LTS](https://nodejs.org/en/) on dev computer (if haven't).
2. In a cmd window, navigate to destination folder and create a project-folder  
   run `npx create-react-app my-app`
3. Navigate to project-folder by running  
   `cd project-folder`
   1. _(Optional)_ Re-structure `src` folder and update dependency paths, run `npm start` to ensure everything still works.
4. Run `npm add electron electron-builder wait-on concurrently --save-dev`
5. Run `npm add electron-is-dev`
6. Copy `electron.js` to `project-folder/public`  
   _NOTE location is important else may fail building for production_
7. Update `package.json` file:
   1. define entry file: `"main": "public/electron.js"`
   2. change "scripts" to the following:
   ```json
   "scripts": {
    "react-start": "react-scripts start",
      "react-build": "react-scripts build",
      "react-test": "react-scripts test",
      "eject": "react-scripts eject",
      "start": "concurrently \"cross-env BROWSER=none npm run react-start\" \"wait-on http://localhost:3000 && electron .\""
   }
   ```
8. Test dev environment: in cmd (navigated to project-folder),  
   run `npm start`  
   this shall open up the App.  
    _Note, may need to install some dependencies if needed, for example run `npm install cross-env --save-dev` and/or install `concurrently`, `wait-on`._

### Product environement

1. With Dev environment set up, in cmd  
   run `npm install electron-builder --save-dev`
2. Update `package.json` file:
   1. add author & description
   2. add homepage: `"homepage": "./"`
   3. add build section:
   ```json
    "build": {
      "appId": "com.example.electron-cra",
      "files": [ "build/**/*", "node_modules/**/*" ],
      "directories": { "buildResources": "assets" }
      }
   ```
   4. add to scripts:  
      `"dist": "npm run react-build && electron-builder"`  
      _NOTE Must build react first then build electron_
3. Test product environment: in cmd run  
   `npm run dist`  
    should generates a build folder  
    and a dist folder with `setup.exe` to ship to users.
4. Update App: installation will overwrite the old-version app.
5. _(Optional)_ Build app to use on mac: Not Tried. _(Build for macOS is supported only on macOS, please see https://electron.build/multi-platform-build )_

## npm commands

"built-in" commands, like `npm start`.  
custom commands, need "run", e.g. `npm run my-app-start`.

- fix security vulnerabilities in dependencies: `npm audit fix`;
- `npm update` to latest packages
- `npm install [packageName]@latest` update particular package to the latest version. (when previous cmd not updating to the latest!)
