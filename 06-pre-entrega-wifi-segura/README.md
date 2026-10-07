# 06 — Seguridad en el aire: cómo sobrevivir a una Wi-Fi pública

## Introducción

Esta práctica tiene como objetivo comprender los riesgos asociados al uso de redes Wi-Fi públicas y analizar qué información puede quedar expuesta durante una conexión web.

Se trabajó con **HTTP y HTTPS**, utilizando las herramientas de desarrollador de Google Chrome para observar una solicitud HTTP real.

El laboratorio se realizó en **Debian GNU/Linux** utilizando **Google Chrome**.

---

## Sitio analizado

Se utilizó el sitio de prueba:

`http://neverssl.com`

NeverSSL está diseñado para permitir observar una conexión HTTP sin el cifrado propio de HTTPS.

Durante la práctica, Chrome accedió a una dirección de prueba de NeverSSL y permitió observar una solicitud HTTP.

### Evidencia 1 — Acceso al sitio

![Acceso a NeverSSL](./Captura%20de%20pantalla%202026-10-06%20215229.png)

---

## Evidencia observada

La solicitud capturada mostró los siguientes datos:

| Dato | Resultado |
|---|---|
| Protocolo | HTTP |
| Request URL | `http://youngbeautifulwonderouszen.neverssl.com/online/` |
| Método | GET |
| Estado | 200 OK |
| Puerto | 80 |
| Host | `youngbeautifulwonderouszen.neverssl.com` |

### Evidencia 2 — Network

Se abrió la herramienta **Network** de Chrome para registrar las solicitudes realizadas por el navegador.

![Network](./Captura%20de%20pantalla%202026-10-06%20215248.png)

### Evidencia 3 — Datos de la solicitud

La sección **Headers** permite observar la URL solicitada, el método utilizado, el código de estado y la dirección remota.

![Datos de la solicitud HTTP](./Captura%20de%20pantalla%202026-10-06%20215304.png)

También se observaron diferentes **Request Headers**, entre ellos:

- Host
- User-Agent
- Accept
- Accept-Encoding
- Accept-Language
- Connection
- Upgrade-Insecure-Requests

Estas cabeceras permiten observar información relacionada con el destino de la comunicación y características del cliente, como el navegador, sistema operativo, idioma y formatos aceptados.

### Evidencia 4 — Request Headers

![Request Headers](./Captura%20de%20pantalla%202026-10-06%20215322.png)

### Evidencia 5 — Confirmación de HTTP

Esta captura muestra de forma directa la URL con `http://`, el método `GET`, el estado `200 OK` y el puerto `80`.

![Evidencia HTTP](./Captura%20de%20pantalla%202026-10-06%20215339.png)

---

## HTTP vs HTTPS

### HTTP

HTTP (HyperText Transfer Protocol) es un protocolo utilizado para la comunicación entre clientes y servidores web.

En esta práctica se observó una solicitud:

- con una URL que comienza con `http://`
- utilizando el método `GET`
- mediante el puerto `80`

HTTP no proporciona por sí mismo el cifrado que ofrece HTTPS.

### HTTPS

HTTPS utiliza HTTP sobre una conexión protegida mediante TLS.

El cifrado ayuda a proteger la información durante el tránsito y dificulta que terceros puedan leer o modificar el contenido de la comunicación.

---

## Riesgos de utilizar HTTP en una Wi-Fi pública

Utilizar HTTP desde una red pública puede generar diferentes riesgos:

### 1. Sniffing o interceptación

Un atacante que pueda observar el tráfico de la red podría analizar información que viaje sin cifrado.

### 2. Man-in-the-Middle

Un atacante puede intentar colocarse entre el usuario y el servidor para interceptar o manipular las comunicaciones.

### 3. Evil Twin

Una red inalámbrica falsa puede imitar a una red legítima para conseguir que los usuarios se conecten y así intentar observar su tráfico.

Una Wi-Fi protegida con contraseña tampoco garantiza por sí sola que las comunicaciones sean seguras.

---

## ¿Cómo ayuda una VPN?

Una VPN establece un **túnel cifrado** entre el dispositivo y el servidor VPN.

El tráfico se **encapsula** dentro de ese túnel y viaja protegido frente a observadores presentes en la red local.

Esto mejora la privacidad y reduce la exposición del tráfico cuando se utiliza una red Wi-Fi pública.

Una VPN, sin embargo, no convierte automáticamente cualquier sitio web en seguro: es importante seguir utilizando HTTPS y mantener buenas prácticas de seguridad.

---

## 3 Reglas de Oro para una Wi-Fi pública

1. **Evitar transmitir información sensible mediante sitios HTTP.**
2. **Comprobar que los sitios importantes utilicen HTTPS y verificar la dirección del sitio.**
3. **Utilizar una VPN confiable cuando sea necesario conectarse desde una red pública y evitar redes sospechosas.**

---

## Conclusión

La práctica permitió comprobar directamente cómo aparece una solicitud HTTP en las herramientas de desarrollador de Chrome.

Se identificaron la **URL, el método GET, el código de estado 200 OK, el puerto 80 y diferentes Request Headers**.

El ejercicio permite comprender por qué el cifrado, HTTPS y el uso de un túnel VPN son importantes para reducir los riesgos al utilizar redes Wi-Fi públicas.

---

## Herramientas utilizadas

- Debian GNU/Linux
- Google Chrome
- Chrome DevTools — Network
- HTTP / HTTPS
- Git / GitHub

