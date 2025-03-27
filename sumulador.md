import json
import random
from dataclasses import dataclass
from typing import Dict, Optional

# Simulación de encapsulación de datos en protocolos de red

@dataclass
class PDU:
    """Unidad de Datos de Protocolo (Protocol Data Unit)"""
    payload: any
    headers: Dict[str, str]

class Protocol:
    def encapsulate(self, data: any) -> PDU:
        raise NotImplementedError
    
    def decapsulate(self, pdu: PDU) -> any:
        raise NotImplementedError

# ========== Protocolos de Capa de Aplicación ==========

class HTTP(Protocol):
    def encapsulate(self, request: Dict) -> PDU:
        """Encapsula una solicitud HTTP con headers"""
        headers = {
            "Method": request.get("method", "GET"),
            "Host": request.get("host", "example.com"),
            "Content-Type": "application/json",
            "Connection": "keep-alive"
        }
        return PDU(payload=request.get("body", ""), headers=headers)
    
    def decapsulate(self, pdu: PDU) -> Dict:
        """Decapsula una respuesta HTTP"""
        return {
            "status": pdu.headers.get("Status", "200 OK"),
            "headers": pdu.headers,
            "body": pdu.payload
        }

class FTP(Protocol):
    def encapsulate(self, command: str, file_data: Optional[bytes] = None) -> PDU:
        """Encapsula un comando FTP"""
        headers = {
            "Protocol": "FTP",
            "Command": command,
            "DataPort": "20" if file_data else "21"
        }
        return PDU(payload=file_data, headers=headers)
    
    def decapsulate(self, pdu: PDU) -> Dict:
        """Decapsula una respuesta FTP"""
        return {
            "response": pdu.headers.get("Response", "200 Command OK"),
            "data": pdu.payload
        }

class DHCP(Protocol):
    def encapsulate(self, message_type: str, requested_ip: Optional[str] = None) -> PDU:
        """Encapsula un mensaje DHCP"""
        headers = {
            "MessageType": message_type,
            "TransactionID": str(random.randint(1000, 9999)),
            "ClientMAC": "00:1A:2B:3C:4D:5E"
        }
        if requested_ip:
            headers["RequestedIP"] = requested_ip
        return PDU(payload=None, headers=headers)
    
    def decapsulate(self, pdu: PDU) -> Dict:
        """Decapsula una oferta DHCP"""
        return {
            "assigned_ip": pdu.headers.get("YourIP", "192.168.1.100"),
            "subnet_mask": pdu.headers.get("SubnetMask", "255.255.255.0"),
            "lease_time": pdu.headers.get("LeaseTime", "86400")
        }

class DNS(Protocol):
    def encapsulate(self, query: str, query_type: str = "A") -> PDU:
        """Encapsula una consulta DNS"""
        headers = {
            "QueryID": str(random.randint(1000, 9999)),
            "QueryType": query_type,
            "RecursionDesired": "1"
        }
        return PDU(payload=query, headers=headers)
    
    def decapsulate(self, pdu: PDU) -> Dict:
        """Decapsula una respuesta DNS"""
        return {
            "answer": pdu.headers.get("Answer", "192.0.2.1"),
            "ttl": pdu.headers.get("TTL", "300")
        }

# ========== Simulación de Comunicación ==========

def simulate_network_communication():
    print("=== Simulación de Encapsulación de Datos ===")
    
    # HTTP Example
    http = HTTP()
    http_request = {"method": "POST", "host": "api.example.com", "body": '{"user": "test"}'}
    http_pdu = http.encapsulate(http_request)
    print(f"\nHTTP Request encapsulado:\nHeaders: {http_pdu.headers}\nBody: {http_pdu.payload}")
    
    # FTP Example
    ftp = FTP()
    ftp_pdu = ftp.encapsulate("STOR file.txt", b"Contenido del archivo")
    print(f"\nFTP Command encapsulado:\nHeaders: {ftp_pdu.headers}\nDatos: {ftp_pdu.payload[:20]}...")
    
    # DHCP Example
    dhcp = DHCP()
    dhcp_discover = dhcp.encapsulate("DHCPDISCOVER")
    print(f"\nDHCP Discover encapsulado:\n{json.dumps(dhcp_discover.headers, indent=2)}")
    
    # DNS Example
    dns = DNS()
    dns_query = dns.encapsulate("example.com")
    print(f"\nDNS Query encapsulada:\n{json.dumps(dns_query.headers, indent=2)}\nConsulta: {dns_query.payload}")

if __name__ == "__main__":
    simulate_network_communication()
