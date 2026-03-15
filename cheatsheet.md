# OpenVAS / GVM Cheatsheet

Este documento sirve como referencia rápida para la configuración y uso de OpenVAS (GVM) en auditorías de seguridad.

---

## 📋 Pestaña de Configuraciones (Configurations)

### Targets (Objetivos)

Aquí podemos añadir los objetivos que queremos escanear en las tareas, incluyendo:

- **Puertos**: especificar rangos o puertos individuales.
- **Autenticación**:  
  - Usar un usuario con privilegios elevados (root, Administrator) si es posible para obtener la máxima información del objetivo.
- **Métodos de identificación de disponibilidad del host**:  
  - Para la prueba de disponibilidad (Alive Test), la opción por defecto “Scan Config Default” utiliza el NVT *Ping Host* de la familia NVT correspondiente.

#### 💡 NVT Family (Familia de NVTs)

- Conocida como **OpenVAS Network Vulnerability Test Family**.
- Las familias consisten en distintas categorías de vulnerabilidades según el sistema o servicio: Linux, Windows, aplicaciones web, etc.
- Permiten escoger qué tipo de chequeos realizar según el objetivo.

### Configuraciones por defecto de OpenVAS

Estas configuraciones son seguras de usar y no deberían interrumpir la red:

| Configuración       | Función principal                                                                 |
|--------------------|----------------------------------------------------------------------------------|
| **Base**           | Obtiene información básica del host y sistema operativo. No busca vulnerabilidades. |
| **Discovery**      | Identifica servicios, puertos accesibles y software en el objetivo.             |
| **Host Discovery** | Verifica si el host está activo y qué dispositivos están en la red. No revisa vulnerabilidades. Usa ping. |
| **System Discovery** | Amplía el Discovery Scan e intenta identificar el sistema operativo y hardware del host. |
| **Full and Fast**  | Opción más segura y completa. Usa inteligencia para elegir los mejores NVT según los puertos accesibles. |

---

## 🔍 Pestaña de Escaneos (Scans)

- Lista los escaneos finalizados.
- Permite **crear nuevas tareas** para ejecutar un escaneo:
  - Las tareas se basan en las configuraciones predefinidas de la pestaña **Configurations**.
- Permite **exportar los resultados** en varios formatos (PDF, XML, CSV).

---

## 📤 Exportación de Resultados (Exporting)

- Los resultados de los escaneos pueden exportarse para su análisis o documentación.
- Formatos compatibles:
  - **PDF**: para informes formales.
  - **XML / CSV**: para análisis automático o integración con otras herramientas.
- Permite seleccionar qué hallazgos incluir (vulnerabilidades críticas, medias, bajas).

---

## ⚙ Funciones adicionales de la versión más reciente (OpenVAS 23.30.1 / GVM 22.35.4)

- Integración completa con **GVMD** y **GSA (interfaz web)**.
- Base de datos de NVTs mantenida y actualizable mediante **greenbone-feed-sync**.
- Soporte para autenticación avanzada en Windows y Linux.
- Escaneo de múltiples hosts simultáneamente con control de puertos y límites de concurrencia.
- Informes personalizables con CVSS y clasificación de riesgos.
- Sistema modular que permite agregar nuevas familias de NVTs y configuraciones de escaneo.
- Uso de **Redis y PostgreSQL** para gestión eficiente de tareas y resultados.
- Compatible con auditorías de red, aplicaciones web y servicios internos.

---

> Esta cheatsheet está pensada como referencia rápida para analistas de seguridad que utilizan OpenVAS en entornos de laboratorio o auditoría profesional.
