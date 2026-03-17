# rinetd: TCP/UDP port redirector

## Step 1: Install Development Tools

- CentOS
  ```bash
  yum groupinstall -y "Development Tools"
  yum install -y automake autoconf libtool
  ```

- Debian
  ```bash
  apt install -y build-essential automake unzip
  ```

## Step 2: Download and Extract `rinetd` Source Code

```bash
wget https://github.com/samhocevar/rinetd/archive/refs/heads/master.zip
unzip master.zip
cd rinetd-main
```

## Step 3: Compile and Install `rinetd`

```bash
./bootstrap
./configure
make
make install
```

## Step 4: Configure `rinetd`

```bash
apt install vim
vim /etc/rinetd.conf
```

Edit:

```conf
0.0.0.0 <local_port> <target_domain> <target_port>
```

## Step 5: Start / Restart `rinetd`

```bash
rinetd -c /etc/rinetd.conf
```

## Step 6: Verify the Status

```bash
netstat -antup | grep rinetd
```

## Step 7: Set Up Auto-Start on Boot

Run
```bash
chmod 755 /etc/rc.d/rc.local
vi /etc/rc.d/rc.local
```

Add
```local
/usr/local/sbin/rinetd -c /etc/rinetd.conf
```

## Problems

### Unable to connect

- Stop rinetd

  ```bash
  pkill rinetd
  ```

- Start rinetd

  ```bash
  rinetd -c /etc/rinetd.conf
  ```