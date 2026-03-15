# 🔬 Laboratorio OpenVAS / GVM – Escaneo de Vulnerabilidades en Localhost

Este laboratorio demuestra el uso de OpenVAS / Greenbone Vulnerability Management (GVM) para realizar un escaneo de vulnerabilidades sobre el propio sistema.

El objetivo es validar el funcionamiento del motor de escaneo y analizar los resultados obtenidos.

---

## 🎯 Objetivo del laboratorio

El objetivo de este laboratorio es:

* Ejecutar un escaneo de vulnerabilidades sobre localhost
* Analizar el reporte generado
* Comprender cómo interpretar los resultados

Target utilizado:

127.0.0.1

---

## ⚙️ Creación del Target

En la interfaz web:

Configuration → Targets → New Target

Configuración utilizada:

| Campo     | Valor     |
| --------- | --------- |
| Name      | localhost |
| Hosts     | 127.0.0.1 |
| Port List | All TCP   |

Guardar el target.
<p align="center">
  <img src="/img/target.png" width="800" alt="Target">
</p>
<b>Nota:</b> Puedes usar dominios, o usar notación CIDR como 192.168.0.1/24 para hacer scan a segmentos o redes completas

---

## 🧪 Creación del Task de escaneo

Ir a:

Scans → Tasks → New Task

Configuración utilizada:

| Campo       | Valor          |
| ----------- | -------------- |
| Name        | Scan Localhost |
| Scan Target | localhost      |
| Scan Config | Full and Fast  |

El perfil Full and Fast es el perfil estándar porque:

* minimiza impacto en el sistema
* prioriza NVT relevantes
* evita técnicas agresivas

---

## 🚀 Ejecución del escaneo

Para iniciar el escaneo:

Scans → Tasks → Run

Durante el escaneo OpenVAS realiza:

1. Descubrimiento del host
2. Enumeración de puertos
3. Identificación de servicios
4. Ejecución de Network Vulnerability Tests (NVT)

<p align="center">
  <img src="/img/progress.png" width="800" alt="Progreso">
</p>

Duración aproximada del escaneo:

6 minutos

---

## 📊 Resultado del escaneo

Resumen del reporte:

| Host      | Critical | High | Medium | Low |
| --------- | -------- | ---- | ------ | --- |
| 127.0.0.1 | 0        | 0    | 1      | 0   |

Resultado total:

1 vulnerabilidad detectada

Nivel de severidad:

Medium

<p align="center">
  <img src="/img/report.png" width="800" alt="report">
</p>

<b>[REPORTE COMPLETO](/install/reporte.pdf)</b>

---

## 🔎 Vulnerabilidad detectada

Nombre:

SSL/TLS Weak Cipher Suites

Puerto afectado:

5432/tcp

Servicio asociado:

PostgreSQL

CVSS:

5.9 (Medium)

---

## 📌 Detalle técnico

El escaneo detectó que el servicio acepta un cipher TLS considerado débil.

Cipher identificado:

TLS_RSA_WITH_SEED_CBC_SHA

Motivos:

* utiliza cifrado CBC
* no proporciona Perfect Forward Secrecy
* menor resistencia a ataques criptográficos modernos

---

## ⚠️ Impacto

Un atacante podría potencialmente:

* interceptar comunicaciones cifradas
* realizar ataques criptográficos
* obtener información sensible

El impacto depende de:

* exposición del servicio
* configuración TLS
* control de acceso al servicio

---

## 🛠️ Mitigación

Se recomienda:

1. Deshabilitar suites TLS débiles

2. Utilizar suites modernas:

TLS_AES_256_GCM_SHA384
TLS_CHACHA20_POLY1305_SHA256

3. Restringir versiones TLS a:

TLS 1.2
TLS 1.3

4. Revisar configuración TLS del servicio PostgreSQL

---

## 🔍 Validación manual

Con Nmap:

nmap --script ssl-enum-ciphers -p 5432 127.0.0.1

Con sslscan:

sslscan 127.0.0.1:5432

---

## 📌 Conclusiones

Este laboratorio permitió:

* ejecutar un escaneo completo
* analizar un reporte real de vulnerabilidades
* comprender cómo interpretar resultados

Incluso un sistema local puede presentar configuraciones inseguras que deben corregirse.
