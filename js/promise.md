# Promise oder das Versprechen dass ich dir etwas zurückgebe
Ein Promise wird in der asynchronen Programmierung genutzt. Wenn wir das Ergebnis einer asynchronen Operation nutzen wollen, müssen wir wissen wann diese Operation beendet ist.

### Callback hell
Um etwas nach einer asynchronen Operation auszuführen wurde dann eine sogenannte Callback Funktion ausgeführt.
Da dann in der Callback Funktion auch wieder ansychrone Operationen gestartet werden können, die dann auch auch wieder callback Funktionen aufrufen. Kann das alles schon sehr unübersichtlich werden.

Es wird dann eine Callback HELL
Callback in callback in callback genested. Auweia.

## Promise to the rescue

Durch die Verwendung von Promises wird der asynchronen Prozeß sehr viel schöner verpackt und ist 
einfacher zu verwenden und zu verstehen.

## Das Promise
Ein Promise ist ein Javascript Object welches 3 verschiedene [Status](https://de.wiktionary.org/wiki/Status)
annehmen kann.

- Pending       | Der Prozess läuft noch
- Fullfilled    | Der Prozess ist erfolgreich beendet
- Rejected      | Der Prozess wurde mit einem Fehler beendet

## Wir bauen ein Promise
```javascript
const myPromise = new Promise((resolve, reject) => {
    
    // führe irgendwelche asynchronen Operationen aus
    // haben sie geklappt?
    resolve(data) 
    // haben sie nicht geklappt?
    reject(err)
})

myPromise.then(data => `mache etwas mit data`).catch(err => `mache etwas mit err`).finally(() => wird immer ausgeführt)

// Die Funktion .then() wird ausgeführt wenn das promise mit resolve beendet wird. Der Status ist dann Fullfilled
// .then() liefert selber auch wieder ein Promise Object zurück
// .catch() wird ausgeführt wenn in einem Promise die reject Methode aufgerufen wird
// also ist da der Ort für die Fehlerbehandlung
// .finally() wird egal was mit dem Promise passiert immer ganz zum Schluß ausgeführt und kann aber auch ganz weggelassen werden 
```

## Promisechaining
Dadurch das ```.then()``` immer auch ein Promise zurückgibt, kann man diese .thens chainen.
```javascript
myPromise
    .then(data => machwasmit(data))
    .then(returnWertVomThenÜberMir => machwas())
    .catch(err => clg(err))

```
Hier wird das nachfolgende .then immer mit dem result des vorherigen aufgerufen. Deswegen, nicht vergessen ergebnisse zu returnen ;)