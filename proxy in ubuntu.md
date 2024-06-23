## to use v2ray for ubuntu :

```shell
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
sudo bash install-release.sh
```

### start v2ray

run this command :

```shell
sudo v2ray -config [custom_config_json]
```


## to use clash

```shell
curl -sLo clash.gz https://github.com/Dreamacro/clash/releases/download/v1.11.8/clash-linux-amd64-v1.11.8.gz
gunzip clash.gz
chmod +x clash
sudo mv clash /usr/local/bin/
```

## to us trojan

```shell
sudo apt-get install trojan
```


## a python script for proxy config

```python
import socket
import select
import struct
from socketserver import ThreadingMixIn, TCPServer, StreamRequestHandler

class ThreadingTCPServer(ThreadingMixIn, TCPServer):
    pass

class SocksProxy(StreamRequestHandler):
    def handle(self):
        print(f'Accepting connection from {self.client_address}')
        
        # SOCKS5 initialization
        self.connection.recv(2)
        self.connection.send(b"\x05\x00")
        
        # SOCKS5 connection request
        data = self.connection.recv(4)
        mode = data[1]
        addrtype = data[3]

        if addrtype == 1:  # IPv4
            addr = socket.inet_ntoa(self.connection.recv(4))
        elif addrtype == 3:  # Domain name
            addr = self.connection.recv(ord(self.connection.recv(1)))
        port = struct.unpack('>H', self.connection.recv(2))[0]

        try:
            if mode == 1:  # CONNECT
                remote = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                remote.connect((addr, port))
                local = remote.getsockname()
                reply = struct.pack("!BBBBIH", 5, 0, 0, 1, local[0], local[1])
            else:
                reply = struct.pack("!BBBBIH", 5, 7, 0, 1, 0, 0)

            self.connection.sendall(reply)

            if reply[1] == 0 and mode == 1:
                self.exchange_loop(self.connection, remote)

        except Exception as e:
            print(f'Error: {e}')
            self.server.close_request(self.request)

    def exchange_loop(self, client, remote):
        while True:
            r, w, e = select.select([client, remote], [], [])
            if client in r:
                data = client.recv(4096)
                if remote.send(data) <= 0:
                    break
            if remote in r:
                data = remote.recv(4096)
                if client.send(data) <= 0:
                    break

if __name__ == '__main__':
    with ThreadingTCPServer(('0.0.0.0', 9011), SocksProxy) as server:
        server.serve_forever()
```


