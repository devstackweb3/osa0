sequenceDiagram participant internaut participant browser participant server

post => backend recup data => ajoute newdata localement (storage local) => POST newdata.json en DB (serveur) => return code 201 Created

loaded html, fetch css file, fetch js file, fetch array of data.json (coming from server side), and add newdata.json (to server side) 

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
activate server
server-->>browser: HTML document
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
activate server
server-->>browser: the css file
deactivate server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
activate server
server-->>browser: the JavaScript file
deactivate server

Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
activate server
server-->>browser: [{ "content": "My added note", "date": "2023-1-1" }, ... ]
deactivate server

internaut->>browser: formular's button pushed
attributes action & method: POST

browser: 
main.js file auto-execution on browser side, storing newdata locally

browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note | State code 201 Created
The note data is POSTED to the URL ending in "/new_note"
activate server
newdata = 1 object creation (key value item) in the "notes" array (from the data provided in the api call)
deactivate server

browser: No DOM reload needed
No event handler execution rendering list of notes needed | NO RELOADING SECTION DATA STATEMENT (Static HTML | JS execution browser side) 
