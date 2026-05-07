# fastapi-elasticsearch-project
FastAPI + Elasticsearch Dockerized Project  This project is a simple backend application built using FastAPI, Elasticsearch, and Docker. The application provides REST APIs to store and search user data using Elasticsearch as the search engine database.

# Build Docker image from Dockerfile
docker build -t fastapi-es .

# Run Elasticsearch container with low RAM usage
docker run -d \
--name elasticsearch \
-p 9200:9200 \
-e discovery.type=single-node \
-e xpack.security.enabled=false \
-e ES_JAVA_OPTS="-Xms256m -Xmx256m" \
docker.elastic.co/elasticsearch/elasticsearch:7.17.10

# Verify Elasticsearch
# Check Elasticsearch response
curl localhost:9200


# STEP 9 : Run FastAPI Container
# Run FastAPI application container
docker run -d \
--name fastapi-container \
-p 8000:8000 \
fastapi-es


# Verify Running Containers

# Show running containers
docker ps



# Check FastAPI Logs

# Show container logs
docker logs fastapi-container


# Test Home API

# Open in browser:
# http://YOUR_PUBLIC_IP:8000

# OR test using curl
curl http://YOUR_PUBLIC_IP:8000


# ================================
# Add Data API
# ================================

# Add data into Elasticsearch
curl -X POST "http://YOUR_PUBLIC_IP:8000/add?name=kadir"


# ================================
# Search Data API
# ================================

# Search stored data
curl "http://YOUR_PUBLIC_IP:8000/search?q=kadir"

