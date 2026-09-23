# ICN292 — Laboratorio 3: Triage de devoluciones en n8n

**Camilo Rivano Lara** · ROL: 202304534-9 · Semilla S = 249
Profesor: José Luis Sáez Tamayo · UTFSM

Parámetros aplicados: *U = $79.000  y D = 14 días

## Archivos

Archivo Qué es

ICN292-Lab3-Rivano_Camilo.pdf - Informe final 
ICN292-Lab3-Rivano_Camilo.docx - Fuente editable del informe 
triage.json Flujo 1 — clasificación por webhook 
emisor.json Flujo 2 — envía las 15 solicitudes de prueba 
resumen.json Flujo 3 — resumen diario programado

## Cómo reproducirlo

1. Importar. En n8n: menú Workflows → **...** → Import from File... para cada `.json`.

2. Crear la tabla de datos `registro_devoluciones` con las columnas `id_solicitud`, `sku`, `monto`, `ruta`, `motivo`, `U_aplicado`, `D_aplicado`, `uf_valor`, `monto_uf` y `fecha` (las de monto y umbrales en tipo Number, el resto String). Luego volver a seleccionarla en los nodos `GUARDAR_REGISTRO` (triage) y `LEER_REGISTRO` (resumen), porque el identificador interno de la tabla no viaja en el `.json`.

3. Activar el triage. El nodo `Webhook` queda escuchando POST en `https://<instancia>.app.n8n.cloud/webhook/triage-devoluciones`.

4. Probar. En el emisor, pegar esa URL en el nodo `ENVIAR_A_TRIAGE` y pulsar **Execute workflow**: manda las 15 solicitudes una por una. El resultado queda en la tabla de datos.

5. Ver el resumen. Abrir el flujo de resumen y pulsar **Execute workflow** para ejecutarlo a demanda; el nodo `MENSAJE` entrega el total del día, la distribución por ruta y la tasa de aprobación automática.
