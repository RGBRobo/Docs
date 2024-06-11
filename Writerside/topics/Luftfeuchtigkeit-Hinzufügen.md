# Luftfeuchtigkeit Hinzufügen

Um die Luftfeuchtigkeit einfügen zu können, muss zuerst eine Messung erstellt werden.

## Übergabewerte

Die Tabelle unten listet alle Parameter auf, die von der API unterstützt werden.
Dabei bestimmt der "Erforderlich-Parameter", ob es zwingend ist diesen anzugeben.

| Feld     | Erforderlich | Format        |
|----------|--------------|---------------|
| id       | ja           | UUID (String) |
| humidity | ja           | double        |

## Code Beispiele

<tabs>
<tab title="Java" >
<code-block lang="java"><![CDATA[
import org.eclipse.paho.client.mqttv3.MqttClient;
import org.eclipse.paho.client.mqttv3.MqttException;
import org.eclipse.paho.client.mqttv3.MqttMessage;
import org.eclipse.paho.client.mqttv3.persist.MemoryPersistence;
import org.json.JSONObject;

public class MqttPublisher {
public static void main(String[] args) {
String broker = "tcp://broker-address:1883";
String clientId = "RGBRobo";
String topic = "/humidity";
String id = "messungID";    // Die Vorher gespeicherte ID
double humidity = 40.5d; // Temperatur als Double

        MemoryPersistence persistence = new MemoryPersistence();

        try {
            MqttClient mqttClient = new MqttClient(broker, clientId, persistence);
            mqttClient.connect();
            JSONObject jsonPayload = new JSONObject();
            jsonPayload.put("id", id);
            jsonPayload.put("humidity", humidity);
            MqttMessage message = new MqttMessage(jsonPayload.toString().getBytes());
            message.setQos(2);
            mqttClient.publish(topic, message);
            mqttClient.disconnect();
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
import json

# Define the broker address and port
broker = "broker-address"
port = 1883
topic = "/humidity"

# Example data
id = "messungID"    # Vorher gespeicherte ID
humidity = 40.5      # Farbwert als Hex-Wert

# Create a JSON payload
payload = json.dumps({"id": id, "humidity": humidity})

# Create a client instance
client = mqtt.Client("RGBRobo")

# Connect to the broker
client.connect(broker, port)

# Publish the message to the specified topic
client.publish(topic, payload, qos=2)

# Disconnect from the broker
client.disconnect()
]]></code-block>
</tab>
</tabs>