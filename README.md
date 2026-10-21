# SerialInsight 2.0

Versión web de SerialInsight, herramienta interna para automatizar la gestión y corrección de logs de pruebas funcionales. Elimina el proceso manual de buscar, editar y transferir logs de los equipos al servidor final, y agiliza el envío de unidades a reparación. Se integra con Shopfloor para validar la estación actual del número de serie antes y después de cada movimiento.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Flask](https://img.shields.io/badge/Framework-Flask-green)
![Server](https://img.shields.io/badge/Server-Waitress-red)
![Status](https://img.shields.io/badge/Status-Production-success)

- [Interfaz y funcionalidades](Funcionalidades.md)
- [Versión anterior (SerialInsight 1.0)](https://github.com/MrAleex3/SerialTrace-for-Foxconn)

![Vista principal](https://github.com/user-attachments/assets/9217e677-aa8e-47f7-bc6e-54750c0a9518)

## Origen del proyecto

SerialInsight nació como solución a un proceso que se había vuelto tedioso, confuso y problemático: mover logs de unidades desde un servidor de pruebas funcionales hasta el servidor de la siguiente estación. Constantemente teníamos problemas por enviar logs incorrectos o duplicarlos accidentalmente, así que decidí crear una herramienta para erradicar ese tipo de confusiones.

Al principio la herramienta era muy básica. Empezó como un script de AutoHotkey que automatizaba el proceso con solo ingresar el número de serie y seleccionar la acción deseada. Funcionó así durante casi medio año, con un launcher `.bat` que se conectaba a una ruta de mi servidor local y copiaba la última versión de la aplicación para que todos los usuarios tuvieran la versión actualizada.

Para evitar problemas de ciberseguridad por estar distribuyendo y ejecutando archivos `.exe` en una red corporativa, decidí migrarla a una plataforma web. SerialInsight fue mi primera aplicación web y sirvió como base e inspiración para crear la suite de herramientas actual, como FVS Monitor.

El objetivo principal de esta herramienta, y de las que le siguieron, es optimizar y facilitar el trabajo diario: dejar de navegar entre carpetas, servidores y páginas web distintas, reducir el proceso a unos cuantos clics y eliminar el problema de buscar, actualizar y enviar logs entre servidores, concentrando toda la información, los logs y el historial en una sola pantalla.

Con la versión web se conservó la misma funcionalidad del script original y se agregaron la integración con Shopfloor, el control de accesos, los logs de auditoría, el tablero de anuncios y la validación de datos para evitar capturar información incorrecta por error humano.

El desarrollo de SerialInsight 1.0, el script, comenzó el 20 de junio de 2025. Esta versión web inició sus primeras pruebas en piso el 4 de enero de 2026 y actualmente acumula más de 16,000 logs generados.

## Puesta en marcha

SerialInsight lee los logs directamente desde las carpetas de red donde las estaciones de prueba suben sus archivos. Solo hay que dar acceso a esas rutas y levantar la aplicación.

**1. Mapear las rutas de red**

El equipo donde correrá el sistema debe tener conexión y permisos de lectura hacia las unidades de red o servidores de las estaciones de prueba.

**2. Configurar las rutas**

En el archivo `rutas.ini` se definen las direcciones a monitorear. Se pueden agregar tantas rutas como se necesiten y activarlas o desactivarlas con el parámetro `Enabled`.

```ini
[General]
Description = Lista de rutas SerialInsight

[Route_1]
Path = \\RutaDeServidor\EquipoPruebas
Enabled = True

[Route_2]
Path = \\RutaDeServidor\EquipoPruebas
Enabled = True
```

**Requisitos**

- Windows 10 o superior.
- Acceso a las rutas de red del sistema de producción.
- Python 3.9 o superior, con Flask y Waitress.

La aplicación se abre en el puerto 10001.

**Estructura del proyecto**

```text
SerialInsight/
├── ServerPass.py         # servidor Flask y lógica de la aplicación
├── Modelo.ini            # modelos y rutas de entrada y salida
├── templates/            # login y tablero
└── static/               # CSS, JS y fuentes
```

## Características

- Búsqueda inteligente de logs: modo dual para buscar en 2 servidores e identificación automática del archivo más reciente.
- Historial extendido (PPID+): rastreo de un serial específico en logs de hace 7 hasta 30 días.
- Gestión de debug y validaciones PASS/FAIL: generación de resultados y detección de equipos en estado de depuración.
- Integración con Shopfloor: consulta el estado y la estación de la unidad antes y después de cada movimiento.
- Control de accesos: registro y control de usuarios.
- Logs de auditoría: registro de quién y cuándo generó un flujo.
- Tablero de anuncios: notificaciones de cambios en la plataforma y consejos de uso.
- Validación de datos: filtros para evitar capturar información incorrecta por error humano.

## Autor

Alejandro Espinoza
Foxconn México
