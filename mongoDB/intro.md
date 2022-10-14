# MongoDB
MongoDB ist eine Datenbank die auf Dokumente basiert.
Leicht zu erstellen, leicht zu benutzen ;D super skalierbar.

Ein Dokument ist ein JavascriptObject
Eine Collection ist ein Array von Dokumenten
Eine Datenbank ist ein Sammlung von Collections

Mit MongoDB können Javascript Objekte einfach in die Datenbank geschrieben werden.
Diese Objekte sind dann die Dokumente in der Datenbank und das Format nennt sich BSON und ist an JSON angelehnt.

## Wie benutzten wir MongoDB in unserer Application

Um uns mit unserer Datenbank zu verbinden brauchen wir als aller erstes den sog. Connectionsstring(z.B. "mongodb+srv://<username>:<password>@cluster0.3ogd1ir.mongodb.net/?retryWrites=true&w=majority" )

Da dieser höchst sensible Daten enthält legen wir in in unsere .env Datei ab.

.env
```
MONGODB_URL="mongodb+srv://<username>:<password>@cluster0.3aod1ir.mongodb.net/?retryWrites=true&w=majority"
```

Nachdem wir das erledigt haben. können wir nun MongoDB in unserer Anwendung nutzen. Das ist hier jetzt nur ein ganz simples Beispiel.

```javascript
import { MongoClient } from 'mongodb

const URL = process.env.MONGODB_URL // holen der Url aus den Umgebungsvariabeln
const client = new MongoClient(URL) // initialisieren eines neuen Clientes

/**
 * So wie unser Browser der Client ist der mit dem Server kommuniziert, so ist der MongoClient 
 * der Client der mit unserer Datenbank kommuniziert. Das Client-Server Prinzip findet
 * man sehr häufig in der Webentwicklung
 * */

client.connect()  // kann man natürlich auch mit async und await nutzen
.then(client => client.db('datenbankname')) // wir haben als parameter den verbundenen client erhalten
.then(db => {
    // jetzt haben wir Zugriff auf unsere datenbank mit den db Object
    // Ab hier können wir dann querys auf unsere Datenbank ausführen

    db.collection('collection').find()
    .then(res => {
        // res ist jetzt der zeiger auf die Datenbank
    })
})
.catch(err => {
    // hier könnt ihr dann error handling ein bauen
})

```

## Ein ausgelagerte DB instanz (singleton pattern)
```javascript
import { MongoClient } from 'mongodb'

const URL = process.env.MONGODB_URL
const client = new MongoClient(URL)

let db

export const getDB = () => {
    return new Promise((resolve, reject) => {
        if(db) resolve(db)
        client.connect()
        .then(client => client.db('carshop'))
        .then(clientDb => {
            db = clientDb
            resolve(db)
        })
        .catch(err => reject(err))
        
    })
}
```
