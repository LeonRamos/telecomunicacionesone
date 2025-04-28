

## 🧪 Actividad Práctica: **Explorando Servicios de Red desde la Terminal**

### 🎯 Objetivo:
Comprender el funcionamiento básico de los servicios DHCP, DNS, NAT, HTTP, FTP y SMTP mediante comandos de terminal, y analizar cómo estos permiten la comunicación en una red.

---

## 🔧 **Requisitos previos:**
- Conexión a red local con internet
- Terminal de comandos (Linux o Windows con WSL / PowerShell)
- Herramientas: `ping`, `ipconfig` / `ifconfig`, `nslookup`, `curl`, `ftp`, `telnet`, `traceroute`, `netstat`, etc.

---

## 🧭 **Pasos de la Actividad:**

---

### 1. 🔄 **DHCP – Obtener IP automáticamente**

**Comando:**
```bash
ipconfig /renew      # en Windows
sudo dhclient        # en Linux
```

**Preguntas para reflexionar:**
- ¿Qué dirección IP te asignó el servidor DHCP?
- ¿Qué pasaría si el servidor DHCP estuviera apagado?

---

### 2. 🌐 **DNS – Resolución de nombres**

**Comando:**
```bash
nslookup www.google.com
```

**Extra:**
```bash
dig www.google.com      # si se quiere más detalle (Linux)
```

**Preguntas:**
- ¿Qué dirección IP te devuelve?
- ¿Cuál es el servidor DNS que estás usando?

---

### 3. 🔁 **NAT – Ver cómo se traduce tu IP privada a pública**

**Comando:**
```bash
curl ifconfig.me
```

**Preguntas:**
- ¿Tu IP local (ipconfig/ifconfig) es diferente a la IP pública?
- ¿Qué hace NAT en este caso?

---

### 4. 🌍 **HTTP – Navegación y comunicación con servidores web**

**Comando:**
```bash
curl http://example.com
```

**Explora encabezados HTTP:**
```bash
curl -I http://example.com
```

**Preguntas:**
- ¿Qué cabeceras HTTP puedes ver?
- ¿Qué código de respuesta se recibe?

---

### 5. 📁 **FTP – Conexión a un servidor de archivos**

**Comando:**
```bash
ftp ftp.debian.org
```

**Navegar:**
```bash
ls
cd debian
get README
```

**Preguntas:**
- ¿Pudiste descargar un archivo?
- ¿Qué comandos FTP existen desde la terminal?

---

### 6. ✉️ **SMTP – Envío de correos por consola (simulación)**

**Conectarse a un servidor SMTP (puerto 25 o 587):**
```bash
telnet smtp.gmail.com 587     # puede requerir habilitar telnet
```

**Simular conversación SMTP (si el servidor responde):**
```bash
EHLO example.com
MAIL FROM:<tuemail@ejemplo.com>
RCPT TO:<destino@ejemplo.com>
DATA
Este es un mensaje de prueba.
.
QUIT
```

**Nota:** Puede no funcionar con servidores como Gmail si no hay autenticación. Puedes usar servidores locales o simuladores si lo deseas.

---

## 📊 **Producto final:**

- Captura de pantalla de cada comando y su resultado.
- Bitácora o tabla con:
  - Servicio probado
  - Herramienta usada
  - Resultado observado
  - Conclusión personal

---

## 🧠 **Cierre reflexivo / Discusión en clase:**

- ¿Cuál de los servicios es más crítico para que internet funcione?
- ¿Qué ocurre si alguno de ellos falla?
- ¿Cómo podrías configurar una red para que use estos servicios sin depender del ISP?

---
