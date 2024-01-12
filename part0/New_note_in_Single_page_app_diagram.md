sequenceDiagram
    participant browser
    participant server

    browser->>server: User creates a new note
    activate browser
    browser->>browser: Capture note content and user action
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/spa/new_note with note data
    activate server
    server-->>server: Handle SPA /new_note endpoint
    server-->>server: Add new note to notes array
    server-->>server: Respond with updated notes data
    deactivate server
    server-->>browser: Updated notes data
    deactivate browser

    Note right of browser: The SPA updates the UI with the new note
