# Arduino Uno Tester RJ45

## Objetivo de la Práctica:
El objetivo de esta práctica es diseñar y construir un probador de cables RJ45 que permita verificar la continuidad y el orden correcto de los cables en un conector RJ45. Este proyecto es ideal para estudiantes de electrónica y telecomunicaciones que buscan comprender cómo funcionan los cables de red y cómo se pueden probar.

## Componentes Utilizados:
- **Arduino Uno**: Placa de desarrollo que actúa como el cerebro del sistema, controlando el flujo de señales a través de los cables.
- **Conectores RJ45**: Utilizados para conectar los cables de red que se van a probar.
- **LEDs**: Indican si cada cable está conectado correctamente y si hay continuidad.
- **Resistencias de 220 ohmios**: Limitan la corriente que pasa a través de los LEDs para evitar que se quemen.
- **Interruptor**: Permite seleccionar entre cables cruzados y rectos.
- **Cables de conexión**: Conectan los componentes entre sí.

## Principal Funcionamiento:
1. **Conexión de los Cables**: El cable RJ45 se conecta entre los dos conectores RJ45 en la protoboard.
2. **Secuencia de LEDs**: Arduino envía una señal de alta (5V) a cada cable del conector RJ45 durante un segundo, y luego la baja. Si todo está bien, los LEDs se encienden uno tras otro.
3. **Detección de Fallos**: Si un cable está roto, el LED correspondiente no se encenderá. Si hay un cable cruzado, los LEDs se encenderán en un orden diferente al esperado.

## Paso a Paso:

### 1. Configuración del Circuito

1. **Conecta los Conectores RJ45**: Conecta los dos conectores RJ45 a la protoboard. Cada pin del conector RJ45 debe estar conectado a un LED a través de una resistencia de 220 ohmios.

2. **Conecta los LEDs**: Cada LED debe estar conectado a un pin digital de Arduino. Por ejemplo, puedes usar los pines digitales 2 a 9.

3. **Conecta el Interruptor**: Conecta el interruptor entre dos pines digitales de Arduino (por ejemplo, pines 10 y 11). Este interruptor permitirá seleccionar entre cables cruzados y rectos.

### 2. Código de Arduino

Aquí tienes un ejemplo básico de código para probar la continuidad de los cables:

```cpp
// Definir los pines para los LEDs
const int ledPins[] = {2, 3, 4, 5, 6, 7, 8, 9};

// Definir los pines para el interruptor
const int switchPin1 = 10;
const int switchPin2 = 11;

void setup() {
  // Inicializar los pines de los LEDs como salidas
  for (int i = 0; i < 8; i++) {
    pinMode(ledPins[i], OUTPUT);
  }

  // Inicializar los pines del interruptor como entradas
  pinMode(switchPin1, INPUT);
  pinMode(switchPin2, INPUT);
}

void loop() {
  // Leer el estado del interruptor
  int switchState = digitalRead(switchPin1);

  // Probar la continuidad de los cables
  if (switchState == HIGH) {
    // Modo cruzado
    testCrossoverCable();
  } else {
    // Modo recto
    testStraightCable();
  }

  delay(1000); // Esperar un segundo antes de probar de nuevo
}

void testStraightCable() {
  for (int i = 0; i < 8; i++) {
    digitalWrite(ledPins[i], HIGH); // Encender el LED correspondiente
    delay(500); // Esperar medio segundo
    digitalWrite(ledPins[i], LOW); // Apagar el LED
    delay(500); // Esperar medio segundo
  }
}

void testCrossoverCable() {
  // Esquema de cable cruzado: 1-3, 2-6, 3-1, 4-4, 5-5, 6-2, 7-7, 8-8
  int crossoverPins[] = {2, 6, 1, 4, 5, 3, 7, 8};
  for (int i = 0; i < 8; i++) {
    digitalWrite(ledPins[crossoverPins[i] - 1], HIGH); // Encender el LED correspondiente
    delay(500); // Esperar medio segundo
    digitalWrite(ledPins[crossoverPins[i] - 1], LOW); // Apagar el LED
    delay(500); // Esperar medio segundo
  }
}
```

### 3. Probar el Circuito

1. **Conecta un Cable RJ45**: Conecta un cable RJ45 entre los dos conectores RJ45 en la protoboard.
2. **Enciende el Arduino**: Enciende el Arduino y observa los LEDs. Si todos los LEDs se encienden en el orden correcto, el cable está bien conectado.
3. **Usa el Interruptor**: Usa el interruptor para cambiar entre el modo recto y cruzado.

