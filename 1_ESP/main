#include <WiFi.h>
#include <DHT.h>
#include "SinricPro.h"
#include "SinricProTemperaturesensor.h"
#include "SinricProCustomDevice.h"

// ===== CONFIGURAÇÕES WIFI E SINRIC PRO =====
#define WIFI_SSID         "nome_rede"
#define WIFI_PASS         "senha_rede"
#define APP_KEY           "chave_app"
#define APP_SECRET        "segredo_app"

#define TEMP_SENSOR_ID    "temp_id"
#define LIGHT_SENSOR_ID   "light_id"
#define RAIN_SENSOR_ID    "rain_id"

// ===== DHT22 =====
#define DHTPIN 4
#define DHTTYPE DHT22
DHT dht(DHTPIN, DHTTYPE);

// ===== LDR =====
#define LDR_PIN 32

// ===== Sensor HW-103 =====
#define RAIN_DIGITAL 27
#define RAIN_ANALOG 34

// Variáveis de controle de tempo
unsigned long lastMillis = 0;
const unsigned long interval = 10000; // Envia dados a cada 10 segundos

void setup() {
  Serial.begin(115200);

  // Inicializa DHT
  dht.begin();
  pinMode(RAIN_DIGITAL, INPUT);

  // Conecta ao WiFi
  WiFi.begin(WIFI_SSID, WIFI_PASS);
  Serial.print("Conectando ao WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi Conectado!");

  // Configura o Sinric Pro
  SinricProTemperaturesensor &tempSensor = SinricPro[TEMP_SENSOR_ID];
  SinricProTemperaturesensor &lightSensor = SinricPro[LIGHT_SENSOR_ID];
  SinricPro.begin(APP_KEY, APP_SECRET);
}

void loop() {
  // Mantém a conexão com o Sinric Pro ativa
  SinricPro.handle();

  // Executa a leitura e envio a cada 'interval' milissegundos
  if (millis() - lastMillis >= interval) {
    lastMillis = millis();

    //Leitura dos sensores
    float tempDHT = dht.readTemperature();
    float umi = dht.readHumidity();
    int light = analogRead(LDR_PIN);
    int rainAnalog = map(analogRead(RAIN_ANALOG), 0, 4095, 0, 100);
    int rainDigital = digitalRead(RAIN_DIGITAL);

    //Verifica se a leitura do DHT é válida
    if (isnan(tempDHT) || isnan(umi)) {
      Serial.println("Erro ao ler o DHT22!");
    } else {
      //Envia temperatura e umidade para o Sinric Pro
      SinricProTemperaturesensor &tempSensor = SinricPro[TEMP_SENSOR_ID];
      SinricProTemperaturesensor &lightSensor = SinricPro[LIGHT_SENSOR_ID];
      SinricProCustomDevice &rainSensor = SinricPro.put<SinricProCustomDevice>(RAIN_SENSOR_ID);
      bool success = tempSensor.sendTemperatureEvent(tempDHT, umi);
      if (success) {
        Serial.println("Dados enviados para o Sinric Pro com sucesso!");
      }
      success = lightSensor.sendTemperatureEvent(light, -1);
      if (success) {
        Serial.println("Dados enviados para o Sinric Pro com sucesso!");
      }
      success = rainSensor.sendRangeValueEvent("rangeInstance1", rainAnalog);
    }

    //Monitor Serial
    Serial.println("===== LEITURA SENSORES =====");
    Serial.printf("Temp: %.2f °C | Umidade: %.2f %%\n", tempDHT, umi);
    Serial.printf("Luz (LDR): %d\n", light);
    Serial.printf("Chuva: %s (Analog: %d)\n", (rainDigital == LOW ? "CHOVENDO" : "SECO"), rainAnalog);
    Serial.println("================================\n");
  }
}
