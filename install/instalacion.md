# 🛠️ Guía de Instalación: OpenVAS (GVM) en Kali Linux

Este recurso técnico es una pieza central del proyecto "El Arsenal de un Analista" (Módulo 6). El objetivo es proporcionar una metodología de despliegue robusta, nativa y verificable para el escáner de vulnerabilidades Greenbone Vulnerability Management (GVM) sobre una distribución Kali Linux.

---

## 📋 1. Requisitos de Infraestructura

Para garantizar que el motor de escaneo procese los NVTs (Network Vulnerability Tests) sin latencias críticas, se deben cumplir los siguientes requisitos mínimos:

* **CPU:** 2 núcleos dedicados (4 recomendados para escaneos concurrentes).
* **Memoria RAM:** 8GB (Mínimo absoluto). El backend de PostgreSQL y el servicio Redis requieren gestión de memoria intensiva.
* **Almacenamiento:** 15GB+ libres en la partición `/var` para la persistencia de la base de datos de firmas.
* **Sistema:** Kali Linux Rolling (Actualizado al último parche de seguridad).

---

## 🚀 2. Implementación Técnica Paso a Paso

### Fase A: Preparación del Ecosistema

Antes de la instalación, sincronizamos los repositorios para evitar conflictos de dependencias con el kernel.

```bash
sudo apt update && sudo apt upgrade -y
```

### Fase B: Despliegue de Binarios

Instalamos el meta-paquete **gvm**. Este paquete consolida el scanner OpenVAS, el gestor de vulnerabilidades y la interfaz web GSA (Greenbone Security Assistant).

```bash
sudo apt install gvm -y
```

### Fase C: Configuración y Sincronización (Setup)

Este proceso inicializa las bases de datos y descarga los feeds de vulnerabilidades (CVEs, CERTs, SCAP).

> ⚠️ **Proceso Crítico:** Esta fase puede demorar entre 30 y 60 minutos. No interrumpas la ejecución, ya que podrías corromper la base de datos de firmas.

```bash
sudo gvm-setup
```

**Nota:** Al finalizar, el sistema generará una contraseña de administrador. Es imperativo documentarla inmediatamente para el acceso a la consola.

---

## ✅ 3. Verificación de Integridad

Como analistas, validamos la operatividad del sistema mediante diagnósticos de logs. Este paso garantiza que todos los microservicios están comunicándose correctamente.

```bash
sudo gvm-check-setup
```

Si el diagnóstico es positivo, el mensaje final indicará: **It seems like your GVM installation is OK.**

---

## ⚙️ 4. Gestión Operativa del Servicio

Para optimizar los recursos de la estación de trabajo, gestionamos el ciclo de vida de los servicios de forma manual:

| Operación  | Comando Técnico        | Impacto en el Sistema                             |
| ---------- | ---------------------- | ------------------------------------------------- |
| Iniciar    | `sudo gvm-start`       | Levanta PostgreSQL, Redis y GSA (Puerto 9392).    |
| Detener    | `sudo gvm-stop`        | Libera memoria RAM cerrando procesos secundarios. |
| Actualizar | `sudo gvm-feed-update` | Sincroniza las firmas con las amenazas del día.   |

---

## 🔒 5. Acceso a la Consola de Gestión

Una vez iniciado el servicio, la interfaz web es accesible localmente:

* **Dirección:** [https://127.0.0.1:9392](https://127.0.0.1:9392)
* **Usuario:** admin
* **Credenciales:** [Utilizar la contraseña generada en la Fase C]

---

## 📝 Notas de Autoría y Licencia

Este manual ha sido desarrollado para fines académicos y profesionales.

* **Autor:** Analista de Ciberseguridad (Portfolio)
* **Licencia:** MIT (Permite uso y distribución citando al autor).

