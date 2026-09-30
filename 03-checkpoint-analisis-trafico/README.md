# Checkpoint 3 — Análisis de tráfico e identificación de protocolos inseguros

## Reporte de Análisis de Tráfico

**Máquina virtual:** Debian GNU/Linux 13  
**Hipervisor:** Oracle VirtualBox  
**Herramienta:** Wireshark 4.4.18  
**Interfaz analizada:** `enp0s3`

---

## 1. Objetivo

El objetivo de esta práctica fue capturar y analizar el tráfico generado desde la máquina virtual utilizando Wireshark, identificando los protocolos involucrados en una navegación web y comparando una comunicación HTTP con una comunicación HTTPS protegida mediante TLS.

Durante la práctica se visitaron:

- `http://neverssl.com`
- `https://www.wikipedia.org`

---

## 2. Protocolos identificados

| Protocolo | Función | Observación |
|---|---|---|
| **DNS** | Resuelve nombres de dominio a direcciones IP. | Se observó la resolución de `neverssl.com`. |
| **TCP** | Establece y mantiene conexiones confiables. | Se identificó el Three-Way Handshake. |
| **HTTP** | Permite la comunicación web sin cifrado TLS. | Se observó un `GET /` y una respuesta `200 OK`. |
| **TLS** | Protege la comunicación mediante cifrado e integridad. | Se observaron TLSv1.2 y TLSv1.3. |
| **OCSP** | Participa en la comprobación del estado de certificados. | Aparecieron paquetes OCSP durante la captura. |

---

## 3. Análisis DNS

Se utilizó el filtro:

```
dns.qry.name contains "neverssl"
```

La respuesta DNS mostró:

- **Dominio:** `neverssl.com`
- **Tipo de registro:** `A`
- **Dirección IP:** `34.223.124.45`
- **Servidor DNS observado:** `172.16.100.4`
- **IP de la máquina de laboratorio:** `10.0.2.15`

La evidencia permite observar cómo el nombre de dominio es traducido a una dirección IPv4 antes de establecer la comunicación con el servidor.

---

## 4. Análisis de tráfico HTTP

Se utilizó el filtro:

```
http
```

Se identificó una solicitud HTTP hacia NeverSSL con:

- **Método:** `GET`
- **URI:** `/`
- **Versión:** `HTTP/1.1`
- **Host:** `neverssl.com`

También se observó la respuesta:

```
HTTP/1.1 200 OK
```

El análisis demuestra que determinados elementos de la comunicación HTTP pueden observarse directamente en Wireshark, como el método, la URI, el Host y otros encabezados.

### ¿Por qué HTTP es inseguro?

HTTP no utiliza TLS para cifrar la comunicación. Por este motivo, información de la capa de aplicación puede quedar expuesta a un tercero que tenga capacidad de observar el tráfico de red.

---

## 5. Análisis de HTTPS/TLS

Se utilizó el filtro:

```
tls
```

La captura mostró comunicaciones **TLSv1.2** y **TLSv1.3**, incluyendo mensajes como:

- Client Hello
- Server Hello
- Application Data

La comunicación se realizó mediante el puerto **443**.

A diferencia del tráfico HTTP observado anteriormente, no se pudo leer directamente el contenido HTTP de la página. En su lugar, Wireshark mostró los mensajes y datos de aplicación protegidos por TLS.

---

## 6. Three-Way Handshake TCP

Se utilizó inicialmente el filtro:

```
tcp.flags.syn == 1
```

Luego se identificó el **Stream Index 13** y se aplicó:

```
tcp.stream == 13
```

Se observaron los tres paquetes que forman el establecimiento inicial de TCP:

1. **SYN** — `10.0.2.15 → 151.101.129.91`
2. **SYN, ACK** — `151.101.129.91 → 10.0.2.15`
3. **ACK** — `10.0.2.15 → 151.101.129.91`

Secuencia:

```
SYN → SYN/ACK → ACK
```

---

## 7. Comparación de seguridad

### HTTP

HTTP no proporciona cifrado de transporte. En la captura se pudieron observar directamente datos de la solicitud, incluyendo el método GET, la URI, el Host y otros encabezados.

### HTTPS

HTTPS utiliza TLS para proteger la comunicación. Proporciona:

- Confidencialidad mediante cifrado.
- Integridad de los datos transmitidos.
- Autenticación del servidor mediante certificados.

### VPN

Una VPN crea un túnel cifrado entre el dispositivo y el servidor VPN. Esto protege el tráfico en ese tramo de la comunicación.

Una VPN no convierte HTTP en HTTPS: la seguridad de la comunicación con el sitio de destino sigue dependiendo del protocolo utilizado hacia ese destino.

---

## 8. Evidencias

Las capturas realizadas durante la práctica permiten demostrar:

1. Resolución DNS de `neverssl.com`.
2. Solicitud HTTP mediante `GET /`.
3. Respuesta HTTP `200 OK`.
4. Comunicación HTTPS mediante TLS.
5. Establecimiento de una conexión TCP mediante SYN → SYN/ACK → ACK.

---

## 9. Conclusión

La práctica permitió observar directamente cómo una navegación web genera diferentes protocolos y etapas de comunicación.

El análisis DNS permitió identificar la resolución de un dominio a una dirección IP. El análisis HTTP mostró una solicitud `GET` y una respuesta `200 OK`, evidenciando que determinados datos de aplicación pueden ser observados directamente.

Por otra parte, el análisis TLS permitió comprobar que HTTPS protege el contenido de aplicación mediante cifrado. Finalmente, el Three-Way Handshake permitió identificar cómo TCP establece inicialmente una conexión mediante la secuencia SYN, SYN/ACK y ACK.

La práctica demuestra la importancia de utilizar protocolos seguros como HTTPS/TLS y de analizar el tráfico de red para detectar comunicaciones que puedan exponer información.
