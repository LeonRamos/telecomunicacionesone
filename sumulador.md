Código para Google Colab este simula el proceso de encapsulación según el modelo OSI

```python
#@title Simulador de Encapsulación OSI
from dataclasses import dataclass
from typing import Dict, Any
import binascii

@dataclass
class PaqueteRed:
    capas: Dict[str, Any]
    payload: bytes

class CapaAplicacion:
    @staticmethod
    def encapsular(datos: str) -> PaqueteRed:
        """Simula las 3 capas superiores del modelo OSI (Aplicación, Presentación, Sesión)"""
        return PaqueteRed(
            capas={
                'formato': 'UTF-8',
                'protocolo': 'HTTP/1.1',
                'session_id': 'SID-12345'
            },
            payload=datos.encode('utf-8')
        )

class CapaTransporte:
    __seq_num = 0  # Variable privada para numeración de segmentos
    
    @classmethod
    def encapsular(cls, paquete: PaqueteRed) -> PaqueteRed:
        """Divide en segmentos y añade numeración"""
        cls.__seq_num += 1
        return PaqueteRed(
            capas={
                **paquete.capas,
                'tipo': 'SEGMENTO',
                'numero_secuencia': cls.__seq_num,
                'puerto_origen': 8080,
                'puerto_destino': 80
            },
            payload=paquete.payload
        )

class CapaRed:
    @staticmethod
    def encapsular(paquete: PaqueteRed, ip_origen: str, ip_destino: str) -> PaqueteRed:
        """Añade direccionamiento IP"""
        return PaqueteRed(
            capas={
                **paquete.capas,
                'tipo': 'PAQUETE',
                'ip_origen': ip_origen,
                'ip_destino': ip_destino
            },
            payload=paquete.payload
        )

class CapaEnlace:
    @staticmethod
    def encapsular(paquete: PaqueteRed, mac_origen: str, mac_destino: str) -> PaqueteRed:
        """Añade direcciones MAC y crea trama"""
        return PaqueteRed(
            capas={
                **paquete.capas,
                'tipo': 'TRAMA',
                'mac_origen': mac_origen,
                'mac_destino': mac_destino
            },
            payload=paquete.payload
        )

class CapaFisica:
    @staticmethod
    def encapsular(paquete: PaqueteRed) -> bytes:
        """Convierte a bits para transmisión"""
        header = str(paquete.capas).encode('utf-8')
        return header + b'|||' + paquete.payload

# === Simulación completa ===
def simular_envio(datos: str, ip_destino: str, mac_destino: str):
    print("=== Simulación de Encapsulación OSI ===")
    
    # 1. Capas superiores (Aplicación, Presentación, Sesión)
    paquete = CapaAplicacion.encapsular(datos)
    print(f"\n[APLICACIÓN] Datos formateados:\n{paquete.capas}\nPayload: {paquete.payload.decode()}")
    
    # 2. Capa de Transporte
    paquete = CapaTransporte.encapsular(paquete)
    print(f"\n[TRANSPORTE] Segmento creado:\nN° secuencia: {paquete.capas['numero_secuencia']}")
    
    # 3. Capa de Red
    paquete = CapaRed.encapsular(paquete, '192.168.1.100', ip_destino)
    print(f"\n[RED] Encabezado IP añadido:\nOrigen: {paquete.capas['ip_origen']}\nDestino: {paquete.capas['ip_destino']}")
    
    # 4. Capa de Enlace
    paquete = CapaEnlace.encapsular(paquete, '00:1A:2B:3C:4D:5E', mac_destino)
    print(f"\n[ENLACE] Trama Ethernet:\nMAC Origen: {paquete.capas['mac_origen']}\nMAC Destino: {paquete.capas['mac_destino']}")
    
    # 5. Capa Física
    bits = CapaFisica.encapsular(paquete)
    print("\n[FÍSICA] Transmisión binaria:")
    print(binascii.hexlify(bits).decode('utf-8'))

# Ejecutar simulación
simular_envio(
    datos="GET /index.html HTTP/1.1\nHost: www.example.com",
    ip_destino="203.0.113.5",
    mac_destino="00:1C:B3:AA:BB:CC"
)
```

### Explicación del código:

1. **Clases por capa OSI**:
   - Cada capa tiene un método `encapsular` que añade su información específica
   - Usa `dataclass` para organizar los paquetes de red
   - Implementa el flujo: Aplicación → Transporte → Red → Enlace → Física

2. **Proceso de encapsulación**:
   - **Capa de aplicación**: Formatea datos y añade metadatos de sesión[2][4]
   - **Capa de transporte**: Divide en segmentos con numeración[2][4]
   - **Capa de red**: Añade direccionamiento IP[2][4]
   - **Capa de enlace**: Incluye direcciones MAC[2][4]
   - **Capa física**: Convierte todo a flujo binario[4]

3. **Características de implementación**:
   - Uso de variables privadas (`__seq_num`) para control interno[1][3]
   - Métodos estáticos para operaciones específicas por capa[1]
   - Tipado fuerte para claridad en los datos[1]

### Cómo usar en Colab:
1. Copia el código en un nuevo notebook
2. Ejecuta la celda (Shift+Enter)
3. Verás la salida detallada del proceso de encapsulación

### Salida esperada:
```
=== Simulación de Encapsulación OSI ===

[APLICACIÓN] Datos formateados:
{'formato': 'UTF-8', 'protocolo': 'HTTP/1.1', 'session_id': 'SID-12345'}
Payload: GET /index.html HTTP/1.1
Host: www.example.com

[TRANSPORTE] Segmento creado:
N° secuencia: 1

[RED] Encabezado IP añadido:
Origen: 192.168.1.100
Destino: 203.0.113.5

[ENLACE] Trama Ethernet:
MAC Origen: 00:1A:2B:3C:4D:5E
MAC Destino: 00:1C:B3:AA:BB:CC

[FÍSICA] Transmisión binaria:
7b27666f726d... (datos binarios)
```
