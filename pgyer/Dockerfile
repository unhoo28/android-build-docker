FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
	curl

# Download pgyer upload tool
RUN curl -# -O https://gh.api.99988866.xyz/https://raw.githubusercontent.com/PGYER/upload-app-api-example/main/shell-demo/pgyer_upload.sh && \
        chmod +x pgyer_upload.sh