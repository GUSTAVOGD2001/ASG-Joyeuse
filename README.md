# ASG-Joyeuse

## Broker MQTT
- Puerto 1883: ESP32 y clientes TCP
- Puerto 9001: Panel web (WebSocket)
- Topic de estado: vfd/status (ESP32 publica)
- Topic de comandos: vfd/cmd (panel publica)

### Secretos requeridos en GitHub Actions
| Secret | Descripción |
|---|---|
| VPS_HOST | IP pública del VPS |
| VPS_USER | Usuario SSH (root o similar) |
| VPS_SSH_KEY | Llave privada SSH |

### Setup inicial en el VPS (solo una vez)
```bash
sudo apt install -y docker.io docker-compose-plugin
cd ~/ASG-Joyeuse
docker compose up -d
```

### Puertos a abrir en el firewall
```bash
sudo ufw allow 1883
sudo ufw allow 9001
```

### Probar conexión
```bash
# Suscribirse
mosquitto_sub -h TU_IP_VPS -p 1883 -t "vfd/#" -v

# Simular ESP32
mosquitto_pub -h TU_IP_VPS -p 1883 -t "vfd/status" \\
  -m '{"estado":"corriendo","freq_out":28.4,"corriente":4.2}'
```
