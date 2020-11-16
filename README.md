# MQTT-server-mosquitto
MQTT server setup mosquitto


https://www.ev3dev.org/docs/tutorials/sending-and-receiving-messages-with-mqtt/



# Install MQTT mosquitto : 

``` sudo apt-get update ```
``` sudo apt-get install mosquitto ```


We need a broker that is always available. Just one for the whole network. It can be a PC, a Raspberry Pi or even an EV3. If it is a Debian-based linux system we can use mosquitto

```
azureuser@orbit:~$ systemctl status mosquitto
● mosquitto.service - LSB: mosquitto MQTT v3.1 message broker
   Loaded: loaded (/etc/init.d/mosquitto; generated)
   Active: active (exited) since Mon 2020-11-16 06:36:22 UTC; 4h 56min ago
     Docs: man:systemd-sysv-generator(8)

Nov 16 06:36:22 orbit systemd[1]: Starting LSB: mosquitto MQTT v3.1 message broker...
Nov 16 06:36:22 orbit mosquitto[12430]:  * Starting network daemon: mosquitto
Nov 16 06:36:22 orbit mosquitto[12430]:    ...done.
Nov 16 06:36:22 orbit systemd[1]: Started LSB: mosquitto MQTT v3.1 message broker.

```

Now we are able to send and receive messages through the broker (by default mosquitto uses port 1883).

``` sudo apt-get install python3-pip ```

``` sudo pip3 install paho-mqtt ``` 

Publisher Code :

``` 
#!/usr/bin/env python3

import paho.mqtt.client as mqtt

# This is the Publisher

client = mqtt.Client()
client.connect("localhost",1883,60)
client.publish("topic/test", "Hello world!");
client.disconnect();
```

Subscriber Code :

```

#!/usr/bin/env python3

import paho.mqtt.client as mqtt

# This is the Subscriber

def on_connect(client, userdata, flags, rc):
  print("Connected with result code "+str(rc))
  client.subscribe("topic/test")

def on_message(client, userdata, msg):
    print("Yes!")
    print(msg.payload.decode())
    client.disconnect()
    
while True:
   client = mqtt.Client()
   client.connect("THE_IP_ADDRESS_OF_OUR_BROKER",1883,60)  #THE_IP_ADDRESS_OF_OUR_BROKER == Server IP Public IP of VM

   client.on_connect = on_connect
   client.on_message = on_message

   client.loop_forever()
```
To run the broker ::

hit this in your terminal :

``` mosquitto -v ```

or 

``` mosquitto -p 1883 ```

Open the ports on VM:

``` sudo ufw enable

sudo ufw allow 22
sudo ufw allow 1883/tcp
```

also open 1883/tcp from networking section of VM in inbound and outbound ports


