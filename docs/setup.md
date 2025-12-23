# Guía de Configuración y Despliegue (Setup)

Este documento detalla los pasos técnicos necesarios para replicar el entorno de automatización.

## 1. Importación del Workflow
1. Descargue el archivo `workflow.json` desde la raíz de este repositorio.
2. En su instancia de **n8n**, haga clic en el menú lateral y seleccione **"Import from File"**.
3. Seleccione el archivo descargado para cargar la estructura de nodos.

## 2. Configuración de Credenciales
El flujo requiere una API Key de **fal.ai**. Siga estos pasos:
1. Obtenga su clave en el dashboard de fal.ai.
2. En n8n, abra los nodos `HTTP Request`, `HTTP Request1`, `HTTP Request3` y `HTTP Request4`.
3. En la sección **Authentication**, elija **Header Auth**.
4. Configure los campos:
   - **Name:** `Authorization`
   - **Value:** `Key SU_API_KEY_AQUI`

## 3. Lógica de Tiempos (Wait Nodes)
Para asegurar la estabilidad del sistema, se han configurado los siguientes intervalos:
- **Wait (Inicial):** 90 segundos para dar tiempo al servidor de Kling de iniciar el renderizado.
- **Wait1 (Polling):** 20 segundos entre cada consulta de estado si el video aún no está listo.

## 4. Descarga del Resultado
Al finalizar con éxito, el video se almacena como un objeto binario en el nodo `HTTP Request2`. Para guardarlo en su Mac:
1. Haga clic en el nodo `HTTP Request2`.
2. Vaya a la pestaña **Binary**.
3. Haga clic en el botón de descarga del archivo.
