Serie de Fourier con Arduino usando FFT
```markdown
# Implementación de la Serie de Fourier con Arduino usando FFT

En este proyecto se implementa la serie de Fourier utilizando la Transformada Rápida de Fourier (FFT), que es una implementación eficiente de la Transformada Discreta de Fourier (DFT). Se modifican los códigos de un Arduino emisor y receptor, donde el emisor genera una señal compuesta y el receptor la analiza utilizando FFT.

## Código para el Arduino Emisor (Maestro)

```cpp
#include <math.h>

const int outputPin = 2;  // Pin para enviar la señal
const int buttonPin = 4;  // Pin para el botón

void setup() {
  pinMode(outputPin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  if (digitalRead(buttonPin) == LOW) {
    // Generar una señal compuesta
    for (int i = 0; i < 128; i++) {
      // Crear una señal con dos frecuencias
      float signal = sin(2 * PI * i / 8) + 0.5 * sin(2 * PI * i / 4);
      int outputValue = map(signal, -1.5, 1.5, 0, 255);
      analogWrite(outputPin, outputValue);
      delayMicroseconds(1000); // 1kHz de frecuencia de muestreo
    }
    Serial.println("Señal enviada");
    delay(1000);
  }
}
```

## Código para el Arduino Receptor (Esclavo)

```cpp
#include "arduinoFFT.h"

#define SAMPLES 128
#define SAMPLING_FREQUENCY 1000 // Hz

arduinoFFT FFT = arduinoFFT();

const int inputPin = A0;  // Pin para recibir la señal

double vReal[SAMPLES];
double vImag[SAMPLES];

void setup() {
  Serial.begin(115200);
}

void loop() {
  // Muestrear la señal
  for (int i = 0; i < SAMPLES; i++) {
    vReal[i] = analogRead(inputPin);
    vImag[i] = 0;
    delayMicroseconds(1000000/SAMPLING_FREQUENCY);
  }

  // Realizar FFT
  FFT.Windowing(vReal, SAMPLES, FFT_WIN_TYP_HAMMING, FFT_FORWARD);
  FFT.Compute(vReal, vImag, SAMPLES, FFT_FORWARD);
  FFT.ComplexToMagnitude(vReal, vImag, SAMPLES);

  // Encontrar la frecuencia dominante
  double peak = 0;
  int peakIndex = 0;
  for (int i = 1; i < (SAMPLES/2); i++) {
    if (vReal[i] > peak) {
      peak = vReal[i];
      peakIndex = i;
    }
  }

  double dominantFreq = (peakIndex * 1.0 * SAMPLING_FREQUENCY) / SAMPLES;

  Serial.print("Frecuencia dominante: ");
  Serial.print(dominantFreq);
  Serial.println(" Hz");

  delay(2000);
}
```

## Explicación del funcionamiento

1. **Arduino Emisor (Maestro)**:
   - Genera una señal compuesta de dos frecuencias diferentes usando la función seno.
   - La señal se envía a través del pin de salida cuando se presiona el botón.

2. **Arduino Receptor (Esclavo)**:
   - Utiliza la biblioteca arduinoFFT para realizar el análisis de Fourier.
   - Muestrea la señal de entrada 128 veces.
   - Aplica la FFT a las muestras recolectadas.
   - Calcula la magnitud del espectro de frecuencia.
   - Encuentra y muestra la frecuencia dominante en la señal.

Este sistema permite generar una señal compuesta en el emisor y analizarla en el receptor utilizando la Transformada Rápida de Fourier. El receptor podrá identificar las frecuencias principales presentes en la señal enviada por el emisor.

## Instalación de la Biblioteca `arduinoFFT`

Para implementar este sistema, asegúrate de instalar la biblioteca `arduinoFFT` a través del Gestor de Bibliotecas de Arduino. 

Conecta el pin de salida del emisor al pin analógico A0 del receptor para la transmisión de la señal.

Este enfoque proporciona una demostración práctica de cómo se puede utilizar la serie de Fourier (implementada como FFT) para analizar señales digitales en un sistema Arduino, lo cual es útil en aplicaciones de procesamiento de señales y análisis de frecuencia.

## Citations

- [Fast Fourier Transform (FFT) on Arduino](https://www.tutorialspoint.com/fast-fourier-transform-fft-on-arduino)
- [EasyFFT: Fast Fourier Transform for Arduino](https://www.hackster.io/abhilashpatel121/easyfft-fast-fourier-transform-fft-for-arduino-9d2677)
- [Arduino Forum: FFT Programming for Voltage Signal](https://forum.arduino.cc/t/programming-for-finding-fft-of-a-voltage-signal/299937)
- [FFTA: Fast Fourier Transform for Arduino](https://github.com/MartinStokroos/FFTA)
- [Norwegian Creations: What is FFT and How Can You Implement It on an Arduino?](https://www.norwegiancreations.com/2017/08/what-is-fft-and-how-can-you-implement-it-on-an-arduino/)
```

