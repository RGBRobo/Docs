# Messung Erstellen

Wenn eine Messung erstellt werden soll, so muss man zuerst das Topic "/new/callback" abonnieren, da dort die ID zurückgeliefert wird.
Danach muss auf das Topic "/new" eine Nachricht gepublisht werden.

## Code Beispiele

<deflist collapsible="true">
    <def title="ID Anfordern" default-state="collapsed">
        <tabs>
    <tab title="Java" >
        <code-block lang="java"><![CDATA[
            import org.eclipse.paho.client.mqttv3.MqttClient;
import org.eclipse.paho.client.mqttv3.MqttException;
import org.eclipse.paho.client.mqttv3.MqttMessage;
import org.eclipse.paho.client.mqttv3.persist.MemoryPersistence;

public class MqttPublisher {
    public static void main(String[] args) {
        String broker = "tcp://broker-address:1883";
        String clientId = "RGBRobo";
        String topic = "/new";
        String content = " "; // Content can be Empty in this Topic
        int qos = 2;
        MemoryPersistence persistence = new MemoryPersistence();
        try {
            MqttClient mqttClient = new MqttClient(broker, clientId, persistence);
            mqttClient.connect();
            MqttMessage message = new MqttMessage(content.getBytes());
            message.setQos(qos);
            mqttClient.publish(topic, message);
            mqttClient.disconnect();
        } catch (MqttException me) {
            me.printStackTrace();
        }
    }
}]]></code-block>
</tab>
<tab title="Python">
<code-block lang="python">
<![CDATA[
import paho.mqtt.client as mqtt
# Define the broker address and port
broker = "broker-address"
port = 1883
topic = "/new"
message = " "
# Create a client instance
client = mqtt.Client("RGBRobo")
# Connect to the broker
client.connect(broker, port)
# Publish the message to the specified topic
client.publish(topic, message)

# Disconnect from the broker

client.disconnect()]]></code-block>
</tab>
</tabs>
    </def>
    <def title="Callback" default-state="collapsed">
        <tabs>
    <tab title="Java">
        <code-block lang="java"><![CDATA[
            import org.eclipse.paho.client.mqttv3.IMqttDeliveryToken;
import org.eclipse.paho.client.mqttv3.MqttCallback;
import org.eclipse.paho.client.mqttv3.MqttClient;
import org.eclipse.paho.client.mqttv3.MqttException;
import org.eclipse.paho.client.mqttv3.MqttMessage;
import org.eclipse.paho.client.mqttv3.persist.MemoryPersistence;

public class MqttSubscriber {
    public static void main(String[] args) {
        String broker = "tcp://broker-address:1883";
        String clientId = "RGBRobo";
        String topic = "/new/callback";
        
        MemoryPersistence persistence = new MemoryPersistence();
        
        try {
            MqttClient mqttClient = new MqttClient(broker, clientId, persistence);
            
            mqttClient.setCallback(new MqttCallback() {
                @Override
                public void connectionLost(Throwable cause) {
                    System.out.println("Connection lost: " + cause.getMessage());
                }
                
                @Override
                public void messageArrived(String topic, MqttMessage message) throws Exception {
                    System.out.println("Message received on topic " + topic + ": " + new String(message.getPayload()));
                }
                
                @Override
                public void deliveryComplete(IMqttDeliveryToken token) {
                    // Not used for subscribing
                }
            });
            
            mqttClient.connect();
            mqttClient.subscribe(topic);
        } catch (MqttException me) {
            me.printStackTrace();
        }
    }

}
]]></code-block>
</tab>
<tab title="Python">
<code-block lang="python">
<![CDATA[
import paho.mqtt.client as mqtt

# Define the broker address and port

broker = "broker-address"
port = 1883
topic = "/new/callback"

# Callback function for when the client connects to the broker

def on_connect(client, userdata, flags, rc):
if rc == 0:
print("Connected successfully")
client.subscribe(topic)
else:
print("Connection failed with code", rc)

# Callback function for when a message is received

def on_message(client, userdata, msg):
print(f"Message received on topic {msg.topic}: {msg.payload.decode()}")

# Create a client instance

client = mqtt.Client("PythonSampleSubscriber")

# Assign callback functions

client.on_connect = on_connect
client.on_message = on_message

# Connect to the broker

client.connect(broker, port)

# Start the network loop

client.loop_forever()
]]></code-block>
</tab>
</tabs>
    </def>
</deflist>


