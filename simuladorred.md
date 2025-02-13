

```
# Simulación de transmisión de datos digital con Arduino Uno

## Objetivo
Crear un sistema simple de transmisión de datos digital que simule el envío de paquetes de información entre dos dispositivos, utilizando principios básicos de redes y sistemas digitales.

## Materiales
- 2 placas Arduino Uno
- 4 LEDs (2 rojos, 2 verdes)
- 4 resistencias de 220 ohms
- 2 pulsadores
- Cables de conexión
- Protoboard

## Configuración del circuito

1. En cada Arduino Uno:
   - Conecta un LED rojo al pin digital 2 (indicador de transmisión)
   - Conecta un LED verde al pin digital 3 (indicador de recepción)
   - Conecta un pulsador al pin digital 4 (para iniciar la transmisión)
   - Conecta el pin digital 5 de un Arduino al pin digital 6 del otro (línea de datos)

2. Conecta las tierras (GND) de ambos Arduino Uno.

## Código

### Arduino transmisor

```cpp
const int transmitLED = 2;
const int receiveLED = 3;
const int buttonPin = 4;
const int dataPin = 5;

void setup() {
  pinMode(transmitLED, OUTPUT);
  pinMode(receiveLED, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(dataPin, OUTPUT);
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    sendData();
  }
}

void sendData() {
  digitalWrite(transmitLED, HIGH);
  
  // Simula el envío de un paquete de 8 bits
  for (int i = 0; i < 8; i++) {
    digitalWrite(dataPin, random(2)); // Envía 0 o 1 aleatoriamente
    delay(100);
  }
  
  digitalWrite(transmitLED, LOW);
  delay(500);
}
```

### Arduino receptor

```cpp
const int transmitLED = 2;
const int receiveLED = 3;
const int dataPin = 6;

void setup() {
  pinMode(transmitLED, OUTPUT);
  pinMode(receiveLED, OUTPUT);
  pinMode(dataPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  if (digitalRead(dataPin) == HIGH) {
    receiveData();
  }
}

void receiveData() {
  digitalWrite(receiveLED, HIGH);
  
  String receivedBits = "";
  
  // Recibe 8 bits
  for (int i = 0; i < 8; i++) {
    receivedBits += digitalRead(dataPin);
    delay(100);
  }
  
  Serial.println("Datos recibidos: " + receivedBits);
  digitalWrite(receiveLED, LOW);
  delay(500);
}
```

## Explicación

Esta práctica simula la transmisión de datos digitales en una red simple[1][5]. Cuando se presiona el botón en el Arduino transmisor, se envía una secuencia de 8 bits aleatorios al receptor[12]. El LED rojo se enciende durante la transmisión, mientras que el LED verde del receptor se ilumina al recibir datos[10].

Este ejercicio ilustra varios conceptos fundamentales de las redes y sistemas digitales:

1. **Señalización digital**: Los datos se transmiten como una serie de 1s y 0s, representando la naturaleza binaria de la comunicación digital[9].
2. **Sincronización**: Ambos dispositivos operan con el mismo intervalo de tiempo (100ms) para asegurar una transmisión correcta[13].
3. **Detección de señal**: El receptor constantemente monitorea la línea de datos para detectar el inicio de una transmisión[11].
4. **Paquetes de datos**: La transmisión de 8 bits simula un paquete de datos básico, similar a cómo se envía la información en redes reales[3].
5. **Indicadores visuales**: Los LEDs proporcionan retroalimentación sobre el estado de la comunicación, similar a los indicadores en equipos de red[7].


```

Puedes copiar y pegar esto en un archivo `.md` para usarlo en tu repositorio de GitHub. ¡Espero que te sea útil!
