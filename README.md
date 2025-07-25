# Demo App – Docker Compose Crash Course

A beginner-friendly project to demonstrate running a Node.js app with MongoDB and Mongo Express using **Docker** and **Docker Compose**.

---

## Tech Stack

- Node.js + Express
- MongoDB
- Mongo Express (GUI for MongoDB)
- Docker & Docker Compose

---

## With Docker (Manual Method)

### Step 1: Create Docker Network

This step helps both containers communicate using a common bridge network.

```bash
docker network create mongo-network
````

> 🔹 **Note:** This step is optional. If you don’t use a custom network, Docker’s default bridge network will still allow basic inter-container communication.

---

### Step 2: Start MongoDB Container

```bash
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb \
  --net mongo-network \
  mongo
```

---

### Step 3: Start Mongo Express Container

```bash
docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  --name mongo-express \
  --net mongo-network \
  mongo-express
```

---

## With Docker Compose (Recommended)

### Step 1: Clone the Repository

```bash
git clone https://github.com/mloges-h/Docker_nodejs_mangodb_mangoexpress.git
cd docker-compose-crash-course
```

### Step 2: Start All Services

```bash
docker-compose -f docker-compose.yaml up -d
```

This will start:

* Node.js app on port `3000`
* MongoDB on port `27017`
* Mongo Express on port `8081`

---

### Step 3: Open Mongo Express in Your Browser

```text
http://<your-server-ip>:8081
```

> Example: `http://localhost:8081`

1. Create a database called: **my-db**
2. Inside that, create a collection: **my-collection**
3. Add a document:

```json
{
  "myid": 1,
  "data": "MongoDB connected successfully Logesh!"
}
```

---

### Step 4: Open the Node.js App UI

```text
http://<your-server-ip>:3000
```

> The app will fetch dynamic data from MongoDB and render it in the browser.

---

## API Endpoints

| Endpoint      | Method | Description                              |
| ------------- | ------ | ---------------------------------------- |
| `/`           | GET    | Loads HTML UI                            |
| `/fetch-data` | GET    | Fetches data from MongoDB (by `myid: 1`) |

---

## Project Structure

```
.
├── app/
│   ├── index.html
│   ├── server.js
│   ├── package.json
├── .env
├── Dockerfile
├── docker-compose.yaml
└── README.md
```

---

## Key Learning Outcomes

* Use of `docker-compose.yaml` for multi-container orchestration
* Managing environment variables via `.env` file
* Accessing MongoDB via browser with Mongo Express
* Connecting Node.js app to MongoDB using credentials securely

---

## Author

**Logesh M**
Linux & Cloud Support Engineer | DevOps Learner
🔗 [GitHub](https://github.com/mloges-h)

---
