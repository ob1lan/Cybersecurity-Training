This basic [Dockerfile](https://docs.docker.com/engine/reference/builder/) can be used to build a basic Kali image with some customisation:
```Dockerfile
FROM kalilinux/kali-rolling

LABEL version="1.0" \
      author="Ob1lan" \
      description="Custom Kali Linux container"

# Set working directory to /root
WORKDIR /root

# Install packages (will take time)
RUN apt update && apt -y upgrade && apt-get install dialog apt-utils -y
RUN apt -y install kali-linux-headless && \
	# clear apt cache/packages
    apt -y autoclean && apt -y autoremove && apt -y clean
	
RUN	git clone https://github.com/Dewalt-arch/pimpmykali && \
	cd pimpmykali && \
	sudo ./pimpmykali.sh --all
	
run apt -y install xrdp && systemctl enable xrdp && systemctl enable xrdp-sesman

RUN echo "kali ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd --create-home --shell /bin/zsh --user-group --groups sudo kali && \
    echo "kali:kali" | chpasswd

# For Reverse Shells and RDP
EXPOSE 4444/tcp
EXPOSE 3389/tcp

ENTRYPOINT ["/bin/bash"]
```
## Usage
```Shell
docker build -t mykali .
docker run -it mykali
```
