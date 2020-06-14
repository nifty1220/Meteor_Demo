
# Meteor

Diese Demo befasst sich damit wie wir mit Meteor unsere erste simple und etwas fortgeschrittenere Web Applikation bzw. App entwickeln können. 

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
Wir erstellen eine einfache "Hello World" Applikation welche uns ein erstes Verständnis für die Projektstruktur von Meteor gibt.

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


Danach wechseln wir in unseren eben erstellten Ordner und starten unser Projekt welches dann unter localhost:3000 zu erreichen ist.  

```
cd helloworld
meteor
# Meteor running on: http://localhost:3000/
```

Et voilà, wir haben unsere erste Hello World Applikation erstellt.

## Erstellung einer Todo List App

Als Erstes erstellen wir wieder ein neues Projekt welches wir gleich starten, da Meteor unseren Code permanent aktualisiert ist es auch nicht notwendig bei Änderungen die Applikation neu zu starten. 

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
und einen Ordner "api" mit der Datei
"tasks.js"

So, nun können wir loslegen.

Beginnen wir damit den nicht benötigten Code aus unserer main.html Datei zu entfernen

```
<head>
  <title>  Todo App </title>
 </head>
```

Jetzt legen wir unsere erste Todo Liste an und fügen hierfür einige HTML Elemente in unsere body.html hinzu und greifen dann mittels Templates mit unsere body.js darauf zu. 

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
    { text: 'Bachelorarbeit schreiben' },
  ],
});
```

# Templates
Der Inhalt von Template Tags wird in Meteor Templates kompiliert, welche wir einfach mit {{ > templateName }} in unser HTML einbauen können. Der Vorteil hierbei ist, dass wir so ganz einfach mit Template.body von unserer JavaScript Datei einfach auf diesen Bereich zugreifen können. 

# Logik
Mit Hilfe der doppelt geschweiften Klammern können wir Logik und Daten in unser HTML einbauen. Mit "helpers" können wir dann die Daten von unserem JavaScript aus an unser Template übergeben. Wir haben also einen Template.body helper welcher uns ein Array mit den Daten liefert. Mit {{ #each tasks }} iterieren wir über das Array und fügen für jeden Wert ein "task" template ein. Innerhalb des #each Blocks können wir dann den Text mit Hilfe des Templates mit {{ text }} anzeigen lassen. 

In unserem JavaScript entry point file (client/main.js) können wir ebenfalls den vorhandenen Code entfernen und importieren unsere body.js 

```
import '../imports/ui/body.js';
```

# CSS
Für alle, die es optisch etwas ansprechender mögen empfehle ich diesen Code in client/main.css einzufügen

```
body {
  font-family: sans-serif;
  background-color: #315481;
  background-image: linear-gradient(to bottom, #315481, #918e82 100%);
  background-attachment: fixed;
 
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
 
  padding: 0;
  margin: 0;
 
  font-size: 14px;
}
 
.container {
  max-width: 600px;
  margin: 0 auto;
  min-height: 100%;
  background: white;
}
 
header {
  background: #d2edf4;
  background-image: linear-gradient(to bottom, #d0edf5, #e1e5f0 100%);
  padding: 20px 15px 15px 15px;
  position: relative;
}
 
#login-buttons {
  display: block;
}
 
h1 {
  font-size: 1.5em;
  margin: 0;
  margin-bottom: 10px;
  display: inline-block;
  margin-right: 1em;
}
 
form {
  margin-top: 10px;
  margin-bottom: -10px;
  position: relative;
}
 
.new-task input {
  box-sizing: border-box;
  padding: 10px 0;
  background: transparent;
  border: none;
  width: 100%;
  padding-right: 80px;
  font-size: 1em;
}
 
.new-task input:focus{
  outline: 0;
}
 
ul {
  margin: 0;
  padding: 0;
  background: white;
}
 
.delete {
  float: right;
  font-weight: bold;
  background: none;
  font-size: 1em;
  border: none;
  position: relative;
}
 
li {
  position: relative;
  list-style: none;
  padding: 15px;
  border-bottom: #eee solid 1px;
}
 
li .text {
  margin-left: 10px;
}
 
li.checked {
  color: #888;
}
 
li.checked .text {
  text-decoration: line-through;
}
 
li.private {
  background: #eee;
  border-color: #ddd;
}
 
header .hide-completed {
  float: right;
}
 
.toggle-private {
  margin-left: 5px;
}
 
@media (max-width: 600px) {
  li {
    padding: 12px 15px;
  }
 
  .search {
    width: 150px;
    clear: both;
  }
 
  .new-task input {
    padding-bottom: 5px;
  }
}
```

# Collections und MongoDB

Jetzt möchte ich, dass wir unsere Daten auch persistent speichern können und hierfür verwendenen wir Collections mit MongoDB. Das Tolle ist, dass MongoDB in Meteor integriert ist und wir es ganz einfach importieren können. Alles was wir hier machen ist eine Collection zu erstellen und zu exportieren. 

imports/api/tasks.js
```
import { Mongo } from 'meteor/mongo';
 
export const Tasks = new Mongo.Collection('tasks');
```

Damit unsere Collection gleich am Start initialisiert wird importieren wir das Skript in unsere server/main.js
Das hat den Vorteil das der Server gleich das gesamte Setup der Collection übernimmt und dann die Daten an den Client schickt.

```
import '../imports/api/tasks.js';
```

Damit unsere Applikation nun auch die Daten aus der Collection und nicht mehr aus dem Array holt müssen wir in unserer body.js die Collection importieren und uns dann mit .find({}) die Daten holen.

```
import { Template } from 'meteor/templating';
 
import { Tasks } from '../api/tasks.js';
 
import './body.html';
 
Template.body.helpers({
    tasks() {
        return Tasks.find({});
      },
});
```

Wenn wir uns jetzt unsere Applikation ansehen, dann sehen wir das unsere Todo Liste leer ist, weil auch unsere Collection noch leer ist. Aber das werden wir gleich ändern.

# Events

Natürlich können wir auch auf Events reagieren. Dafür fügen wir zunächst ein Form Element in unsere body.html ein und werden dann in unserer body.js dieses Submit Event handlen. 

```
    <div class="container">
      <header>
        <h1>Todo List</h1>
 
        <form class="new-task">
            <input type="text" name="text" placeholder="Type to add new tasks" />
          </form>
 
      </header>
```

Mit Template.body.events können wir jetzt mit dem Event arbeiten und alles was wir machen ist bei dem Submit Event von "new-task" uns den Wert des Input Elements zu holen, der Collection "Tasks" hinzuzufügen und zum schluss das Input Feld zu resetten.

```
    tasks() {
        return Tasks.find({});
      },
});
 
Template.body.events({
    'submit .new-task'(event) {

      event.preventDefault();
 
      const target = event.target;
      const text = target.text.value;
  
      Tasks.insert({
        text,
        createdAt: new Date(), // current time
      });
  
      target.text.value = '';
    },
  });
```

# Checkbox und Delete

Im letzten Schritt werden wir jetzt noch die Funktion hinzufügen, welche es uns ermöglicht Tasks auch zu löschen oder abzuhacken. Dazu lagern wir unser task Template aus der body.html in ein eigenes File aus. 

task.html
```
<template name="task">
    <li class="{{#if checked}}checked{{/if}}">
      <button class="delete">&times;</button>
  
      <input type="checkbox" checked="{{checked}}" class="toggle-checked" />
  
      <span class="text">{{text}}</span>
    </li>
  </template>
```
Mit "class="{{#if checked}}checked{{/if}}" können wir dem Elemenet die Klasse "checked" zuweisen falls checked true ist, um so beispielsweise den Text mit CSS durchzustreichen.

Wir haben also wieder ein template mit einer Checkbox und einem Delete Button. 

Alles was jetzt noch zu tun ist, ist wieder auf die Events zu reagieren.

task.js
```
import { Template } from 'meteor/templating';
 
import { Tasks } from '../api/tasks.js';
 
import './task.html';
 
Template.task.events({
  'click .toggle-checked'() {
    Tasks.update(this._id, {
      $set: { checked: ! this.checked },
    });
  },
  'click .delete'() {
    Tasks.remove(this._id);
  },
});
```
Jedes Objekt einer Collection hat eine unique ID und mit "this._id" können wir den jeweiligen Task updated oder entfernen. Die Update Funktion verwendet 2 Argumente, zuerst die ID welches Elemenet bearbeitet werde soll und danach was die Veränderung sein soll. In unserem Fall nutzen wir $set um das checked Feld einzuschalten. 

Ausserdem benötigen wir in unsere body.js auch noch die eben erstellte task.js da sie darin verwendet wird.

```
import { Tasks } from '../api/tasks.js';
 
import './task.js';
import './body.html';
 
Template.body.helpers({
```

Damit wäre die Applikation fertig.

# Running on mobile
 
Für denn Fall das man seine Applikation auch am Smartphone laufen lassen will kann man das ganz einfach mit diesem Emulator machen.

iOS (Benötigt Mac)

```
meteor install-sdk ios

meteor add-platform ios
meteor run ios
```

Android

```
meteor install-sdk android

meteor add-platform android
meteor run android
```
