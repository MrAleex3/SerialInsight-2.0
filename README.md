<h1 align="center">SerialInsight 2.0</h1>

<p align="center">
  Una actualización para mi herramienta interna desarrollada para automatizar la gestión y corrección de logs de pruebas funcionales. Eliminar el proceso manual de buscar, editar y transferir logs de equipos al servidor final y agiliza el envío de unidades a reparación. Se integra con Shopfloor para validar la estacion actual del numero de serie de la unidad antes y después de cada movimiento, todo desde una interfaz web moderna.
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="Funcionalidades.md">Interfaz y funcionalidades</a> ·
  <a href="#estructura-del-proyecto">Estructura</a> ·
  <a href="https://github.com/MrAleex3/SerialTrace-for-Foxconn">Versión Anterior</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9%2B-blue" alt="Python">
  <img src="https://img.shields.io/badge/Framework-Flask-green" alt="Flask">
  <img src="https://img.shields.io/badge/Server-Waitress-red" alt="Server">
  <img src="https://img.shields.io/badge/Status-Production-success" alt="Status">
</p>

<p align="center">
<img width="1347" height="680" alt="image" src="https://github.com/user-attachments/assets/9217e677-aa8e-47f7-bc6e-54750c0a9518" />
</p>

---

## El Origen del Proyecto

SerialInsight nació como solución a un proceso que se había vuelto tedioso, confuso y problemático: mover logs de unidades desde un servidor de pruebas funcionales hasta el sevidor de la siguiente estacion. Constantemente lidiábamos con problemas por enviar logs incorrectos o duplicarlos accidentalmente, por lo que me me dio la idea de crear una herramienta para tratar de erradicar este tipo de confusiones.

Al principio, la herramienta era muy básica. Empezó como un script de *AutoHotKey* que automatizaba el proceso con solo ingresar el número de serie y seleccionar la acción deseada. Funcionó así durante casi medio año, utilizando un launcher `.bat` que se conectaba a una ruta de mi servidor local y copiaba la última versión de la aplicación para que todos los usuarios tuvieran la version actualizada.

pero para evitar problemas de cyberseguridad por estar distribuyendo y ejecutando archivos `.exe` en una red corporativa, decidí migrarla a una plataforma web. **SerialInsight fue mi primera aplicación web** y sirvió como la base e inspiración para crear toda mi suite de herramientas actuales (como FVS Monitor). 

El objetivo principal de esta herramienta (y de todas las que le siguieron) es optimizar y facilitarnos "la vida" en el trabajo. Buscando que dejemos de navegar entre un montón de carpetas, servidores y páginas web distintas, facilitando el proceso a unos cuantos clicks y eliminando el principal problema que teniamos que era el problema de buscar, actualizar y enviar logs entre servidores. Concentrando toda la informacion, logs e historial en una sola pantalla, a un solo click.

Con esta actualización web se conservó exactamente la misma funcionalidad que el script original, pero se agregaron nuevas características como:

- **Integración con Shopfloor:** Consulta el estado y la estación de la unidad antes y después de realizar el proceso.
- **Control de accesos:** Registro y control de usuarios.
- **Logs de Auditoría:** Registro de monitoreo para saber quién y cuándo generó un flujo. 
- **Tablero de anuncios:** Un pequeño apartado para notificar cambios en la plataforma, consejos de uso, etc.
- **Validación de datos:** Filtros integrados para evitar colocar información incorrecta por error humano.

> **Nota histórica:** El desarrollo de SerialInsight 1.0 (el script) comenzó el 20 de junio de 2025. Esta nueva versión web inició sus primeras pruebas en piso el 4 de enero de 2026, abriendo camino junto a sus aplicaciones hermanas como *FVS MONITOR* y actualmente con mas de 13,000 logs generados.

---

## Quick Start

Serialinsight funciona leyendo los logs directamente desde las carpetas de red donde las estaciones de pruebas suben sus archivos, solo necesitas darle acceso a esas rutas y levantar la app.

**1. Mapear las rutas de red**  
El equipo donde correra el sistema debe tener conexión y permisos de lectura hacia las unidades de red o servidores de las estaciones de prueba.

**2. Configurar las rutas**  
Abre el archivo `rutas.ini` y define las direcciones a monitorear. Puedes agregar tantas rutas como necesites, apagarlas o encenderlas usando el parametro `Enabled`.

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

## Features

### 1. Busqueda Inteligente de Logs
- **Modo Dual:** Soporte para busqueda en 2 servidores.
- **Lectura en Tiempo Real:** Identifica automaticamente el archivo de log mas reciente en el servidor remoto y filtra la informacion relevante.
- **Visualizacion Clara:** Muestra los datos como el `ID del equipo de prueba`, `Hora`, `Status`, `Prueba` y `Resultado`.

### 2. Historial Extendido (PPID+)
- **Busqueda Profunda:** Puede rastrear un serial especifico en logs de **hace 7 dias o hasta 30 dias atras**.

### 3. Gestion de Debug y Validaciones (PASS/FAIL)
- **Interaccion Directa:** Al hacer doble clic en un resultado, se habilitan acciones que se pueden realizar para ese serial.
- **Inyeccion de Resultados:**
  - **Generar FAIL:** Permite forzar el fallo de una unidad y subir el log actualizado al servidor destino.
  - **Generar PASS:** Permite dar el pase a una unidad.
- **Manejo de System ID (Debug):** Detecta automaticamente los equipos de prueba en estado de depuracion y solicita al usuario el ID correcto antes de procesar el log.

### 4. Auditoría y Seguridad
- **Logging de Eventos:** Cada accion queda registrada en un servidor central de auditoría con:
  - Fecha y Hora.
  - Usuario e IP.
  - Serial e ID del equipo de pruebas utilizado.
