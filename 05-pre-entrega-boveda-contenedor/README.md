# Pre-Entrega 5 — Mi bóveda y contenedor seguro

## Objetivo

Aplicar mecanismos básicos de protección de credenciales y almacenamiento mediante **KeePassXC** y **VeraCrypt**, documentando la configuración y las evidencias del procedimiento realizado en Debian.

## 1. Bóveda de identidad — KeePassXC

- Base de datos local: `Boveda_Ciberseguridad.kdbx`
- Protección mediante contraseña maestra robusta.
- Se crearon **3 registros de prueba**.
- Se utilizó el generador interno de KeePassXC.
- Las contraseñas generadas tienen más de 16 caracteres y combinan mayúsculas, minúsculas, números y símbolos.
- La evidencia final muestra los **3 apuntes** en la bóveda.

## 2. Contenedor acorazado — VeraCrypt

Se creó un contenedor de archivos VeraCrypt con:

- Tamaño: **100 MB**
- Algoritmo de cifrado: **AES**
- Sistema de archivos: **exFAT**
- Tipo: volumen VeraCrypt común
- Archivo de evidencia: `evidencia.txt`

El contenedor fue montado para almacenar el archivo de evidencia y posteriormente desmontado.

También se realizó una **copia de seguridad del encabezado (Header Backup)** en una ubicación separada del contenedor.

## 3. Evidencias documentadas

El procedimiento incluye evidencias de:

1. Bóveda KeePassXC con 3 registros.
2. Generador interno de contraseñas.
3. Configuración de 100 MB.
4. Configuración AES.
5. Configuración exFAT.
6. Creación exitosa del volumen.
7. Montaje del volumen.
8. Archivo `evidencia.txt`.
9. Copia de seguridad del encabezado.
10. Desmontaje final.

## 4. Resultado

La práctica fue realizada en Debian mediante KeePassXC y VeraCrypt, verificando los requisitos solicitados y documentando las etapas principales mediante capturas de pantalla.

> **Nota de seguridad:** no se incluyen contraseñas reales ni archivos de claves sensibles dentro del repositorio.
