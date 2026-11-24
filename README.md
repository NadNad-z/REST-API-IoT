# REST API IoT

**Nama :** Yulia Nada Zahrah
**NPM :** 2410020111
**Kelas :** 5A SI Reg BJB

---

## Deskripsi
Proyek IoT sederhana yang mensimulasikan sensor ESP32 (suhu dan kelembaban), mengirim datanya lewat MQTT ke Node-RED, menyimpannya di SQLite, lalu menampilkannya di dashboard web secara real-time menggunakan REST API dan WebSocket.

## Fitur
- Simulasi sensor ESP32 (suhu dan kelembaban, dikirim tiap 3 detik)
- Penerimaan data lewat MQTT (Mosquitto)
- Penyimpanan riwayat data ke database SQLite
- REST API dengan autentikasi API Key
- Dashboard real-time lewat WebSocket (polling REST sebagai cadangan)
- Grafik suhu dan kelembaban (Chart.js) dan tabel 10 data terakhir
- Batas suhu (threshold) yang bisa diubah, dengan peringatan saat terlampaui
- Kontrol perangkat (lampu ON/OFF)

## Arsitektur
```
simulasi_esp32.py --MQTT--> Mosquitto --> Node-RED --> SQLite (iot.db)
                                             |
                                  REST API + WebSocket
                                             |
                                      dashboard.html
```

## Isi Repository
| File | Fungsi |
|---|---|
| `simulasi_esp32.py` | Simulator sensor ESP32 (publish data ke MQTT) |
| `flows.json` | Flow Node-RED (MQTT, REST API, WebSocket, SQLite) |
| `dashboard.html` | Tampilan dashboard web |

## Kebutuhan
- Node.js dan Node-RED (dengan node `node-red-node-sqlite`)
- Mosquitto MQTT Broker (port 1883)
- Python 3 dan library `paho-mqtt` (`pip install paho-mqtt`)

## Cara Menjalankan
1. Jalankan **Mosquitto** (broker MQTT, port 1883).
2. Jalankan **Node-RED**, lalu impor `flows.json` (menu ☰ → Import) dan klik **Deploy**.
3. Letakkan `dashboard.html` di folder `httpStatic` Node-RED.
4. Sesuaikan path database SQLite (`C:/iot-rest-api/iot.db`) dengan lokasi di komputer kamu.
5. Jalankan simulator:
   ```
   py simulasi_esp32.py
   ```
6. Buka dashboard di `http://localhost:1880/dashboard.html`.

## Catatan
- API Key (`iot-kampus-2026`) hanya untuk keperluan simulasi. Pada sistem sebenarnya, key tidak boleh ditaruh di sisi client, melainkan disimpan di server atau memakai autentikasi login/token.

## Tampilan
![Dashboard]("<img width="640" height="303" alt="tampilan" src="https://github.com/user-attachments/assets/8342b64a-dd91-4e96-80c5-0596961600fd" />
")
![Flow Node-RED](<img width="460" height="279" alt="flow" src="<img width="460" height="279" alt="flow" src="https://github.com/user-attachments/assets/48809523-1cfb-4fec-9829-98f34a570359" />
" />
)
