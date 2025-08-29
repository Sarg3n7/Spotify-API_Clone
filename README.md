# 🎵 Spotify API Clone – Microservices with Spring Boot
A **Spotify-inspired backend project** built with **Java Spring Boot**, designed using a **microservices architecture**. This project demonstrates **scalable API development**, **hybrid database integration**, and **social networking features** for music applications. It is tailored to showcase backend development skills for **Java Developer roles**.

## 📌 Features
### 🎶 Song Microservice
- Create, update, delete, and retrieve songs (CRUD APIs).
- Manage song favorites count (increment/decrement).
- Stores songs in **MongoDB** (`songs` collection).

### 👤 Profile Microservice
- Create and manage user profiles with secure login.
- Follow / unfollow users.
- Like / unlike songs and maintain a "Liked Songs" playlist.
- Fetch all favorite songs of friends.
- Stores relationships in **Neo4j** (graph database).

## 🛠️ Tech Stack
- **Java 8 / Spring Boot** – REST API development  
- **Microservices Architecture** – Song Service & Profile Service  
- **MongoDB** – Song metadata storage (10k+ records)  
- **Neo4j** – User relationships & recommendations (1k+ connections)  
- **Maven** – Build automation & dependency management  
- **VS Code + Spring Boot Extension Pack** – Development & debugging  

## ⚙️ Installation & Setup
### 1. Prerequisites
- [Java JDK 8](https://adoptium.net/temurin/releases/?version=8)  
- [Apache Maven 3.6+](https://maven.apache.org/)  
- [MongoDB Community Edition](https://www.mongodb.com/try/download/community)  
- [Neo4j 3.5.25](https://neo4j.com/download-center/#community)  

### 2. Database Setup
#### MongoDB
```bash
# Start MongoDB
mongod

# Open Mongo Shell
mongosh "mongodb://localhost:27017"

# Create DB & Collection
use csc301-test
db.createCollection("songs")

# Insert sample song
db.songs.insertOne({
  songName: "Never Gonna Give You Up",
  songArtistFullName: "Rick Astley",
  songAlbum: "Whenever You Need Somebody",
  songAmountFavourites: 0
})
```

#### Neo4j
1. Start Neo4j:
   ```bash
   bin\neo4j.bat console
   ```
2. Open [http://localhost:7474](http://localhost:7474)  
3. Set password (e.g., `neo4j1234`)  
4. Ensure Bolt is running at `bolt://localhost:7687`.

### 3. Run Microservices
Open each service in separate terminals:
```bash
# For Song Microservice
cd song-microservice
mvn clean install -DskipTests
mvn spring-boot:run

# For Profile Microservice
cd profile-microservice
mvn clean install -DskipTests
mvn spring-boot:run
```
- Song Microservice → `http://localhost:3001`  
- Profile Microservice → `http://localhost:3002`  

## ⚙️ Configuration – application-example.properties
⚠️ For security, real credentials must **not** be committed. Instead, copy this template into your local `application.properties` file and fill in the actual DB details.
```properties
# ========================
# MongoDB Configuration
# ========================
spring.data.mongodb.uri=mongodb://localhost:27017/csc301-test

# ========================
# Neo4j Configuration
# ========================
spring.neo4j.uri=bolt://localhost:7687
spring.neo4j.authentication.username=neo4j
spring.neo4j.authentication.password=neo4j1234

# ========================
# Server Ports
# ========================
# Song Microservice
server.port=3001

# Profile Microservice
# (override in profile-microservice if needed)
server.port=3002
```

## 🚀 Example API Endpoints
### Song Service
- `POST /addSong?songName=Hello&songArtistFullName=Adele&songAlbum=25`  
- `GET /getSongTitleById/{songId}`  
- `PUT /updateSongFavouritesCount/{songId}?shouldDecrement=false`  

### Profile Service
- `POST /profile?userName=john&fullName=John Doe&password=1234`  
- `PUT /followFriend/john/alex`  
- `PUT /likeSong/john/{songId}`  
- `GET /getAllFriendFavouriteSongTitles/john`  

## 📌 Future Improvements
- Add JWT Authentication for secure profile management.  
- Containerize services with Docker for easy deployment.  
- CI/CD pipeline integration with GitHub Actions or Jenkins.  

