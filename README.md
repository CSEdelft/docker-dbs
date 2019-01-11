# Dockerized databases for CSE1500

Pros:
1. Databases are cleanly separated from your system
2. Identical setup for everyone (easier to debug)
3. Closer to a production setup
4. Easy to remove after you are done

Cons:
1. A tiny bit less performant

## How to

1. [Install Docker](https://docs.docker.com/install/)
2. ```git clone https://github.com/CSEdelft/docker-dbs```
3. ```cd docker-dbs```
4. cd into a database directory
5. ```make``` (wait a bit for the database to start)
6. ```make connect```
7. Do your thing.
8. ```make kill``` (shutdown the database and remove the image)

## Known Issues

On macOS you have to allow docker access into the directory, otherwise it cannot bind to the filesystem and persist database data (and won't even start). Do this in ```Docker->Preferences->File Sharing```.

