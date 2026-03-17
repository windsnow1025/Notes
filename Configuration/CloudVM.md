# Cloud VM

## System

- Switch User: `su - <username>`
- OS: `cat /etc/os-release`
- Disk: `df -h`
- RAM: `free -h`
- CPU: `top`
- Fetch URL: `wget --spider <url>`

## Root Login

1. Create password for root user

```bash
sudo passwd root
```

2. Login as root user

```bash
su -
```

### SSH Key Pair

1. Generate key pair

```bash
ssh-keygen -t rsa
```

2. Copy public key to authorized keys

```bash
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
```

3. View private key and save to `id_rsa`

```bash
cat /root/.ssh/id_rsa
```

### Permit Root Login (Optional: GCP)

1. Edit sshd_config
    ```bash
    vim /etc/ssh/sshd_config
    ```

   Edit:
    ```bash
    PermitRootLogin yes
    ```

2. Restart ssh
    ```bash
    systemctl restart ssh
    ```

## Nginx + HTTPS

1. Install Nginx
  ```bash
  apt update
  apt install nginx
  apt install libnginx-mod-stream
  ```
2. Update config files: `/etc/nginx/nginx.conf` and `/etc/nginx/sites-available/default`
3. Reload config: `nginx -s reload`
4. Certbot Certificates

  ```bash
  apt install snapd
  snap install core
  snap install --classic certbot
  ln -s /snap/bin/certbot /usr/bin/certbot
  ```

5. Cert
  ```bash
  certbot --nginx
  ```

### Nginx Command

- Uninstall Nginx: `apt remove nginx nginx-common`, `apt purge nginx nginx-common`
- Start Nginx: `systemctl start nginx`
- Stop Nginx: `nginx -s stop`
- Check Error Log: `cat /var/log/nginx/error.log`

### Remove Cert

```bash
certbot revoke --cert-name <domain_name>
```

Clear certbot config in `/etc/nginx/sites-available/default`.

### Problems

HTTP POST Request will be redirected to HTTPS GET Request causing unexpected behavior.