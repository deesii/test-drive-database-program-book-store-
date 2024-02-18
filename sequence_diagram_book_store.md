:::mermaid

sequenceDiagram
    participant t as terminal
    participant app as Main program (in app.py)
    participant ar as books_repository class <br /> (in lib/books_repository.py)
    participant db_conn as database_connection class in (in lib/database_connection.py)
    participant db as Postgres database

    Note left of t: Flow of time <br />⬇ <br /> ⬇ <br /> ⬇ 

    t->>app: Runs `python app.py`
    app->>db_conn: Opens connection to database by calling .connect method on database_connection
    db_conn->>db_conn: Opens database connection using PG and stores the connection
    app->>ar: Calls all method on books_repository
    ar->>db_conn: Sends SQL query by calling execute method on db_conn
    db_conn->>db: Sends query to database via the open database connection
    db->>db_conn: Returns an list of dictionaries, one for each row of the books table

    db_conn->>ar: Returns an instance of objects, one for each row of the books table
    loop 
        ar->>ar: Loops through list and creates a book object for every row
    end
    ar->>app: Returns list of book objects
    app->>t: Prints list of books to terminal

:::