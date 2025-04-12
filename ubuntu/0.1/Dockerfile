FROM ubuntu:24.10
RUN apt-get update && apt-get install -y python3 python3-pip && rm -rf /var/lib/apt/lists/*
WORKDIR /app
ARG SJP_TAG=0.1.1
ARG SJP_HASH=30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b
ADD --checksum=sha256:${SJP_HASH} https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${SJP_TAG}.tar.gz /tmp/app.tar.gz
RUN tar -xzf /tmp/app.tar.gz --strip-components=1 -C /app && rm /tmp/app.tar.gz
RUN pip3 install --break-system-packages -r requirements.txt
CMD ["python3", "main.py"]