#include <WiFi.h>
#include <WebServer.h>

// Replace with your desired AP credentials
const char* ssid = "ESP32_AP";
const char* password = "12345678";

// Web server running on port 80
WebServer server(80);

// LED Control
const int ledPin = 35;
bool ledState = false;

// Ultrasonic Sensor Pins
const int trigPin = 5;
const int echoPin = 18;

// Function to get distance from ultrasonic sensor
long getDistance() {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    long duration = pulseIn(echoPin, HIGH);
    long distance = duration * 0.034 / 2; // Convert to cm
    return distance;
}

void setup() {
    pinMode(ledPin, OUTPUT);
    digitalWrite(ledPin, LOW);

    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);

    Serial.begin(115200);

    WiFi.softAP(ssid, password);
    Serial.println("Access Point started");
    Serial.print("AP IP address: ");
    Serial.println(WiFi.softAPIP());

    server.on("/", handleRoot);
    server.on("/toggle", handleToggle);
    server.on("/distance", handleDistance);
    
    server.begin();
    Serial.println("Web server started");
}

void loop() {
    server.handleClient();
}

// Serve HTML page
void handleRoot() {
    String html = "<!DOCTYPE html>"
                  "<html>"
                  "<head><title>ESP32 LED & Ultrasonic Sensor</title></head>"
                  "<body>"
                  "<h1>ESP32 LED Control & Ultrasonic Sensor</h1>"
                  "<button onclick=\"toggleLED()\">Toggle LED</button>"
                  "<p>Ultrasonic Sensor Distance: <span id='distance'>--</span> cm</p>"
                  "<script>"
                  "function toggleLED() { fetch('/toggle'); }"
                  "function updateDistance() {"
                  " fetch('/distance')"
                  " .then(response => response.text())"
                  " .then(data => { document.getElementById('distance').innerText = data; });"
                  "}"
                  "setInterval(updateDistance, 1000);"
                  "</script>"
                  "</body>"
                  "</html>";
    server.send(200, "text/html", html);
}

// Toggle LED function
void handleToggle() {
    ledState = !ledState;
    digitalWrite(ledPin, ledState ? HIGH : LOW);
    server.send(200, "text/plain", ledState ? "LED ON" : "LED OFF");
}

// Get distance from ultrasonic sensor
void handleDistance() {
    long distance = getDistance();
    server.send(200, "text/plain", String(distance));
}
