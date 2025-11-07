# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
    ```
    curl http://localhost:3000/users
    ```
    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**  
    ```
    curl http://localhost:3001/products
    ```
    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---

### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**  
    ```
    curl http://localhost:3002/orders
    ```
    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**  
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**  
    ```
    curl http://localhost:3003/api/orders
    ```

---

## Instructions
Step 1: gitclone "https://github.com/jatinggg/Microservices-Dockerized-Task.git" 
Step 2: Add a Dockerfile for each of the services
Step 3: Add following code in the dockerfile for each service Exposing the appropriate ports:
        # example gateway-service
        FROM node:21-alpine
        WORKDIR /app
        COPY package*.json ./
        RUN npm install
        COPY . .
        EXPOSE 3003
        CMD ["npm", "start"]

    user-service : port 3000
    product-service : port 3001
    order-service : port 3002
    gateway-service : port 3003

Step 4: Add the "start":"node app.js" script in the package.json for each service to run the node application 
        example 
        {
                "name": "microservice",
                "version": "1.0.0",
                "dependencies": {
                      "express": "^4.17.1",
                      "axios": "^0.24.0"
                },
                "scripts":{
                      "start":"node app.js"
                }
        }

Step 5: Add docker-compose file under the microservices folder with following code :

    version: '3.8'

    services:
      user-service:
        build: ./user-service
        ports:
          - "3000:3000"

    product-service:
      build: ./product-service
      ports:
        - "3001:3001"

    order-service:
      build: ./order-service
      ports:
        - "3002:3002"

    gateway-service:
      build: ./gateway-service
      ports:
        - "3003:3003"


Step 6: In the terminal run below code to build and run the containers 
        docker-compose up --build

Step 7: Once the services are running, use the above endpoints to verify the functionality.

Happy testing!
