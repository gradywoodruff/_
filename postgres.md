# Postgres

    $rm -rf /usr/local/var/postgres    # install the binary

    $ brew install postgresql

    # init it
    $ initdb /usr/local/var/postgres

    # start the postgres server
    $ postgres -D /usr/local/var/postgres

    # create your database
    $ createdb mydb


    # Access db.
    $ psql mydb
    psql (9.0.1)
    Type "help" for help.

On error, first update:

    brew update
    brew upgrade