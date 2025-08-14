# Date

## 1. Verify the System Date and Time

```shell
date
```

## 2. Update the System Time

Using NTP (Network Time Protocol):

```shell
sudo timedatectl set-ntp true
```

Manually Setting the Date and Time:

```shell
sudo date -s "2025-09-01 00:00:00"
```

# Set proxy (if using a proxy server)

## 1. System-Wide Proxy Configuration

1. Open the File:
   ```shell
   sudo nano /etc/environment
   ```

2. Add the Following Lines:
   ```text
   http_proxy="http://150.61.8.70:10080"
   https_proxy="http://150.61.8.70:10080"
   no_proxy="localhost,127.0.0.1"
   ```

3. Save and Exit:

   Press Ctrl+X, then Y, and Enter.

## 2. Setting Proxy for a Single Session or Application

1. For the Current Session:

```shell
export http_proxy="http://150.61.8.70:10080"
export https_proxy="http://150.61.8.70:10080"
```

- For reset
   ```shell
   unset http_proxy
   unset https_proxy
   ```


2. For a Specific Command:

```shell
http_proxy="http://150.61.8.70:10080" wget http://example.com
```

# Update software

```shell
sudo apt update
```

```shell
sudo apt full-upgrade
```

# Install

## Remote Desktop

```bash
sudo apt-get install xrdp
```

## Install Python on the Raspberry Pi

install the build tools

```bash
sudo apt update
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev  libsqlite3-dev
```  

download

```bash
cd /usr/src
sudo wget https://www.python.org/ftp/python/3.12.6/Python-3.12.6.tgz
sudo tar -xzvf Python-3.12.6.tgz 
cd Python-3.12.6/
```

```bash
sudo ./configure --enable-optimizations
sudo make altinstall
```

```bash
/usr/local/bin/python3.12 -V
/usr/bin/python3 -V
```

```bash
sudo rm /usr/bin/python
sudo rm /usr/bin/python3
```

```bash
sudo ln -s /usr/local/bin/python3.12 /usr/bin/python
sudo ln -s /usr/local/bin/python3.12 /usr/bin/python3
```