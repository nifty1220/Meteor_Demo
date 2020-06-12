
# Electron

Dieses Techdemo gibt eine kurzen Einblick in die Funktionalitäten von Electron. 

Electron ist ein Framework, mit welchem es möglich ist, cross-plattform Desktop Applikationen mithilfe von Javascript, HTML & CSS zu entwickeln. Electron basiert auf Chromium und Node.js. Im Gegensatz zu einem Browser kann daher auf Node.js zurückgegriffen werden. Es können auch andere Frameworks wie React, Vue oder Angular zusammen mit Electron verwendet werden.

## Vorraussetzungen 
* [npm](https://www.npmjs.com/)
* [Node.js](https://nodejs.org/en/)


## Installation
```
npm install electron --save-dev
```
Durch diesen Befehl wird Electron als Abhängigkeit in die App eingebunden.

Als Editor wird [Visual Studio Code](https://code.visualstudio.com/) oder [Atom](https://atom.io/) empfohlen, welche übrigends beide mit dem Electron Framework erstellt worden sind. 

## Erste App mit Electron
1. Erstellen eines Projektordners,navigieren in den entsprechenden Projektordner und `npm init` im Terminal ausführen. Daraufhin wird ein package.json File erstellt. 
Dies sollte dann wiefolgt aussehen:
```
{
  "name": "your-app",
  "version": "0.1.0",
  "main": "main.js",
  "scripts": {
    "start": "electron ."
  }
}
```
2. Electron mit `npm install electron --save-dev` zur App hinzufügen
3. Projektstruktur:
```
your-app/
├── package.json
├── main.js
└── index.html
```
Im main.js wird folgender Code benötigt:
```javascript
const { app, BrowserWindow } = require('electron');

function createWindow () {
  // creates the browserwindow
  let win = new BrowserWindow({
    width: 1000,
    height: 800,
    webPreferences: {
      nodeIntegration: true
    }
  })

  // loads the index.html
  win.loadFile('index.html');

  // optional open devtools automatic at startup
  //win.webContents.openDevTools();
}

// method is called when electron is ready to create the browserwindow
app.whenReady().then(createWindow);

// it is common for macOS that an app stays open in the background when closing it
// mac apps are normally closed with Cmd+Q
app.on('window-all-closed', () => {
    if (process.platform !== 'darwin'){
        app.quit();
    }
});

//it is also common on macOS to open a window when clicking on the icon in the dock and no other windows are open
app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0){
        createWindow();
    }
});
```
Im main.js File können alle Features, welche das Electron-Modul bereitstellt, aufgerufen werden.
Die index.html kann nach Belieben bearbeitet werden.

## Fortgeschrittene App mit Electron
In unserer App werden die Features von Electron mithilfe einer Screen-Recording App veranschaulicht. Das Projekt wird mit Electron-Forge erstellt.
Electron-Forge erstellt ein Boilerplate und hat auch die benötigten Funktionen zum Bundlen der App.
```
npx create-electron-app screen-recorder
```
Im main.js wird nur `nodeIntegration: true` hinzugefügt. Dies gibt uns die Möglichkeit mit node.js im Frontend zu arbeiten.

Die Screen-Recorder App beinhaltet noch ein Simples HTML-File mit einem Video-Element und Buttons zum Starten, Stoppen und Auswählen der Videosource.

Der eigentliche Renderprozess findet in der render.js statt. Hier wird auf Electron und Node-Module zurückgegriffen, um die verschiedenen Features zu zeigen. Mit Electron wurde im Renderprozess z.B. auf das desktopCapturer Modul zugegriffen, welches die Bildschirmaufnahme ermöglicht. Es wurde auch im Frontend mit dem writeFile Modul auf node.js zurückgegriffen.

## App Bundlen
Das Bundlen der App ist dank Electron-Forge ziemlich einfach. 
```
npm run make
```
Dies erstellt uns einen out-Folder, welcher eine Executable unserer App beinhaltet.

