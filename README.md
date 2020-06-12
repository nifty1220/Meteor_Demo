
# Meteor

Diese Demo befasst sich damit wie wir mit Meteor unsere erste Simple und entwas fortgeschrittenere Web Applikation entwickeln können. 

Meteor ist eine Open Cource Plattform zum Erstellen von Web-, App- und Desktopanwendungen welche mit einer Reihe von Technologien, wie Vue.js, React oder MongoDB, daherkommt. Meteor verwaltet automatisch den Datenfluss zwischen Cloud- und Clientanwendungen sowie den Status und das Rendering der Client-Benutzeroberfläche, unabhängig davon, welches UI-Framework man verwenden.

## Vorraussetzungen 
* [npm](https://www.npmjs.com/)
* [Node.js](https://nodejs.org/en/)


## Installation

Windows
```
choco install meteor
```

Mac OS oder Linux
```
curl https://install.meteor.com/ | sh
```

## Erstellung einer HelloWorld Applikation
```
meteor create helloworld
```

```
cd simple-todos
meteor
```
Running on localhost:3000

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

