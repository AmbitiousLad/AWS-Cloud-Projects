# A simple MERN stack application 

# File Structure
.
├── MERN-docker-compose
│   ├── docker-compose.yaml
│   ├── mern
│   │   ├── backend
│   │   │   ├── db
│   │   │   │   └── connection.js
│   │   │   ├── Dockerfile
│   │   │   ├── package.json
│   │   │   ├── package-lock.json
│   │   │   ├── routes
│   │   │   │   └── record.js
│   │   │   └── server.js
│   │   └── frontend
│   │       ├── cypress
│   │       │   ├── fixtures
│   │       │   │   └── example.json
│   │       │   ├── integration
│   │       │   │   └── endToEnd.spec.js
│   │       │   ├── plugins
│   │       │   │   └── index.js
│   │       │   └── support
│   │       │       ├── commands.js
│   │       │       └── index.js
│   │       ├── cypress.json
│   │       ├── Dockerfile
│   │       ├── index.html
│   │       ├── package.json
│   │       ├── package-lock.json
│   │       ├── postcss.config.js
│   │       ├── public
│   │       │   └── vite.svg
│   │       ├── src
│   │       │   ├── App.jsx
│   │       │   ├── assets
│   │       │   │   └── mongodb.svg
│   │       │   ├── components
│   │       │   │   ├── Navbar.jsx
│   │       │   │   ├── Record.jsx
│   │       │   │   └── RecordList.jsx
│   │       │   ├── index.css
│   │       │   └── main.jsx
│   │       ├── tailwind.config.js
│   │       └── vite.config.js
│   └── README.md
└── opt
    └── data
        ├── collection-0-6278686471770441124.wt
        ├── collection-2-6278686471770441124.wt
        ├── collection-4-6278686471770441124.wt
        ├── collection-7-6278686471770441124.wt
        ├── diagnostic.data
        │   ├── metrics.2025-03-16T07-15-59Z-00000
        │   └── metrics.interim
        ├── index-1-6278686471770441124.wt
        ├── index-3-6278686471770441124.wt
        ├── index-5-6278686471770441124.wt
        ├── index-6-6278686471770441124.wt
        ├── index-8-6278686471770441124.wt
        ├── journal
        │   ├── WiredTigerLog.0000000001
        │   └── WiredTigerPreplog.0000000001
        ├── _mdb_catalog.wt
        ├── mongod.lock
        ├── sizeStorer.wt
        ├── storage.bson
        ├── WiredTiger
        ├── WiredTigerHS.wt
        ├── WiredTiger.lock
        ├── WiredTiger.turtle
        └── WiredTiger.wt

19 directories, 51 files

### Create a network for the docker containers

`docker network create demo`

### Build the client 

```sh
cd mern/frontend
docker build -t mern-frontend .
```

### Run the client

`docker run --name=frontend --network=demo -d -p 5173:5173 mern-frontend`

### Verify the client is running

Open your browser and type `http://localhost:5173`

### Run the mongodb container

`docker run --network=demo --name mongodb -d -p 27017:27017 -v ~/opt/data:/data/db mongodb:latest`

### Build the server

```sh
cd mern/backend
docker build -t mern-backend .
```

### Run the server

`docker run --name=backend --network=demo -d -p 5050:5050 mern-backend`

## Using Docker Compose

`docker compose up -d`
