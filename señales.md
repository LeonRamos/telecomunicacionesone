Sistema Diagnóstico:

```markdown
# Sistema de Diagnóstico Automotriz con Arduino y Compuerta NAND

Este proyecto implementa un sistema de diagnóstico simplificado utilizando la tabla de verdad de una compuerta NAND entre un Arduino maestro (emisor) y un Arduino esclavo (receptor). A continuación, se muestra el código y la explicación del funcionamiento del sistema.

## Código para el Arduino Emisor (Maestro)

```cpp
const int outputPin1 = 2;  // Pin para enviar la señal A
const int outputPin2 = 3;  // Pin para enviar la señal B
const int buttonPin = 4;   // Pin para el botón

void setup() {
  pinMode(outputPin1, OUTPUT);
  pinMode(outputPin2, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    // Simular todas las combinaciones de entrada NAND
    for (int i = 0; i < 4; i++) {
      int a = (i >> 1) & 1;
      int b = i & 1;
      
      digitalWrite(outputPin1, a);
      digitalWrite(outputPin2, b);
      
      Serial.print("Enviando: A=");
      Serial.print(a);
      Serial.print(", B=");
      Serial.println(b);
      
      delay(1000);  // Esperar 1 segundo entre cada combinación
    }
    Serial.println("Ciclo completo");
    delay(2000);  // Esperar 2 segundos antes de permitir un nuevo ciclo
  }
}
```

## Código para el Arduino Receptor (Esclavo)

```cpp
const int inputPin1 = 2;  // Pin para recibir la señal A
const int inputPin2 = 3;  // Pin para recibir la señal B
const int outputLED = 13; // LED para mostrar el resultado NAND

void setup() {
  pinMode(inputPin1, INPUT);
  pinMode(inputPin2, INPUT);
  pinMode(outputLED, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int a = digitalRead(inputPin1);
  int b = digitalRead(inputPin2);
  
  // Implementar lógica NAND
  int result = !(a && b);
  
  digitalWrite(outputLED, result);
  
  Serial.print("Recibido: A=");
  Serial.print(a);
  Serial.print(", B=");
  Serial.print(b);
  Serial.print(" | Resultado NAND: ");
  Serial.println(result);
  
  delay(100);  // Pequeña pausa para estabilidad
}
```

## Explicación del funcionamiento

1. **Arduino Emisor (Maestro)**:
   - Utiliza dos pines de salida para simular las entradas A y B de una compuerta NAND.
   - Al presionar el botón, genera todas las combinaciones posibles de A y B (00, 01, 10, 11).
   - Envía cada combinación secuencialmente, esperando 1 segundo entre cada una.

2. **Arduino Receptor (Esclavo)**:
   - Lee continuamente los estados de los pines de entrada A y B.
   - Implementa la lógica NAND: resultado = !(A && B).
   - Muestra el resultado en un LED (encendido para 1, apagado para 0).
   - Imprime los valores recibidos y el resultado en el monitor serial.

Este sistema simula un diagnóstico de automóvil simplificado, donde el maestro envía diferentes combinaciones de señales (como si fueran sensores) y el esclavo las procesa utilizando la lógica NAND. En un escenario real de diagnóstico automotriz, podrías expandir este concepto para incluir múltiples señales y lógicas más complejas basadas en las especificaciones del vehículo.

## Conexiones

- Conecta el pin 2 del Arduino emisor al pin 2 del Arduino receptor (señal A).
- Conecta el pin 3 del Arduino emisor al pin 3 del Arduino receptor (señal B).
- Conecta las tierras (GND) de ambos Arduinos.
- En el Arduino emisor, conecta un botón entre el pin 4 y GND.
- En el Arduino receptor, conecta un LED con su resistencia apropiada al pin 13.

Este sistema te permitirá observar cómo se comporta una compuerta NAND en todas sus combinaciones posibles, simulando un proceso de diagnóstico simple. Puedes expandir este concepto para incluir más compuertas lógicas o condiciones más complejas según las necesidades específicas del diagnóstico automotriz que desees implementar.

## Citations

- [Identification of Basic Logic Gate ICs Using Arduino](https://projecthub.arduino.cc/shreyas_arbatti/identification-of-basic-logic-gate-ics-using-arduino-48e659)
- [How to create digital gates on Arduino](https://forum.arduino.cc/t/how-to-create-digital-gates-on-arduino/54250)
- [Logic gates using Arduino Uno](https://www.auraauro.com/uncategorized/logic-gates-using-arduino-uno/)
- [DroneBot Workshop: Basic Logic](https://dronebotworkshop.com/basic-logic/)
- [NAND gate logic using Arduino](https://forum.arduino.cc/t/nand-logic-gate-ics-arduino/19779)
- [Arduino implementation of logic gates](https://www.researchgate.net/publication/322159080_Digital_Logic_Gate_Simulation_using_Arduino_Microcontroller)
```


