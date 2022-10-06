# Express Middleware und routing

-----------> Request (URL, Methode, Content-Type)

------------------------EXPRESS SERVER-------------------------
                            |
                            |
                            v
                    --------------- middleware app.use() --> middleware
                    Logging = ausgabe von req.method req.url dann next()
                    next() reicht den Request weiter
                            |
                            |
                            v
                    --------------- middleware
                    app.use(express.json())
                    Schaut nach dem Content-Type und wenn dieser 'application/json' ist
                    dann baut es uns ein req.body Object z.B. req.body.marke = 'Audi'
                    next() reicht den Request weiter
                            |
                            |
                            v
                    --------------- Routing
                    Routen definieren wir über die Request methode und die Request URL

                    app.get('/api/pirates)
                            | wenn die methode und/oder die URL nicht passt reiche den Request zur nächsten Route weiter
                            v
                    app.post('/api/schiffe)

                    app.use((req,res) => res.status(404).end()) 

--------------------------------------------------------------

<---------------- Response zum Client
