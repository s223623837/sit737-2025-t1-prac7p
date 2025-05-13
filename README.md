# MongoDB Deployment on Kubernetes with MongoDB Compass Access

## Overview

This project demonstrates how to deploy a MongoDB database on a Kubernetes cluster using secret management, persistent volumes, and service exposure. It also covers how to perform CRUD operations using MongoDB Compass by securely connecting to the database.

## Project Structure

```

.
├── mongo-secret.yaml         # Stores MongoDB credentials as Kubernetes secret
├── mongo-pvc.yaml            # Defines a PersistentVolumeClaim for data persistence
├── mongo-deployment.yaml     # MongoDB Deployment specification
├── mongo-service.yaml        # Service to expose MongoDB to the host machine
├── sample-data.json          # (Optional) Sample documents to use for testing
└── README.md                 # This file

````

## Setup Instructions

### 1. Apply Kubernetes Configuration Files

Run the following commands to deploy MongoDB into your Kubernetes cluster:

```bash
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-pvc.yaml
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml
````

### 2. Verify MongoDB Pod Status

Use this command to check if the MongoDB pod is running:

```bash
kubectl get pods
```

You should see the `mongo-deployment` pod in `Running` status.

### 3. Expose MongoDB Locally via Port Forwarding

Run the following to forward MongoDB's port 27017 to your local machine:

```bash
kubectl port-forward svc/mongo-service 27017:27017
```

Keep this terminal open to maintain the port-forwarding session.

---

## Connect Using MongoDB Compass

1. Open MongoDB Compass.
2. Use the following connection string:

```
mongodb://mongoUser:mongoPass@localhost:27017
```

3. Select `admin` as the authentication database.

---

## Sample CRUD Operations in MongoDB Compass

1. **Create Database**: `mydb`
2. **Create Collection**: `students`
3. **Insert Documents**:

```json
[
  {
    "name": "Alice Smith",
    "age": 22,
    "major": "Computer Science"
  },
  {
    "name": "Bob Johnson",
    "age": 24,
    "major": "Electrical Engineering"
  },
  {
    "name": "Carol Lee",
    "age": 23,
    "major": "Mechanical Engineering"
  },
  {
    "name": "David Kim",
    "age": 21,
    "major": "Civil Engineering"
  },
  {
    "name": "Emma Wilson",
    "age": 25,
    "major": "Data Science"
  }
]
```

4. Use Compass to:

   * Read documents
   * Update document fields
   * Delete individual documents

---

## Notes

* Ensure your MongoDB `mongo-service` uses a `NodePort` or `port-forward` to allow external tools like Compass to connect.
* You can scale, monitor, and modify the MongoDB instance as needed using `kubectl`.

---

## Cleanup

To delete all deployed resources:

```bash
kubectl delete -f mongo-secret.yaml
kubectl delete -f mongo-pvc.yaml
kubectl delete -f mongo-deployment.yaml
kubectl delete -f mongo-service.yaml
```

---

## Author

**Bidhan Gupta**
SIT737 - Task 7 Practical Submission
Deakin University

