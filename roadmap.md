# Unser Weg zum schönen Backend

## Erstellen eines NPM Repositories

Wir erstellen ein basis NPM Modul
``npm init``
und erhalten ein package.json

Wenn wir das packages.json File mit default Werten füllen wollen

``npm init -y``

#### Die package.json
In dieser Datei werden alle Dependencies aufgelistet alle Informationen zu unseren eigenen Modul.

Wichtig ist das diese Datei zum installieren der Dependencies benötigt wird.

``npm install``
installiert alle Module die in den Dependcies stehen

##### Module system
Node.js hat 2 Modul Systeme
CommonJS ( const express = require('express'))
ESM EcmascriptModules ( import express from 'express')

ESM ist das modernere System und gewinnt immer mehr an Bedeutung

Dafür müssen wir eine extra Zeile in unsere package.json schreiben, sonst bekommen wir einen Error.

"type":"module"

## Unsere extra Module

- express (das ist unser Server)
``npm i express``
- axios (damit wir im backend fetchen können)
``npm i axios``
- ejs (damit wir eine template engine haben, brauchen wir eher weniger)
``npm i ejs``
- express-validator(damit wir user eingaben validieren können)
``npm i express-validator``
- cors (um die cors header zu konfigurieren)
 - Wir wollen bestimmen wer einen request zu unseren server senden darf und das machen wir mit unserem cors modul. Dafault (app.use(cors())) erlauben wir request  von überall.
``npm i cors``
- multer library zum upload von dateien (eins von vielen formidable)
``npm i multer``
- dotenv um eigene Umgebungsvariabeln zu erstellen (z.B. PORT, API_KEY, MONGO_DB_URL usw. )
``npm i dotenv``


#### only dev
- nodemon (damit wir unseren Server nicht immer neustarten müssen. Das ist nur eine DevDependency)
``npm i -D nodemon``


##### Nutzen von Nodemon
Um Nodemon nutzen zu können müssen wir ein extra Script in der package.json anlegen:

```
"scripts":{
    "test": //default angelegt 
    "dev": "nodemon index.js", // komma vor und nach der zeile nicht vergessen und dateiname muss passen
}
```

## Einrichten von Express
```javascript
import express from 'express'

const app = express()
const PORT = 9999 // später auch mit env variabeln gelöst

/**
 * 
 *  routen und weiter Dinge .....
 * 
 **/
 
 // starten des Server
 app.listen(PORT, () => console.log('Der Server läuft auf Port:', PORT))
 ```

## Anlegen von Backendrouten mit express

Request Methoden
GET
POST
PUT
DELETE

Mit diesen Methoden können wir alles darstellen was für eine CRUD Anwendung benötigt wird.

C = Create (Wir erstellen einen Datensatz) --> POST
R = Read (Wir lesen einen Datensatz) --> GET
U = Update (Wir bearbeiten einen Datensatz) --> PUT
D = Delete (Wir löschen einen Datensatz) --> DELETE

Wie sieht das mit express aus?

```javascript
// routen mit express
app.get('/', (req,res)=> {
    // wir machen etwas
    res.status(200)
    res.json({message: 'Alles ist cool'})
})
// selbe route andere methode, das ist eine unterschied
app.post('/', (req,res) => {
    res.send('fdgfgdf')
})

app.put('/', (req,res) => {

})
app.delete('/', (req,res) => {

})
```

## Einrichten der Template Engine
``` 
// Wir konfigurieren express, so das ejs als Template engine genutzt werden soll 
app.set('view engine', 'ejs')

// Um jetzt in einen Response mit einer EJS View zu antworten
res.render('meineEJSview', {Möglichedaten})
```

## Nutzen von Axios zum fetchen von Daten

```javascript
axios.get('https://meineapi.de') // liefert ein Promise als return 
.then(response => machetwas()) //verarbeite den fullfiled fall
.catch(err => macheauchetwas()) // verarbeite den rejected fall

// axios bietet eine einfach Möglichkeit die RequestMethod zu ändern

axios.get()
axios.post()
axios.put()
axios.delete()
```

