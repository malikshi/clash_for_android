**Table of Contents**

- [Clash For Android Config](#clash-for-android-config)
- [Features](#features)
  - [Clash for Android](#clash-for-android)
    - [Download Config](#download-config)
    - [Edit Files Proxy Provider](#edit-files-proxy-provider)
      - [Shadowsocks](#shadowsocks)
      - [Vmess](#vmess)
      - [Snell](#snell)
      - [Trojan](#trojan)
    - [Edit Files Rule Provider](#edit-files-rule-provider)
      - [Rule Direct/Bypassed Connection](#rule-directbypassed-connection)
    - [Setting Clash For Android](#setting-clash-for-android)
        - [Import Main.yaml](#import-mainyaml)
        - [Import Proxy Provider](#import-proxy-provider)
        - [Import Rule Provider](#import-rule-provider)
        - [Start Clash For Android](#start-clash-for-android)

# Clash For Android Config

Clash For Android Config untuk VVIP IPTUNNELS
- [Buy VVIP IPTUNNELS](https://linktr.ee/iptunnelscom)
- [Join Telegram](https://t.me/joinchat/RihiceTtK1QhBMm7)
- [Requests Rules](https://github.com/malikshi/open_clash/issues/new/choose)

# Features

* Pisah traffik umum, sosmed, streaming, gaming.
* Adblock & Privacy rules.
* Support Gaming filtering port.
* Support web streaming locked region ID.
* Support 10 marketplace ID.
* Support Direct/Bypass traffik.


## Clash for Android

Antarmuka UI dari clash untuk Android. Kompatibel dengan Shadowsocks ShadowsocksR, Vmess, Trojan, Snell dan protokol lainnya, dan mengimplementasikan proxy kebijakan sesuai dengan konfigurasi aturan yang fleksibel.

### Download Config

Download zip master dan ekstrak file [**clash_for_android-main.zip**](https://codeload.github.com/malikshi/clash_for_android/zip/refs/heads/main)

Video : [Download Config](https://youtu.be/lgyJ_ohdYgM)

### Edit Files Proxy Provider


Mengisi akun tunnel pada setiap files pada folder proxy_provider yang dimana terdapat file umum.yaml, gaming.yaml, sosmed.yaml, streaming.yaml, dan trafficIndo.yaml.
Fungsi dari masing masing proxy provider
* umum.yaml digunakan untuk traffic browsing secara umum yang tidak masuk dalam rule provider.
* gaming.yaml digunakan untuk traffic gaming, dan gunakan tipe proxy yang memiliki latency kecil.
* sosmed.yaml digunakan untuk traffic sosial media.
* streaming.yaml digunakan untuk traffic streaming seperti youtube, twitch, anime.
* trafficIndo.yaml dikhususkan untuk websites/layanan yang diharuskan untuk menggunakan lokasi Indonesia seperti netflix, disney+, marketplace online, dan VOD Streaming lainnya.

Video : [Edit Proxy Provider](https://youtu.be/dANGCW91E1k)

#### Shadowsocks

* Shadowsocks Original / tanpa plugin
```yaml
- name: "shadowsocks"
  type: ss
  server: aaa.bbb.ccc.ddd
  port: 34963
  cipher: chacha20-ietf-poly1305
  password: passwordss
  udp: true
```
* Shadowsocks dengan plugin obfs
```yaml
- name: "shadowsocks obfs"
    type: ss
    server: aaa.bbb.ccc.ddd
    port: 32033
    cipher: chacha20-ietf-poly1305
    password: passwordss
    plugin: obfs
    plugin-opts:
      mode: tls
      host: BUG.COM
```

#### Vmess

* Vmess websocket dengan BUG SNI
```yaml
- name: "Vmess ws bug SNI"
  type: vmess
  server: aaa.bbb.ccc.ddd
  port: 443
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  udp: true
  tls: true
  skip-cert-verify: true
  servername: BUGSNI.COM
  network: ws
  ws-opts:
    path: /iptunnelscom
    headers:
      Host: BUGSNI.COM
    max-early-data: 2048
    early-data-header-name: Sec-WebSocket-Protocol
```
* Vmess websocket dengan BUG CDN (bolak-balik)
```yaml
- name: "vmess ws bug CDN"
  type: vmess
  server: IPCDN/BUGCDN.COM
  port: 443
  uuid: UUIDMU
  alterId: 0
  cipher: auto
  udp: true
  tls: true
  skip-cert-verify: false
  servername: namadomainservermu.com
  network: ws
  ws-opts:
    path: /iptunnelscom
    headers:
      Host: namadomainservermu.com
    max-early-data: 2048
    early-data-header-name: Sec-WebSocket-Protocol
```
* Vmess gRPC bug SNI
```yaml
proxies:
  - name: vmess grpc SNI
    server: aaa.bbb.ccc.ddd
    port: 443
    type: vmess
    uuid: UUIDMU
    alterId: 0
    cipher: auto
    network: grpc
    tls: true
    servername: BUGSNI.COM
    skip-cert-verify: true
    grpc-opts:
      grpc-service-name: grpcpath
```
* Vmess gRPC bug CDN
```yaml
proxies:
  - name: vmess grpc CDN
    server: IPCDN/BUGCDN.COM
    port: 443
    type: vmess
    uuid: UUIDMU
    alterId: 0
    cipher: auto
    network: grpc
    tls: true
    servername: namadomainservermu.com
    skip-cert-verify: false
    grpc-opts:
      grpc-service-name: grpcpath
```

#### Snell

* Snell Server v3 (support udp).
```yaml
- name: "snell server"
  type: snell
  server: aaa.bbb.ccc.ddd
  port: 33223
  psk: password
  version: 3
  udp: true
  obfs-opts:
    mode: tls
    host: BUGSNI.COM
```

#### Trojan

* Trojan-gfw bug SNI
```yaml
- name: "trojan-gfw SNI"
  type: trojan
  server: aaa.bbb.ccc.ddd
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
    - h2
    - http/1.1
  skip-cert-verify: true
```
* Trojan-go websocket bug CDN
```yaml
- name: trojan ws cdn
  server: IPCDN/BUGCDN.COM
  port: 443
  type: trojan
  password: PASSWORD
  network: ws
  sni: namadomainservermu.com
  skip-cert-verify: false
  udp: true
  ws-opts:
    path: /iptunnelstrgo
    headers:
        Host: namadomainservermu.com
```
* Trojan gRPC bug SNI
```yaml
- name: "trojan gRPC SNI"
  type: trojan
  server: aaa.bbb.ccc.ddd
  port: 443
  password: PASSWORD
  udp: true
  sni: BUGSNI.COM
  alpn:
  - h2
  skip-cert-verify: true
  network: grpc
  grpc-opts:
    grpc-service-name: iptunnelstrojangrpc
```
* Trojan gRPC bug CDN
```yaml
- name: "trojan gRPC CDN"
  type: trojan
  server: IPCDN/BUGCDN.COM
  port: 443
  password: PASSWORD
  udp: true
  sni: namadomainservermu.com
  alpn:
  - h2
  skip-cert-verify: false
  network: grpc
  grpc-opts:
    grpc-service-name: iptunnelstrojangrpc
```


### Edit Files Rule Provider

Config Openclash VVIP IPTUNNELS kalian tidak perlu melakukan update manual dari banyaknya rules pada folder rule_provider. Cukup edit rule_direct.yaml dikarenakan itu customize tiap orang untuk bypass trafficnya. Untuk rule yang lain jika ada tambahan silahkan chat ke grup telegram IPTUNNELS atau open issues pada repository ini.

#### Rule Direct/Bypassed Connection

rule_direct.yaml bersifat offline dimana pengguna dapat mengedit traffic apa saja yang di direct/bypass (tidak menggunakan tunnel). Agar lebih mudah sebagai default sudah disetting bypass traffic Whatsapp.

### Setting Clash For Android

Setelah selesai mengedit config main.yaml dan setiap file pada folder proxy_provider serta rule_direct.yaml pada folder rule_provider maka kita akan setting CFA. Silahkan buka aplikasi clash for android.
<img src="https://raw.githubusercontent.com/malikshi/clash_for_android/main/assets/cfa.jpg" border="0">

##### Import Main.yaml

Jika ada yang perlu diedit silahkan edit main.yaml kemudian import main.yaml.

Video:  [Import Main.yaml](https://youtu.be/ehopTWNQ_xs)

![impormain](assets/import%20main%20yaml.gif)

##### Import Proxy Provider

Jika Semua file pada folder proxy_provider yang terdiri dari umum.yaml, trafficIndo.yaml, streaming.yaml, sosmed.yaml dan gaming.yaml sudah diisi dengan akun maka selanjutnya import file-file tersebut pada Provider Files

Video:  [Import Proxy Provider](https://youtu.be/pUdBvfzAjWo)

![importproxy](assets/import%20proxy%20provider.gif)

##### Import Rule Provider

traffic direct/bypass sudah disikan ke rule_direct.yaml. ada dua cara untuk import seluruh file pada folder rule_provider, pertama hanya import rule_direct.yaml dan saat klik icon save pada profile akan melakukan fetching seluruh rules jadi membutukan koneksi internet. Kedua import seluruh file secara manual.

Video:  [Import Rule Provider](https://youtu.be/OPdKD2FSj-4)

![importrule](assets/import%20rule%20provider.gif)

##### Start Clash For Android

Semua langkah - langkah diatas sudah dijalankan maka tinggal start clash for android dengan memilih profile yang tadi dibuat dan tap START untuk memulai.

Video:  [Start Clash For Android](https://youtu.be/WCpX68RbZl8)