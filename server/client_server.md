# Client Server Prinzip

        |       Request
        |   ------------->      |
 Client |                       |
        |                       | Server
        |                       |
        |                       |
        |   <-----------------  |
        |   Response

## Aufbau eines Request

- Methode: GET POST PUT DELETE 
- Url: z.B https://localhost:9898/api/piraten
- Header: Konfiguation des request
    - Content-Type: 'application/json'      (app.use(express.json()))
                    'multipart/formdata'
    - credentials: include
- Body: packen wir bei Bedarf Daten rein

### example fetch (frontend)
fetch('https://localhost:9898/api/piraten', {
    method: 'POST',
    headers: {
        'content-type': 'application/json'
    },
    body: JSON.stringify({piratenname: 'Huck', ...})
})

## Aufbau einer Response
- Header: 
 - cors: Access-Control-Allow-Origin: *
### CORS-HEADER
Header set Access-Control-Allow-Origin "https://externe.quelle"
Header set Access-Control-Allow-Methods "GET,PUT,POST,DELETE"
Header set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"

- Status (200 alls ok, 404 not found, 403 unauthorized, 500 internal server error)
- Body: packen wir bei Bedarfdaten rein
