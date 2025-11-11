# gopy-java

Java (Spring Boot) rewrite of your static site with Docker deployment.

## What's inside
- Serves your original `index.html` and `styles.css` at `/`
- Example REST endpoints:
  - `GET /api/health` → returns JSON status
  - `POST /api/echo`  → echoes JSON body
- Dockerfile and docker-compose for easy deployment

## Prereqs
- JDK 21 (Temurin recommended)
- Maven 3.9+
- Docker Desktop

## Run locally (no Docker)
```bash
mvn spring-boot:run
```
Open http://localhost:8080/

## Build the JAR
```bash
mvn -q -DskipTests package
```
The JAR will be at `target/gopy-java-1.0.0.jar`.

## Build & run with Docker
```bash
docker build -t gopy-java:1.0.0 .
docker run --rm -p 8080:8080 gopy-java:1.0.0
```

## Or use docker-compose
```bash
docker compose up --build
```

If you hit Windows port conflicts (e.g., MySQL using 3306), change the published port in `docker-compose.yml`.

## Project layout
```
src/
  main/
    java/com/example/
      Application.java
      config/CorsConfig.java
      web/ApiController.java
    resources/
      application.properties
      static/
        index.html
        styles.css
Dockerfile
docker-compose.yml
```

## Notes
- Static assets are served from `src/main/resources/static`.
- You can evolve the API under `com.example.web` to match your future needs.
