# SerialInsight 2.0

Versión web de SerialInsight, herramienta interna para automatizar la gestión y corrección de logs de pruebas funcionales. Elimina el proceso manual de buscar, editar y transferir logs de los equipos al servidor final, y agiliza el envío de unidades a reparación. Se integra con Shopfloor para validar la estación actual del número de serie antes y después de cada movimiento.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Flask](https://img.shields.io/badge/Framework-Flask-green)
![Server](https://img.shields.io/badge/Server-Waitress-red)
![Status](https://img.shields.io/badge/Status-Production-success)

- [Versión anterior (SerialInsight 1.0)](https://github.com/MrAleex3/SerialTrace-for-Foxconn)

![Vista principal](https://github.com/user-attachments/assets/9217e677-aa8e-47f7-bc6e-54750c0a9518)

## Origen del proyecto

SerialInsight nació como solución a un proceso que se había vuelto tedioso, confuso y problemático: mover logs de unidades desde un servidor de pruebas funcionales hasta el servidor de la siguiente estación. Constantemente teníamos problemas por enviar logs incorrectos o duplicarlos accidentalmente, así que decidí crear una herramienta para erradicar ese tipo de confusiones.

Al principio la herramienta era muy básica. Empezó como un script de AutoHotkey que automatizaba el proceso con solo ingresar el número de serie y seleccionar la acción deseada. Funcionó así durante casi medio año, con un launcher `.bat` que se conectaba a una ruta de mi servidor local y copiaba la última versión de la aplicación para que todos los usuarios tuvieran la versión actualizada.

Para evitar problemas de ciberseguridad por estar distribuyendo y ejecutando archivos `.exe` en una red corporativa, decidí migrarla a una plataforma web. SerialInsight fue mi primera aplicación web y sirvió como base e inspiración para crear la suite de herramientas actual, como FVS Monitor.

El objetivo principal de esta herramienta, y de las que le siguieron, es optimizar y facilitar el trabajo diario: dejar de navegar entre carpetas, servidores y páginas web distintas, reducir el proceso a unos cuantos clics y eliminar el problema de buscar, actualizar y enviar logs entre servidores, concentrando toda la información, los logs y el historial en una sola pantalla.

Con la versión web se conservó la misma funcionalidad del script original y se agregaron:

- Integración con Shopfloor: consulta el estado y la estación de la unidad antes y después de realizar el proceso.
- Control de accesos: registro y control de usuarios.
- Logs de auditoría: registro para saber quién y cuándo generó un flujo.
- Tablero de anuncios: apartado para notificar cambios en la plataforma y consejos de uso.
- Validación de datos: filtros para evitar capturar información incorrecta por error humano.

El desarrollo de SerialInsight 1.0, el script, comenzó el 20 de junio de 2025. Esta versión web inició sus primeras pruebas en piso el 4 de enero de 2026 y actualmente acumula más de 13,000 logs generados.

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

## Características

### Búsqueda inteligente de logs

- Modo dual: soporte para búsqueda en 2 servidores.
- Lectura en tiempo real: identifica automáticamente el archivo de log más reciente en el servidor remoto y filtra la información relevante.
- Visualización clara: muestra el ID del equipo de prueba, la hora, el status, la prueba y el resultado en una lista ordenada.

### Historial extendido (PPID+)

- Búsqueda profunda: puede rastrear un serial específico en logs de hace 7 hasta 30 días.

### Gestión de debug y validaciones (PASS/FAIL)

- Interacción directa: al hacer doble clic en un resultado se habilitan las acciones disponibles para ese serial.
- Inyección de resultados:
  - Generar FAIL: fuerza el fallo de una unidad y sube el log actualizado al servidor destino.
  - Generar PASS: da el pase a una unidad.
- Manejo de System ID (debug): detecta automáticamente los equipos de prueba en estado de depuración y solicita al usuario el ID correcto antes de procesar el log.

### Auditoría y seguridad

- Registro de eventos: cada acción queda registrada en un servidor central de auditoría con fecha, hora, usuario, IP, serial e ID del equipo de prueba utilizado.

## Autor

Alejandro Espinoza
Foxconn México
