sequenceDiagram
participant internaut
participant browser
participant server

post => backend recup data => ajoute data en DB => return code 302 with location as headers for redirection to it

loaded html fetch css file and jsfile

jsfile loaded executes itself and fetch data from (url) then map on it to renders notes

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
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

    browser->>server: POST https://fullstack-exampleapp.herokuapp.com/new_note
    The note data is POSTED to the URL ending in "/new_note"
    activate server
    newdata = 1 object creation (key value item) in the "notes" array (from the data provided in the api call)
    deactivate server

    server-->>browser: State code 302 (Redirection to header's location) | {activation reload}
    request the body of POST request (newdata)
    deactivate server

    RELOADING PAGE STATEMENT
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes | HTML Document
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css | CSS Document
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js | JS Doc. server side rendered
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json | Array of DATA.json + newData.json
