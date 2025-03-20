

## 3.1 Técnicas de Modulación Analógica

### 3.1.1 Modulación en Amplitud (AM) y Modulación en Frecuencia (FM)

**Modulación en Amplitud (AM):**
La modulación de amplitud es un método de modulación analógica que consiste en variar la amplitud de una onda portadora según la señal moduladora. Esta técnica es sencilla de implementar y se utiliza comúnmente en transmisiones de radio AM. La modulación AM produce un espectro que incluye la portadora original y dos bandas laterales, superior e inferior, que contienen información idéntica[1][2].

**Modulación en Frecuencia (FM):**
La modulación de frecuencia varía la frecuencia de la onda portadora en función de la señal moduladora. A diferencia de la AM, la FM es menos susceptible a la interferencia de ruido y se utiliza en aplicaciones como la radio FM y sistemas de comunicación inalámbrica. La frecuencia instantánea de la señal modulada es proporcional al valor instantáneo de la señal moduladora[2].

## 3.2 Técnicas de Modulación Digital

### 3.2.1 Modulación por Desplazamiento de Amplitud (ASK), Modulación por Desplazamiento de Frecuencia (FSK), Modulación por Desplazamiento de Fase (PSK) y Modulación de Amplitud en Cuadratura (QAM)

- **Modulación por Desplazamiento de Amplitud (ASK):** En ASK, los dos valores binarios de los datos de entrada se representan mediante dos diferentes amplitudes de la frecuencia portadora. Se utiliza comúnmente en transmisiones por fibra óptica con tecnología LED[5].
  
- **Modulación por Desplazamiento de Frecuencia (FSK):** FSK varía la frecuencia de la portadora para representar diferentes estados digitales. Es resistente a la interferencia y se utiliza en sistemas de comunicación inalámbrica[4][5].

- **Modulación por Desplazamiento de Fase (PSK):** PSK cambia la fase de la portadora para codificar la información. Es eficiente en términos de ancho de banda y se utiliza en sistemas de comunicación avanzados como Wi-Fi y redes móviles[4][5].

- **Modulación de Amplitud en Cuadratura (QAM):** QAM combina ASK y PSK para transmitir múltiples bits por símbolo, aumentando la eficiencia del ancho de banda. Se utiliza en sistemas de comunicación modernos como cablemódem y redes inalámbricas[4][5].

## 3.3 Conversión Analógico-Digital

### 3.3.1 Muestreo, Cuantización y Codificación

1. **Muestreo:** Consiste en tomar muestras de una señal analógica a intervalos regulares. El criterio de Nyquist establece que la frecuencia de muestreo debe ser al menos el doble de la frecuencia máxima de la señal para evitar el aliasing[6].

2. **Cuantización:** Asigna un valor discreto a cada muestra, convirtiendo una señal continua en una señal digital con un número finito de valores posibles. Puede ser uniforme o no uniforme[6].

3. **Codificación:** Asigna un código digital a cada valor cuantizado, permitiendo la representación digital de la señal original[6].

## 3.4 Códigos de Línea

### 3.4.1 RZ, NRZ, NRZ-L, AMI, Pseudo-Ternaria, Manchester, Manchester Diferencial, B8ZS, HDB3

- **RZ (Retourn to Zero):** Un código que vuelve a cero después de cada pulso, siendo autosincronizante pero requiriendo más ancho de banda[7].

- **NRZ (Non-Return to Zero):** Un código que no vuelve a cero entre bits, disponible en versiones unipolares y bipolares[7].

- **NRZ-L (Non-Return to Zero-Level):** Similar a NRZ pero con un nivel de referencia para la lógica[7].

- **AMI (Alternate Mark Inversion):** Utiliza polaridades alternas para representar los unos y ceros[7].

- **Pseudo-Ternaria:** Utiliza tres niveles para representar los datos, reduciendo la interferencia[7].

- **Manchester y Manchester Diferencial:** Códigos que utilizan transiciones para representar los bits, permitiendo autosincronismo[7].

- **B8ZS y HDB3:** Códigos utilizados para evitar largas secuencias de ceros y mantener el sincronismo en transmisiones de alta velocidad[7].

## 3.5 Modem, Estándares y Protocolos

Los estándares para módems establecen cómo se realizan las transmisiones de datos, incluyendo la modulación y técnicas de transmisión. Estos estándares son cruciales para garantizar la compatibilidad entre diferentes dispositivos y sistemas de comunicación[8].

---


## Ejemplo de Modulación Analógica: Modulación en Amplitud (AM)

### Pasos

1. **Definir la Señal Moduladora:**
   - Supongamos que tenemos una señal moduladora $$m(t) = \sin(2\pi \times 1000t)$$, que es una onda senoidal con una frecuencia de 1000 Hz.

2. **Definir la Portadora:**
   - La portadora es una onda senoidal con una frecuencia mucho mayor que la señal moduladora. Digamos que tiene una frecuencia de 100 kHz. La portadora se puede representar como $$c(t) = \sin(2\pi \times 100000t)$$.

3. **Aplicar la Modulación de Amplitud:**
   - La modulación de amplitud se realiza multiplicando la portadora por la señal moduladora más un valor constante para evitar que la amplitud sea negativa. La ecuación general es:
     $$
     y(t) = (1 + m(t)) \times c(t)
     $$
   - Sustituyendo las ecuaciones anteriores, obtenemos:
     $$
     y(t) = (1 + \sin(2\pi \times 1000t)) \times \sin(2\pi \times 100000t)
     $$

4. **Visualizar el Resultado:**
   - La señal modulada $$y(t)$$ tendrá una amplitud que varía según la señal moduladora. Esto se puede visualizar gráficamente para ver cómo la amplitud de la portadora cambia con el tiempo.

## Ejemplo de Modulación Digital: Modulación por Desplazamiento de Amplitud (ASK)

### Pasos

1. **Definir la Señal Digital:**
   - Supongamos que tenemos una secuencia de bits digitales: `1010`.

2. **Definir la Portadora:**
   - La portadora es una onda senoidal con una frecuencia alta, por ejemplo, 100 kHz. La portadora se puede representar como $$c(t) = \sin(2\pi \times 100000t)$$.

3. **Aplicar la Modulación ASK:**
   - En ASK, cada bit se representa por un nivel de amplitud diferente. Por ejemplo, un `1` podría representarse con una amplitud alta y un `0` con una amplitud baja o ausencia de señal.
   - Para cada bit, multiplicamos la portadora por el nivel de amplitud correspondiente durante un período de símbolo.

4. **Visualizar el Resultado:**
   - La señal modulada tendrá diferentes amplitudes para cada bit. Por ejemplo:
     - Para el bit `1`, la señal es $$A \times \sin(2\pi \times 100000t)$$.
     - Para el bit `0`, la señal es $$0 \times \sin(2\pi \times 100000t)$$ o una amplitud muy baja.

5. **Transmisión y Recepción:**
   - La señal modulada se transmite y en el receptor se demodula para recuperar la secuencia original de bits.


## Ejemplo de Modulación Analógica - Modulación en Amplitud (AM) en la Radio

### Pasos

1. **Definir la Señal Moduladora:**
   - Imagina que estás escuchando tu canción favorita en la radio. La voz del cantante y la música son la señal moduladora. Esta señal es una onda sonora continua que varía en amplitud y frecuencia según la melodía y el volumen de la música.

2. **Definir la Portadora:**
   - La radio utiliza una frecuencia de radiofrecuencia (RF) como portadora. Por ejemplo, una estación de radio puede transmitir en una frecuencia de 95.5 MHz.

3. **Aplicar la Modulación de Amplitud:**
   - La modulación de amplitud se utiliza para variar la amplitud de la onda portadora según la señal de audio. Esto significa que cuando la música es más fuerte, la amplitud de la onda portadora aumenta, y cuando es más suave, disminuye.

4. **Visualizar el Resultado:**
   - Al recibir la señal modulada en tu radio, el receptor demodula la señal para recuperar la música original. Así, puedes escuchar la canción con los cambios de volumen y frecuencia originales.

**Aplicación Diaria:**
- Cada vez que escuchas la radio, estás recibiendo señales moduladas en amplitud. La modulación AM es común en transmisiones de radio AM.

## Ejemplo de Modulación Digital - Modulación por Desplazamiento de Amplitud (ASK) en Sensores de Movimiento

### Pasos

1. **Definir la Señal Digital:**
   - Imagina un sensor de movimiento en una casa que envía señales digitales (`1` o `0`) para indicar si detecta movimiento o no.

2. **Definir la Portadora:**
   - El sensor utiliza una frecuencia de radiofrecuencia como portadora para transmitir la información.

3. **Aplicar la Modulación ASK:**
   - Cuando el sensor detecta movimiento, envía una señal de alta amplitud (`1`). Si no detecta movimiento, envía una señal de baja amplitud o ausencia de señal (`0`).

4. **Visualizar el Resultado:**
   - El receptor en el sistema de seguridad recibe la señal modulada y la demodula para determinar si hay movimiento o no. Si la señal es fuerte, activa la alarma; si es débil o ausente, no hace nada.

**Aplicación Diaria:**
- Los sensores de movimiento en sistemas de seguridad utilizan modulación digital para transmitir información sobre la presencia o ausencia de movimiento. Esto es útil para activar luces o alarmas automáticamente.

# Práctica

### Proyecto: Control de Brillo de LED con ESP32

**Objetivo:** Aprender a controlar el brillo de un LED utilizando PWM en la ESP32, que es similar al concepto de modulación por desplazamiento de amplitud (ASK).

**Materiales necesarios:**
- Placa ESP32 (por ejemplo, ESP32 DevKit V1)
- LED
- Resistencia (330 ohmios)
- Protoboard
- Cables de conexión

**Pasos a seguir:**

1. **Configurar el entorno de Arduino IDE:**
   - Asegúrate de tener instalado el soporte para ESP32 en el Arduino IDE. Si no lo tienes, puedes instalarlo siguiendo las instrucciones en el sitio oficial de Arduino.

2. **Conectar el LED a la ESP32:**
   - Conecta el LED a una resistencia (330 ohmios) y luego conecta el extremo positivo del LED al pin GPIO5 de la ESP32. El extremo negativo del LED va al extremo positivo de la resistencia, y el extremo negativo de la resistencia va a tierra (GND) de la ESP32.

3. **Escribir el código:**
   - Abre el Arduino IDE y crea un nuevo proyecto. Copia el siguiente código y pégalo en el editor:

```cpp
// Configuración del pin del LED
const int ledPin = 5;

// Configuración del canal PWM
const int pwmChannel = 0;

// Configuración de la frecuencia y resolución del PWM
const int pwmFrequency = 1000; // 1 kHz
const int pwmResolution = 8; // 8 bits (0-255)

void setup() {
  // Configurar el pin del LED como salida
  pinMode(ledPin, OUTPUT);

  // Configurar el canal PWM
  ledcSetup(pwmChannel, pwmFrequency, pwmResolution);
  ledcAttachPin(ledPin, pwmChannel);
}

void loop() {
  // Incrementar el brillo del LED
  for (int dutyCycle = 0; dutyCycle = 0; dutyCycle--) {
    ledcWrite(pwmChannel, dutyCycle);
    delay(15);
  }
}
```

4. **Subir el código a la ESP32:**
   - Selecciona la placa ESP32 en el menú "Tools" > "Board" y selecciona el puerto correcto.
   - Haz clic en el botón "Upload" para subir el código a la ESP32.

5. **Observar el resultado:**
   - Una vez que el código esté cargado, observa cómo el brillo del LED cambia gradualmente, aumentando y disminuyendo en un ciclo continuo. Esto ilustra cómo se puede controlar la amplitud de una señal, similar al concepto de ASK.

---

**Explicación del concepto:**
- En este proyecto, el brillo del LED se controla variando el ciclo de trabajo del PWM, que es similar a cómo se varía la amplitud en la modulación por desplazamiento de amplitud (ASK). En ASK, la amplitud de la onda portadora se ajusta para representar diferentes estados digitales (por ejemplo, `1` y `0`). En este caso, el brillo del LED representa la amplitud variable.



