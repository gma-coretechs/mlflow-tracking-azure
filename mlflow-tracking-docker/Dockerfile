FROM python:3.7.0-stretch

# Set the working directory to /
WORKDIR /app
# Copy the directory contents into the container at /
COPY ./mlflow-tracking-docker .

# Install any needed packages specified in requirements.txt
RUN apt-get update && \
 apt-get -y install python3-dev default-libmysqlclient-dev build-essential && \
 rm -rf /var/lib/apt/lists/*

RUN pip install -r requirements.txt && chmod +x setup_mlflow.sh

# REQUIRED:
# ENV AZURE_STORAGE_ACCESS_KEY <access_key>
# ENV MLFLOW_SERVER_FILE_STORE
# ENV MLFLOW_SERVER_DEFAULT_ARTIFACT_ROOT

# OPTIONAL (if unset, will set to default):
ENV MLFLOW_SERVER_HOST 0.0.0.0
ENV MLFLOW_SERVER_PORT 5000
ENV MLFLOW_SERVER_WORKERS 4

# NOTE: Needed to connect to MySQL in Azure
RUN wget https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem

CMD ["./setup_mlflow.sh"]
