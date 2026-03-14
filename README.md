# 🔍 ¿Qué es OpenVAS? Conceptos y Contexto Histórico

Este documento proporciona el trasfondo teórico necesario para entender **OpenVAS (Open Vulnerability Assessment System)** como componente central del arsenal de un analista de ciberseguridad.

---

## 1. Definición Técnica

OpenVAS es un **motor de escaneo de vulnerabilidades de código abierto** que constituye el núcleo del framework **Greenbone Vulnerability Management (GVM)**. Se utiliza para identificar:

- Fallos de seguridad
- Configuraciones erróneas
- Parches faltantes en activos de red, servidores y aplicaciones

A diferencia de otros escáneres, OpenVAS se basa en una **comunidad activa** que mantiene una **base de datos de pruebas de vulnerabilidad** (NVTs - *Network Vulnerability Tests*) en constante actualización.

---

## 2. Breve Historia: El Origen de una Alternativa Libre

La historia de OpenVAS está intrínsecamente ligada a la de **Nessus**, otro de los escáneres más conocidos en la industria.

1. **El Inicio (2005):**  
   Nessus era originalmente un proyecto de código abierto. En octubre de 2005, la empresa **Tenable Network Security** cambió su licencia a propietaria (*closed source*).

2. **El Fork:**  
   En respuesta a este cambio, la comunidad de software libre realizó un fork de la última versión GPL de Nessus, bautizado inicialmente como **GNessUs**.

3. **Evolución a OpenVAS:**  
   Tras varios años de desarrollo independiente, el proyecto pasó a llamarse **OpenVAS**.

4. **Greenbone Networks:**  
   Desde 2008, la empresa alemana **Greenbone Networks** se convirtió en el principal contribuyente y desarrollador del proyecto, estructurándolo bajo la arquitectura **GVM (Greenbone Vulnerability Management)** que conocemos hoy.

---

## 3. ¿Para qué sirve en una Auditoría?

En el marco de un **ciclo de gestión de vulnerabilidades**, OpenVAS cumple funciones críticas:

- **Identificación de Activos:**  
  Escaneo de rangos de red para descubrir servicios activos (HTTP, SSH, SMB, etc.).
- **Detección de Vulnerabilidades Conocidas (CVE):**  
  Cruza la información del sistema objetivo con miles de firmas para identificar CVEs específicos.
- **Auditoría de Configuraciones:**  
  Verifica si los servicios están configurados siguiendo las mejores prácticas (ej. cifrados débiles o contraseñas por defecto).
- **Gestión de Riesgos:**  
  Clasifica los hallazgos según su criticidad (Baja, Media, Alta, Crítica) basándose en el estándar **CVSS**.
- **Generación de Reportes:**  
  Permite exportar los resultados en múltiples formatos (*PDF, XML, CSV*) para su posterior análisis y remediación.

---

## 4. Diferenciación: OpenVAS vs GVM

Es común confundir ambos términos:

- **OpenVAS:**  
  Estrictamente el **scanner**, el motor que realiza las pruebas de vulnerabilidad.
- **GVM (Greenbone Vulnerability Management):**  
  El framework completo que incluye:
  - La base de datos (**PostgreSQL**)  
  - La interfaz web (**GSA**)  
  - El gestor de sesiones (**GVMD**)

---

## 📝 Notas de Autoría

- **Proyecto:** El Arsenal de un Analista - Módulo 6  
- **Referencia:** Documentación oficial de Greenbone Networks y registros históricos de la comunidad OSS
