sequenceDiagram | User visiting the Single Page App
participant internaut
participant browser
participant server

Visiting SPA page => rethrieving HTML file (GET Method) => rethrieving CSS file (GET Method) => rethrieving JS file (GET Method) => rethrieving ARRAY OF DATA JSON (GET Method)

loaded html, fetch css file, jsfile & data.json

jsfile loaded executes itself and fetch data from (url) then map on it to renders notes

    internaut->>browser: visiting SPA page

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
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

    Note right of browser: The browser executes the callback function that renders the notes

    
