# Pre-Entrega 4 — Analista de Amenazas por un Día

## Análisis de un caso simulado de Phishing e Ingeniería Social

### 1. Introducción

El presente trabajo analiza un correo electrónico sospechoso recibido por un profesor de una universidad. El mensaje informa que una bonificación por investigación fue aprobada y solicita ingresar al sitio `portal-universitario-pagos.net` para confirmar datos bancarios antes de las 5:00 PM. El objetivo es identificar las señales de alerta, analizar los riesgos y proponer medidas de respuesta y prevención.

### 2. Identificación de señales de alerta

1. **Dominio sospechoso:** el sitio indicado es `portal-universitario-pagos.net`. El dominio debe verificarse antes de ingresar información.
2. **Urgencia:** el mensaje establece un límite de tiempo: antes de las 5:00 PM. La presión temporal es una técnica de Ingeniería Social.
3. **Beneficio inesperado:** la promesa de una bonificación por investigación busca generar interés y provocar una acción rápida.
4. **Solicitud de datos bancarios:** pedir información bancaria mediante un enlace recibido por correo constituye una señal de riesgo.
5. **Solicitud de inicio de sesión:** el atacante podría utilizar una página falsa para obtener credenciales u otros datos.
6. **Posible suplantación:** el mensaje intenta presentarse como una comunicación legítima relacionada con la universidad, característica de un posible ataque de Phishing.

### 3. Exposición de riesgos

Si el profesor introduce sus datos en el portal falso, un atacante podría obtener información bancaria o credenciales utilizadas durante el acceso. Si esas credenciales fueran reutilizadas en otros servicios, el riesgo podría extenderse a otras cuentas.

En un entorno universitario, una cuenta comprometida también podría utilizarse como punto de acceso inicial para intentar alcanzar otros sistemas o información institucional. El Phishing puede además utilizarse para obtener acceso inicial, instalar malware o producir filtraciones de datos.

### 4. Plan de acción inmediato

1. **Reportar y bloquear:** informar inmediatamente el correo al equipo de seguridad o soporte y bloquear el dominio o enlace sospechoso.
2. **Alertar y verificar:** comunicar el incidente al personal y comprobar si otros empleados recibieron el mismo mensaje. Si alguien ingresó credenciales, iniciar el procedimiento de respuesta correspondiente.
3. **Proteger las cuentas:** revisar las cuentas potencialmente afectadas, cambiar credenciales comprometidas y reforzar la **Autenticación Multifactor (MFA)**.

### 5. Consejo de prevención para estudiantes

**Boletín de prevención — La lupa sobre el enlace**

Si recibís un correo que promete un beneficio y te pide iniciar sesión, no hagas clic directamente. En este caso, antes de acceder a **portal-universitario-pagos.net**, pasá el cursor sobre el enlace sin abrirlo y revisá la dirección real. Si el dominio no coincide con el sitio oficial de la universidad, no ingreses usuario, contraseña ni datos bancarios. Verificá el mensaje por otro canal, por ejemplo, ingresando manualmente al sitio oficial o consultando al soporte. Ante la duda, reportalo.

### 6. Terminología aplicada

| Concepto | Aplicación al caso |
|---|---|
| **Ingeniería Social** | Manipulación del usuario mediante urgencia, beneficio económico y apariencia de legitimidad. |
| **Phishing** | Intento de engañar al destinatario para que entregue información mediante un mensaje y un sitio falso. |
| **Spoofing** | Posible suplantación de una identidad o entidad legítima para hacer que el mensaje parezca confiable. |
| **MFA** | Medida adicional de seguridad que puede reducir el impacto del robo de una contraseña. |

### 7. Conclusión

El caso presenta varias características compatibles con un intento de Phishing: un dominio que debe ser verificado, presión temporal, una recompensa inesperada y una solicitud de información sensible. El análisis demuestra la importancia de no confiar únicamente en la apariencia de un correo y de verificar el destino real de los enlaces.

La combinación de educación, verificación por canales alternativos, reporte de incidentes y MFA permite construir una defensa multicapa frente a la Ingeniería Social.

**Documento correspondiente a la Pre-Entrega 4 — Analista de Amenazas por un Día.**
