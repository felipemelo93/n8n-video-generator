# n8n-video-generator

Workflow de automatización para la generación de video mediante IA, desarrollado para la prueba técnica del **Grupo ICC**. El sistema integra n8n con la API de Kling (vía fal.ai).

## 🚀 Visión General
Este proyecto resuelve la generación asíncrona de video, implementando un sistema de **polling manual** (espera y re-intento) para gestionar los tiempos de procesamiento de la IA de forma eficiente.

## 📂 Estructura del Proyecto
* `workflow.json`: Exportación completa del flujo de n8n.
* `/docs`: 
    * `setup.md`: Instrucciones detalladas de configuración.
    * `analisis-costes.md`: Análisis económico y técnico.
    * `experimentos.md`: Bitácora de pruebas de prompts.
* `/assets`: 
    * `imagen-base.png`: Input utilizado para la generación.
    * `video-final.mp4`: Resultado obtenido (9.42 MB).
    * `/screenshots`: Evidencias de la ejecución exitosa de los nodos.

## 🛠️ Cómo Ejecutar
1. **Importación:** Cargue el archivo `workflow.json` en su instancia de n8n.
2. **Credenciales:** Configure su API Key de fal.ai en los nodos "HTTP Request" (Header Auth: `Authorization`).
3. **Trigger:** Ejecute el workflow e introduzca los parámetros:
   - `image_url`: URL de la imagen.
   - `prompt`: Descripción del movimiento.

## 📝 Notas de Implementación
* **Sistema de Polling:** Se implementó una lógica de bucle con nodos `Wait` y un nodo `IF`. Si el estado no es `COMPLETED`, el flujo re-intenta la consulta a través de `HTTP Request4`.
* **Manejo de Errores:** El nodo `IF` detecta el estado `FAILED` para detener la ejecución y evitar consumos innecesarios de créditos.
