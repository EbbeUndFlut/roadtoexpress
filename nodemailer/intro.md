# Nodemailer
Durch Nodemailer sind wir in der Lage, Emails zu erstellen und zu versenden. 
Was wir dazu benötigen ist der Zugang zu einem Mailserver /-dienst.

Dieser stellt uns eine URL (smtp.meinmailserver.de) und authentifizierungs Daten zur Verfügung.

## Installation
``npm install nodemailer`` 

## Grundlegende Benutzung
```javascript
import nodemailer from 'nodemailer'

const transport = nodemailer.createTransport({
    host: 'smtp.meinmailserver.de',
    port:2525,
    auth:{
        user: 'meinuser',
        pass: 'meinpass'
    }
})

// eine einfache Email erstellen, denkt daran das alles Werte natürlich auch mit variabeln gefüllt werden können

const message = {
    from: "sender@meinmailserver.de",
    to: "reciever@andererserver.de",
    subject: "Email Titel",
    text: "Plain Text, der angezeigt wird, wenn HTML unterdrückt wird",
    html: "<p>Alles in HTML, dann sieht es auch super aus</p>
}

// absenden der email

transporter.sendMail(message, (err, info) => {
    // mache etwas wenn die Mail gesendet wurde
})

```

## Wie funktioniert das?
Die Emails die wir jetzt versenden, werden nicht direkt von unserem Server gesendet. Sie werden vom Transporter zum SMTP Server geleitet und dieser versendet die Emails dann.

Es gibt diverse Mailanbieter die uns einen smtp Port und Adresse zur Verfügung stellen. So das Wir uns mit einem usernamen und einen Passwort anmelden können.

GMAIL ist dort etwas tricky, google will dann das man seinen account für less secure apps entsperrt. Und genau diese Möglichkeit wollten sie am 06.2022 abschaffen