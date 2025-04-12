FROM python:3.12-slim
WORKDIR /app
ADD --checksum=sha256:9adccb8fe17a40252df1a3acdea7edef4633b4ecaa8ba2dd5e0270f87ae43eab https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.tar.gz /tmp/app.tar.gz
RUN tar -xzf /tmp/app.tar.gz --strip-components=1 -C /app && rm /tmp/app.tar.gz
RUN pip3 install --break-system-packages -r requirements.txt
CMD ["python3", "main.py"]