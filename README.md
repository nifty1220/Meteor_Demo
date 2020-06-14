
# Meteor

Diese Demo befasst sich damit wie wir mit Meteor unsere erste Simple und entwas fortgeschrittenere Web Applikation entwickeln können. 

Meteor ist eine Open Cource Plattform zum Erstellen von Web-, App- und Desktopanwendungen welche mit einer Reihe von Technologien, wie Vue.js, React oder MongoDB, daherkommt. Meteor verwaltet automatisch den Datenfluss zwischen Cloud- und Clientanwendungen sowie den Status und das Rendering der Client-Benutzeroberfläche, unabhängig davon, welches UI-Framework man verwenden.

## Vorraussetzungen 
* [chocolatey (Windows)](https://chocolatey.org/)



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
Wir erstellen eine einfache "Hello World" Applikation mit welcher wir ein erstes Verständnis für die Projekt Struktur von Meteor gibt

```
meteor create helloworld
```

Durch diesen Befehl wird ein Projekt erstellt welches die folgenden Datein beinhaltet:

* client/main.js        # a JavaScript entry point loaded on the client
* client/main.html      # an HTML file that defines view templates
* client/main.css       # a CSS file to define your app's styles
* server/main.js        # a JavaScript entry point loaded on the server
* test/main.js          # a JavaScript entry point when running tests
* package.json          # a control file for installing npm packages
* package-lock.json     # describes the npm dependency tree
* node_modules/         # packages installed by npm
* .meteor/              # internal Meteor files
* .gitignore            # a control file for git

```
cd helloworld
meteor
# Meteor running on: http://localhost:3000/
```
Danach wechseln wir in unseren eben erstellten Ordner und starten unser Projekt welches dann unter localhost:3000 zu erreichen ist.  

Et voilà, wir haben unsere erste Hello World Applikation erstellt.

## Erstellung einer Todo List App

Als erstes erstellen wir wieder ein neues Projekt welches wir gleich starten, da Meteor unseren Code permanent aktualisiert ist es auch nicht notwendig die Applikation neu zu starten. 

```
meteor create to-do
cd simple-todos
meteor
```

Jetzt bereiten wir unsere Projekt vor, damit wir alle notwendigen Datein für unsere Applikation zur Verfügungn haben. Wir erstellen einen neuen Ordner "imports" in unserem Projekt welcher den Ordner "ui" mit den Datein 
"body.html"
"body.js"
"task.html"
"task.js"
und einen api Ordner mit der Datei
"tasks.js"


