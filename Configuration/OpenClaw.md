# OpenClaw

## Commands

- Start: `openclaw gateway start`
- Restart: `openclaw gateway restart`
- Configure: `openclaw configure`
- Analysis: `openclaw doctor`
- List Skills: `openclaw skills list`
- Get Config: `openclaw config get <key>`
- Template Directory: `cd $(npm root -g)/openclaw/docs/reference/templates/`

## Requirements

RAM: 4GB; Disk: 20GB

## Dependencies

### Node.js

```bash
apt update
apt install nodejs
apt install lsof
```

### For Skills

- Install pnpm
    ```bash
    npm install -g pnpm
    source /root/.bashrc
    ```
- Upgrade Go
    ```bash
    apt remove golang-go
    curl -LO https://go.dev/dl/go1.26.1.linux-amd64.tar.gz
    rm -rf /usr/local/go && tar -C /usr/local -xzf go1.26.1.linux-amd64.tar.gz
    rm go1.26.1.linux-amd64.tar.gz
    export PATH=$PATH:/usr/local/go/bin
    echo 'export PATH=$PATH:/usr/local/go/bin' >> /root/.bashrc
    ```
- Install uv
    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    source $HOME/.local/bin/env
    ```
- Install Homebrew
  1. In non-root user
      ```bash
      /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
      eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
      echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.bashrc
      ```
  2. In root user
      ```bash
      export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"
      echo 'export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"' >> /root/.bashrc
      ```

## Configuration

Primary:

```bash
export NODE_COMPILE_CACHE=/var/tmp/openclaw-compile-cache
mkdir -p /var/tmp/openclaw-compile-cache
export OPENCLAW_NO_RESPAWN=1

echo 'export NODE_COMPILE_CACHE=/var/tmp/openclaw-compile-cache' >> ~/.bashrc
echo 'export OPENCLAW_NO_RESPAWN=1' >> ~/.bashrc
```

Config:

```bash
openclaw config set tools.profile full
openclaw config set gateway.bind lan
openclaw config set gateway.controlUi.allowedOrigins '["*"]'
```

### Nginx

Use the server block in `/etc/nginx/sites-available/default`

```bash
server {
    server_name <server_name>;

    location / {
        proxy_pass http://localhost:18789/;

        proxy_buffering off;
        proxy_request_buffering off;

        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Port $server_port;
        proxy_set_header X-Forwarded-Host $host;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### Dashboard Token

```bash
openclaw config set gateway.auth.token '<token>'
```

Open the dashboard URL and paste the token in Control UI settings

```bash
openclaw devices list
openclaw devices approve <requestId>
```

### Optional

#### Telegram

@BotFather >> `/mybots` >> Bot Settings >> Group Privacy >> Turn off

```bash
openclaw config set channels.telegram.groupPolicy open
```

##### Group Chats

`/activation`: `always`

##### *Group command privilege under pair mode bug workaround

@userinfobot >> `/start` >> Get `Id`

```bash
openclaw config set channels.telegram.allowFrom '["<TelegramID>"]'
```

#### gog

1. APIs & Services

   APIs & Services >> Enabled APIs & Services >> Enable APIs and services:
  - Gmail API
  - Google Calendar API
  - Google Drive API
  - Google People API
  - Google Sheets API
  - Google Docs API

2. Client

   Google Auth Platform >> Clients >> Get started: Audience: External

   Google Auth Platform >> Audience >> Test users >> Add users: <email>

3. OAuth

   Google Auth Platform >> Overview >> Create OAuth client: Application type: Desktop app >> Download JSON

   Rename `client_secret_<id>.apps.googleusercontent.com.json` to `credentials.json` and upload to `/root/.config/gogcli/credentials.json`.

4. Data Access

   Google Auth Platform >> Data Access >> Add or remove scopes:
  - https://www.googleapis.com/auth/gmail.readonly
  - https://www.googleapis.com/auth/calendar.readonly
  - https://www.googleapis.com/auth/drive.readonly
  - https://www.googleapis.com/auth/contacts.readonly
  - https://www.googleapis.com/auth/spreadsheets.readonly
  - https://www.googleapis.com/auth/documents.readonly

5. gog

    ```bash
    gog auth credentials /root/.config/gogcli/credentials.json
    rm -rf /root/.config/gogcli/keyring
    gog auth add <email> \
      --services gmail,calendar,drive,sheets,docs,contacts \
      --readonly \
      --remote
    ```

   Open `auth_url` and get <redirect-url>.

    ```bash
    gog auth add <email> \
      --services gmail,calendar,drive,sheets,docs,contacts \
      --readonly \
      --remote \
      --step 2 \
      --auth-url "<redirect_url>"
    ```

   Enter passphrase to unlock "/root/.config/gogcli/keyring": `gocli`