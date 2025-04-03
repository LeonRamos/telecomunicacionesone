

# 📡 **Cómo conectar un ESP32 a una red WiFi**  

Este tutorial te guiará para conectar tu ESP32 a una red WiFi utilizando el entorno Arduino.  

## 🔹 **Material necesario**  
- Placa **ESP32**  
- Cable **micro USB**  
- Entorno de desarrollo **Arduino IDE**  
- Conexión a internet  

---

## 🛠 **Paso 1: Configurar el Entorno**  

### 🔹 **Instalar Arduino IDE**  
Si aún no tienes instalado **Arduino IDE**, descárgalo desde [aquí](https://www.arduino.cc/en/software).  

### 🔹 **Agregar soporte para ESP32 en Arduino IDE**  
1. Abre **Arduino IDE**.  
2. Ve a **Archivo** → **Preferencias**.  
3. En el campo **Gestor de URLs Adicionales para Tarjetas**, agrega:  

   ```
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
4. Pulsa **OK**.  
5. Ve a **Herramientas** → **Placa** → **Gestor de Tarjetas**.  
6. Busca **esp32**, selecciona el paquete de **Espressif Systems** y haz clic en **Instalar**.  

---

## 🔌 **Paso 2: Conectar el ESP32 a la PC**  
1. Usa un **cable micro USB** para conectar tu ESP32 al PC.  
2. Ve a **Herramientas** → **Placa** y selecciona tu modelo de ESP32 (por ejemplo, "ESP32 Dev Module").  
3. Ve a **Herramientas** → **Puerto** y selecciona el puerto al que está conectado el ESP32.  

---

## 📝 **Paso 3: Escribir el Código**  

1. Abre **Arduino IDE** y copia el siguiente código:  

```cpp
#include <WiFi.h>  // Biblioteca para WiFi en ESP32

const char* ssid = "NOMBRE_DE_TU_WIFI";     // Nombre de la red WiFi
const char* password = "CONTRASEÑA_DE_TU_WIFI"; // Contraseña de la red

void setup() {
    Serial.begin(115200);  // Iniciar puerto serie
    WiFi.begin(ssid, password);  // Conectar a la red WiFi
    Serial.print("Conectando a WiFi");

    while (WiFi.status() != WL_CONNECTED) {
        delay(1000);
        Serial.print(".");
    }

    Serial.println("\nConectado a WiFi!");
    Serial.print("Dirección IP: ");
    Serial.println(WiFi.localIP());  // Mostrar IP asignada
}

void loop() {
    // Tu código aquí (si lo necesitas)
}
```

2. **Reemplaza** `"NOMBRE_DE_TU_WIFI"` y `"CONTRASEÑA_DE_TU_WIFI"` con los datos de tu red.  

---

## 🚀 **Paso 4: Subir el Código al ESP32**  
1. Conecta el ESP32 a la PC.  
2. En Arduino IDE, haz clic en el botón **"Subir"** (flecha hacia la derecha).  
3. Espera a que se complete la carga del código.  
4. Si ves un error, mantén presionado el botón **"BOOT"** del ESP32 mientras subes el código.  

---

## 📡 **Paso 5: Verificar la Conexión**  
1. Abre **Monitor Serie** en Arduino IDE (**Herramientas → Monitor Serie**).  
2. Ajusta la velocidad a **115200 baudios**.  
3. Si todo está bien, deberías ver algo como:  

   ```
   Conectando a WiFi...
   Conectado a WiFi!
   Dirección IP: 192.168.1.100
   ```

Ahora tu ESP32 está conectado a la red WiFi y tiene una dirección IP asignada.  

---

