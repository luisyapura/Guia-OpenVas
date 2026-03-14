🛠️ Guía de Instalación: OpenVAS (GVM) en Kali Linux

Este recurso forma parte del proyecto "El Arsenal de un Analista" (Módulo 6 - Máster en Ciberseguridad). Documenta la implementación nativa de Greenbone Vulnerability Management (GVM) sobre Kali Linux, optimizando el rendimiento para auditorías de vulnerabilidades profesionales.

📋 1. Requisitos del Sistema

Para asegurar un escaneo fluido y evitar cuellos de botella en el procesamiento de NVTs (Network Vulnerability Tests), se recomiendan los siguientes parámetros:

CPU: Mínimo 2 núcleos (4 recomendados).

RAM: Mínimo 8GB (GVM consume recursos considerables de PostgreSQL y Redis).

Almacenamiento: 15GB+ libres en /var/lib/gvm para la base de datos de firmas.

SO: Kali Linux Rolling (Totalmente actualizado).

🚀 2. Proceso de Instalación Paso a Paso

Fase A: Actualización de Repositorios

Antes de integrar nuevas herramientas, es imperativo asegurar la integridad de las dependencias existentes.

sudo apt update && sudo apt full-upgrade -y


Fase B: Descarga de Binarios

Instalamos el meta-paquete gvm, que incluye el scanner OpenVAS, el gestor de vulnerabilidades y la interfaz web (GSA).

sudo apt install gvm -y


Fase C: Configuración y Sincronización (Setup)

Este es el paso más crítico. El script gvm-setup descarga los feeds de vulnerabilidades (CVEs, Certs, Scap).

[!WARNING]
Tiempo estimado: 30-60 minutos dependiendo de la conexión a internet. No interrumpas este proceso.

sudo gvm-setup


Al finalizar, el sistema mostrará una contraseña generada automáticamente para el usuario admin.
¡Regístrala de inmediato!

✅ 3. Verificación de la Instalación

Como analistas, no suponemos que la instalación fue exitosa; la verificamos mediante logs y diagnósticos integrados.

sudo gvm-check-setup


Si el resultado muestra It seems like your GVM-23.x.x installation is OK, el entorno está listo para producción.

⚙️ 4. Gestión del Servicio

Para mantener la eficiencia de la máquina de auditoría, gestionamos el ciclo de vida de los servicios manualmente:

Acción

Comando

Descripción

Iniciar

sudo gvm-start

Lanza los servicios y abre la GUI en el puerto 9392.

Detener

sudo gvm-stop

Libera memoria RAM cerrando procesos de PostgreSQL y GVM.

Feed Sync

sudo gvm-feed-update

Sincroniza las últimas vulnerabilidades del día.

🔒 5. Acceso a la Interfaz (GSA)

Una vez iniciado el servicio, accede mediante tu navegador a la consola de Greenbone Security Assistant:

URL: https://127.0.0.1:9392

Usuario: admin

Password: [La generada en el paso 2C]

📝 Notas de Autoría

Este manual ha sido desarrollado para el portfolio de Ciberseguridad bajo licencia MIT. Se prioriza el rigor técnico y la reproducibilidad de la auditoría.
