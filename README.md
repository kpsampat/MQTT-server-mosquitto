# MQTT-server-mosquitto
MQTT server setup mosquitto


https://www.ev3dev.org/docs/tutorials/sending-and-receiving-messages-with-mqtt/



# Install MQTT mosquitto : 
``` sudo apt-get install mosquitto ```

```
kishan@dev:~# systemctl status mosquitto
● mosquitto.service - LSB: mosquitto MQTT v3.1 message broker
   Loaded: loaded (/etc/init.d/mosquitto)
   Active: active (running) since Wed 2016-05-11 07:40:51 WEST; 7min ago
   CGroup: /system.slice/mosquitto.service
           └─685 /usr/sbin/mosquitto -c /etc/mosquitto/mosquitto.conf
```
