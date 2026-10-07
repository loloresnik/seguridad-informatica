# Checkpoint 7 — Reporte de Auditoría de Red Local

## Datos generales

- **Autor:** Lorenzo Resnik
- **Fecha:** 07/10/2026
- **Entorno:** Debian GNU/Linux en Oracle VirtualBox
- **Red de laboratorio:** Hotspot de teléfono móvil
- **Segmento analizado:** `172.20.10.0/28`
- **Herramienta:** Nmap 7.95

### Declaración de ética

El análisis se realizó únicamente sobre dispositivos pertenecientes a la red de laboratorio utilizada para la práctica y con autorización para realizar el reconocimiento. El objetivo es identificar servicios expuestos y documentar recomendaciones de seguridad.

---

# Dispositivo 1

## Identificación

| Dato | Resultado |
|---|---|
| **Dirección IP** | `172.20.10.1` |
| **Dirección MAC** | `6A:A7:29:D6:3A:64` |
| **Estado** | Host activo |
| **Sistema operativo** | No identificado específicamente por Nmap |

El dispositivo `172.20.10.1` corresponde al gateway de la red del hotspot, según la ruta obtenida durante la práctica.

## Puertos y servicios

El escaneo se realizó con:

```bash
sudo nmap -sV -Pn 172.20.10.1
```

Nmap informó 996 puertos TCP cerrados y los siguientes puertos abiertos:

| Puerto | Estado | Servicio | Versión |
|---|---|---|---|
| 21/tcp | open | FTP | No identificada |
| 53/tcp | open | domain/DNS | No identificada |
| 49152/tcp | open | tcpwrapped | No identificada |
| 62078/tcp | open | tcpwrapped | No identificada |

### Análisis de hallazgos

#### Puerto 21/tcp — FTP

**¿Qué es?**  
FTP es un protocolo utilizado para la transferencia de archivos entre equipos.

**¿Por qué importa?**  
Si el servicio FTP no es necesario, mantenerlo expuesto representa una superficie de ataque innecesaria. Además, FTP tradicional no proporciona por sí mismo el cifrado de las credenciales y datos de la comunicación.

**Recomendación:**  
Deshabilitar el servicio FTP si no es necesario. Si se requiere transferencia de archivos, utilizar una alternativa segura y restringir el acceso únicamente a los equipos que lo necesiten.

#### Puerto 53/tcp — DNS

**¿Qué es?**  
El puerto 53 está asociado al servicio DNS, utilizado para resolver nombres de dominio.

**¿Por qué importa?**  
En un gateway es razonable encontrar DNS abierto, pero el servicio debería aceptar consultas únicamente de los clientes autorizados. Una exposición innecesaria puede permitir consultas desde redes no previstas o aumentar la superficie de ataque.

**Recomendación:**  
Mantener el servicio únicamente si es necesario y restringir las consultas DNS a los clientes de la red autorizada.

#### Puertos 49152/tcp y 62078/tcp — tcpwrapped

**¿Qué es?**  
Nmap detectó ambos puertos como `tcpwrapped`, lo que indica que la conexión TCP fue aceptada o filtrada de una forma que impidió identificar el servicio concreto.

**¿Por qué importa?**  
No es posible determinar con la evidencia obtenida qué servicio se encuentra detrás de estos puertos. Por el criterio de mínimo servicio necesario, cualquier puerto abierto que no tenga una función conocida debería investigarse.

**Recomendación:**  
Identificar qué procesos utilizan estos puertos y cerrar o restringir aquellos que no sean necesarios.

---

# Dispositivo 2

## Identificación

| Dato | Resultado |
|---|---|
| **Dirección IP** | `172.20.10.5` |
| **Dirección MAC** | `08:00:27:D6:4B:3F` |
| **Estado** | Host activo |
| **Sistema operativo** | No identificado específicamente por Nmap |

El dispositivo corresponde a la máquina Debian utilizada para realizar la práctica. Nmap no pudo determinar específicamente el sistema operativo.

## Puertos y servicios

El escaneo se realizó con:

```bash
sudo nmap -sV -O -Pn 172.20.10.5
```

Resultado: Nmap informó que los **1000 puertos TCP analizados se encontraban cerrados** y no identificó servicios abiertos.

| Puerto | Estado | Servicio | Versión |
|---|---|---|---|
| Puertos TCP analizados | closed | No se detectaron servicios abiertos | No aplica |

### Análisis del hallazgo

**¿Qué se encontró?**  
No se detectaron servicios TCP abiertos en los 1000 puertos analizados.

**¿Por qué importa?**  
Desde el punto de vista de exposición de servicios TCP, el resultado es favorable porque no se identificaron servicios accesibles desde el dispositivo utilizado para la auditoría.

**Recomendación:**  
Mantener activos únicamente los servicios necesarios, conservar el sistema actualizado y utilizar un firewall para controlar las conexiones entrantes.

---

# Comparación de los dispositivos

| Aspecto | Dispositivo 1 — 172.20.10.1 | Dispositivo 2 — 172.20.10.5 |
|---|---|---|
| Host activo | Sí | Sí |
| Puertos abiertos detectados | 4 | 0 |
| FTP | Sí, 21/tcp | No |
| DNS | Sí, 53/tcp | No |
| tcpwrapped | 49152/tcp y 62078/tcp | No |
| SO identificado por Nmap | No específicamente | No específicamente |
| Exposición observada | Mayor | Baja |

---

# Recomendaciones generales

1. **Aplicar el principio de mínimo servicio necesario:** mantener abiertos únicamente los puertos requeridos.
2. **Deshabilitar servicios innecesarios**, especialmente servicios de transferencia de archivos que no estén siendo utilizados.
3. **Restringir servicios de infraestructura**, como DNS, a los clientes autorizados.
4. **Investigar puertos tcpwrapped** para identificar qué procesos los utilizan.
5. **Mantener los sistemas actualizados** y utilizar reglas de firewall para controlar el tráfico entrante.
6. **Repetir periódicamente la auditoría** para comprobar que no aparezcan nuevos servicios expuestos.

# Conclusión

El reconocimiento permitió identificar dos dispositivos activos en la red de laboratorio. El dispositivo `172.20.10.1`, utilizado como gateway del hotspot, presentó cuatro puertos TCP abiertos: FTP, DNS y dos puertos identificados como tcpwrapped. El principal hallazgo a revisar es el servicio FTP, que debería mantenerse únicamente si existe una necesidad concreta.

El dispositivo `172.20.10.5`, correspondiente a la máquina Debian utilizada durante la práctica, no presentó puertos TCP abiertos entre los 1000 puertos analizados.

El análisis demuestra la importancia de no limitarse a detectar puertos, sino de interpretar qué servicios están expuestos, determinar si son necesarios y aplicar el principio de mínimo servicio necesario.
