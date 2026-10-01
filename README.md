# User Login App with Docker, MongoDB & Mongo Express

A basic web app with **user registration and login**, backed by **MongoDB** running in Docker, with **Mongo Express** as a browser-based database viewer. Built as a hands-on project to learn Docker and container networking.

## Features

- Create a new user account
- Log in with an existing user
- User data stored in MongoDB
- MongoDB and Mongo Express run as Docker containers
- View and manage the database through the Mongo Express web UI

## Tech Stack

- **App:** Node.js + Express *(change if yours differs)*
- **Database:** MongoDB (Docker image)
- **DB admin UI:** Mongo Express (Docker image)
- **Containers:** Docker (and Docker Compose)

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed and running
- [Node.js](https://nodejs.org/) 18+ and npm

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

### 2. Start MongoDB and Mongo Express

Using Docker Compose:

```bash
docker-compose -f mongo.yaml up
```

Or manually:

```bash
# Create a network so the containers can talk to each other
docker network create mongo-network

# MongoDB
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb \
  --net mongo-network \
  mongo

# Mongo Express
docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  --name mongo-express \
  --net mongo-network \
  mongo-express
```

> The username and password above are for local learning only. Never use them in production.

### 3. Install dependencies and run the app

```bash
npm install
npm start
```

### 4. Open it

| Service | URL |
|---------|-----|
| App | http://localhost:3000 |
| Mongo Express | http://localhost:8081 |

## Usage

1. Open the app and click **Sign up** to create a user.
2. Log in with the credentials you just created.
3. Open Mongo Express to see the new user saved in the database.

## Project Structure

```
.
├── server.js        # Express server and routes
├── package.json
├── mongo.yaml       # Docker Compose file for MongoDB + Mongo Express
└── public/          # Frontend files (login / signup pages)
```

## Useful Docker Commands

```bash
docker ps                     # List running containers
docker logs mongodb           # View MongoDB logs
docker-compose -f mongo.yaml down   # Stop and remove containers
docker network ls             # List networks
```

## What I Learned

- Running databases in Docker containers
- Connecting multiple containers with a Docker network
- Using environment variables to configure containers
- Docker Compose for multi-container setups

## License

MIT