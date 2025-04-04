# Update software

```shell
sudo apt update
```

```shell
sudo apt full-upgrade
```

# Set proxy (if use proxy server)

## 1. System-Wide Proxy Configuration

1. Open the File:
   ```shell
   sudo nano /etc/environment
   ```

2. Add the Following Lines:
   ```text
   http_proxy="http://150.61.8.70:10086"
   https_proxy="http://150.61.8.70:10086"
   no_proxy="localhost,127.0.0.1"
   ```

3. Save and Exit:

   Press Ctrl+X, then Y, and Enter.

## 2. Configuring Proxy for APT (Package Manager)

1. Create/Edit the APT Proxy File:
   ```shell
   sudo nano /etc/apt/apt.conf.d/95proxies
   ```


2. Add These Lines:
   ```text
      Acquire::http::Proxy "http://150.61.8.70:10086";
      Acquire::https::Proxy "http://150.61.8.70:10086";
   ```

3. Save and Exit:

   Use Ctrl+X, then Y, and Enter.

## 3. Setting Proxy for a Single Session or Application

1. For the Current Session:

```shell
export http_proxy="http://150.61.8.70:10086"
export https_proxy="http://150.61.8.70:10086"
```

2. For a Specific Command:

```shell
http_proxy="http://150.61.8.70:10086" wget http://example.com
```

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
sudo date -s "2025-03-31 15:00:00"
```

# Install

## Install Virtual Keyboard on Raspberry Pi

```shell
sudo apt install onboard
sudo apt install at-spi2-core
```
