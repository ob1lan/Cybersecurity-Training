This basic [Dockerfile](https://docs.docker.com/engine/reference/builder/) can be used to build a basic Kali image with some customisation:
```docker
FROM kalilinux/kali-rolling

LABEL version="1.0" \
      author="Ob1lan" \
      description="Custom Kali Linux container"

# Set working directory to /root
WORKDIR /root

# Install packages (will take time)
RUN apt update && apt -y upgrade && apt -y install kali-linux-headless

ENTRYPOINT ["/bin/bash"]
```
## Usage
```bash
docker build -t mykali .
docker run -it mykali
```
