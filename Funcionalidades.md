# Interfaz y funcionalidades

---

## Vista principal

Pantalla de búsqueda de logs por número de serie, con el historial de pruebas y las acciones disponibles para cada resultado.

<p align="center">
  <img src="https://github.com/user-attachments/assets/9217e677-aa8e-47f7-bc6e-54750c0a9518" alt="Vista principal" />
</p>

---

## Búsqueda inteligente de logs

- Modo dual: búsqueda en 2 servidores.
- Lectura en tiempo real: identifica automáticamente el archivo de log más reciente en el servidor remoto y filtra la información relevante.
- Visualización clara: muestra el ID del equipo de prueba, la hora, el status, la prueba y el resultado en una lista ordenada.

---

## Historial extendido (PPID+)

- Búsqueda profunda: rastrea un serial específico en logs de hace 7 hasta 30 días.
- Análisis multiarchivo: opera sobre varios logs históricos según patrones de fecha para encontrar todas las ocurrencias de una unidad.

---

## Gestión de debug y validaciones PASS/FAIL

- Interacción directa: al hacer doble clic en un resultado se habilitan las acciones disponibles para ese serial.
- Generar FAIL: fuerza el fallo de una unidad y sube el log actualizado al servidor destino.
- Generar PASS: da el pase a una unidad.
- Manejo de System ID: detecta automáticamente los equipos de prueba en estado de depuración y solicita el ID correcto antes de procesar el log.

---

## Integración con Shopfloor

Consulta el estado y la estación de la unidad antes y después de realizar el proceso, para validar que el movimiento corresponda.

---

## Control de accesos y auditoría

- Registro y control de usuarios.
- Cada acción queda registrada en un servidor central de auditoría con fecha, hora, usuario, IP, serial e ID del equipo de prueba utilizado.

---
<p align="center">
  <a href="README.md">Volver al README principal</a>
</p>
