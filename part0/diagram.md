sequenceDiagram
    participant browser
    participant server

    browser->>server: User writes note and clicks Save
    activate browser
    browser->>browser: Capture note content and user action
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note with note data
    activate server
    server-->>server: Handle /new_note endpoint
    server-->>server: Add new note to notes array
    server-->>server: Redirect to /notes
    deactivate server
    server-->>browser: HTTP 302 (Redirect)
    deactivate browser

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
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes

