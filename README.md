
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
"body.html",
"body.js",
"task.html",
"task.js"
und einen api Ordner mit der Datei
"tasks.js"

So, nun können wir loslegen.

Beginnen wir damit den nicht benötigten code aus unserer main.html Datei zu entfernen

```
<head>
  <title>  Todo App </title>
 </head>
```

Jetzt legen wir unsere erste Todo Liste an und fügen hierführ einige HTML Elemente in unsere body.html hinzu und greifen dann mittels Templates mit unsere body.js darauf zu. 

import/ui/body.html
```
<head>
<body>
    <div class="container">
      <header>
        <h1>Todo List</h1>
      </header>
  
      <ul>
        {{#each tasks}}
          {{> task}}
        {{/each}}
      </ul>
    </div>
  </body>
  
  <template name="task">
    <li>{{text}}</li>
  </template>
```

import/ui/body.js
```
import { Template } from 'meteor/templating';
 
import './body.html';
 
Template.body.helpers({
  tasks: [
    { text: 'This is task 1' },
    { text: 'This is task 2' },
    { text: 'This is task 3' },
  ],
});
```
# Templates
Der Inhalt von Template Tags wir in Meteor templates kompiliert, welche wir einfach mit {{> templateName }} in unser HTML einbauen können. Der Vorteil hierbei ist, dass wir so ganz einfach mit Template.body von unserer JavaScript Datei einfach auf diesen Bereich zugreifen können. 

# Logik
Mit Hilfe der doppelt geschweiften Klammern können wir Logik und Daten in unser HTML einbauen. Mit Hilfe eines Helpers können wir dann die Daten von unserem JavaScript aus an unser Template weitgergeben. Wir haben also einen Template.body helper welcher uns ein Array mit den Daten liefert. Mit {{ #each tasks }} iterieren wir über das Array und fügen für jeden Wert ein "task" template ein. Innerhalb des #each Blocks können wir dann den Text mit Hilfe des Templates mit {{ text }} anzeigen lassen. 

In unserem JavaScript entry point file (client/main.js) können wir ebenfalls den vorhandenen Code entfernen und importieren unsere body.js 
```
import '../imports/ui/body.js';
```

