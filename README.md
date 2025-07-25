# Demo App – Docker Compose Crash Course

A beginner-friendly project to demonstrate running a Node.js app with MongoDB and Mongo Express using **Docker** and **Docker Compose**. Once 

> **After cloning the repository from GitHub, make sure to update the `/app/index.html` file. Replace `localhost` URLs with your actual server IP address.**
<img width="650" height="542" alt="image" src="https://github.com/user-attachments/assets/6d08db95-9d07-43fa-92a7-10c961cf4d8f" />

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
docker run -itd -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
```

---

### Step 3: Start Mongo Express Container

```bash
docker run -itd -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password -e ME_CONFIG_MONGODB_SERVER=mongodb --name mongo-express --net mongo-network mongo-express
```
## Step 4: Build and run your Node.js App

Go to the directory containing your Dockerfile and server.js.

## Build the image:

docker build -t my-node-app .

## Run the container:

```bash
docker run -itd -p 3000:3000 -e MONGO_DB_USERNAME=admin -e MONGO_DB_PWD=supersecret --name node-app --net mongo-network my-node-app
```
## Step 5: Test everything

```text
http://<your-server-ip>:8081
```
> Example: `http://<your-server-ip>:8081`

1. Create a database called: **my-db**
2. Inside that, create a collection: **my-collection**
3. Add a document:

```json
{
  "myid": 1,
  "data": "MongoDB connected successfully Logesh!"
}
```
## Why we doing this? Because of server.js we have mentioned it
<img width="679" height="252" alt="image" src="https://github.com/user-attachments/assets/4193696a-3cd0-465e-8380-2394df980dc3" />

## Visit your Node.js app `http://<your-server-ip>:3000`

## Before writing new document 
<img width="888" height="341" alt="image" src="https://github.com/user-attachments/assets/1a565c6e-9571-4a21-96f7-a6464a12ac50" />

## After writing new document 
<img width="882" height="371" alt="image" src="https://github.com/user-attachments/assets/d1f1a992-f64c-4578-ace8-725e68c2a23e" />

## With Docker Compose (Recommended)

### Step 1: Clone the Repository

```bash
git clone https://github.com/mloges-h/Docker_nodejs_mangodb_mangoexpress.git
cd Docker_nodejs_mangodb_mangoexpress
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
## Why we doing this? Because of server.js we have mentioned it
<img width="679" height="252" alt="image" src="https://github.com/user-attachments/assets/4193696a-3cd0-465e-8380-2394df980dc3" />
---

### Step 4: Open the Node.js App UI

```text
http://<your-server-ip>:3000
```
## Before writing new document 
<img width="888" height="341" alt="image" src="https://github.com/user-attachments/assets/78d1c9b6-f8a1-4118-a257-fab39aef5de6" />

## After writing new document 
<img width="882" height="371" alt="image" src="https://github.com/user-attachments/assets/4f7d0c32-675e-427a-a43c-dcd462180309" />

> The app will fetch dynamic data from MongoDB and render it in the browser.

---

## API Endpoints

| Endpoint      | Method | Description                              |
| ------------- | ------ | ---------------------------------------- |
| `/`           | GET    | Loads HTML UI                            |
| `/fetch-data` | GET    | Fetches data from MongoDB (by `myid: 1`)
                          which is in server.js |

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
