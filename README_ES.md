````markdown
# Supervisor de Router con ESPHome

## Visión General

Este proyecto utiliza ESPHome en un ESP8266 para monitorear la conectividad a Internet de tu router mediante el establecimiento periódico de una conexión TCP a 8.8.8.8 en el puerto 53. Si tres verificaciones consecutivas de conectividad fallan, el firmware activa un reinicio del router a través de un relé conectado. Después de dos intentos de reinicio, el sistema entra en un período de bloqueo de 30 minutos antes de volver a intentarlo, ayudando a prevenir ciclos continuos de reinicio.

## Características

- **Monitoreo Automático de Conectividad:** Verifica la conectividad cada 60 segundos.
- **Reinicio Automático:** Activa un reinicio del router mediante un relé tras tres fallos consecutivos.
- **Mecanismo de Bloqueo:** Después de dos intentos de reinicio, entra en un período de bloqueo de 30 minutos antes de intentar nuevamente.
- **Integración con ESPHome:** Se gestiona fácilmente mediante el ESPHome Dashboard o Home Assistant.

## Requisitos de Hardware

- Placa ESP8266 (por ejemplo, esp01s)
- Módulo de relé (para controlar el encendido/reset del router)
- Cableado y fuente de alimentación adecuados

## Requisitos de Software

- [ESPHome](https://esphome.io/)
- ESPHome Dashboard o herramienta de línea de comandos para cargar firmware y ver logs

## Instalación

1. **Clona este repositorio:**
   ```bash
   git clone https://github.com/jpucheu/supervisor.git
   cd supervisor
   ```
2. **Edita el archivo YAML:**
   - Abre `supervisor.yaml` y actualiza las credenciales de WiFi.
   - Ajusta las asignaciones de pines de hardware si es necesario.
3. **Compila y Sube el Firmware:**
   ```bash
   esphome supervisor.yaml run
   ```
4. **Monitorea los Logs:**  
   Usa el ESPHome Dashboard o ejecuta:
   ```bash
   esphome supervisor.yaml logs
   ```
   para asegurarte de que las verificaciones de conectividad y la lógica de reinicio funcionen correctamente.

## Configuración

- **Verificación de Conectividad:**  
  El script intenta una conexión TCP a 8.8.8.8 en el puerto 53 cada 60 segundos.
- **Control del Relé:**  
  El relé está conectado a GPIO0 y se activa durante 15 segundos durante un intento de reinicio.
- **Período de Bloqueo:**  
  Tras dos intentos de reinicio, el sistema espera 30 minutos antes de reiniciar los contadores y reanudar la operación normal.

## Solución de Problemas

- Verifica que el ESP8266 esté correctamente conectado a tu red WiFi.
- Asegúrate de que el cableado del relé sea correcto.
- Revisa los logs de ESPHome para mensajes que indiquen el estado de la conectividad y los intentos de reinicio.
- Ajusta los intervalos y umbrales en el archivo YAML según las necesidades de tu entorno de red.

## Contribuciones

¡Se agradecen las contribuciones! Por favor, abre un issue o envía un pull request con mejoras o correcciones de errores.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT.
