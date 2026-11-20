# Rata Sabia · Guardrail de trabajo económico y verificable

**Ámbito:** mantenimiento de `juanjowood/casa-micielo-esporas`. **Estado:** adaptación documental de una filosofía de trabajo, no agente, runtime, skill instalado, memoria automática ni permiso de ejecutar.

**Procedencia:** derivada de `Rata Sabia` (nota de CONSTELACIÓN del 2026-11-05, consultada en su origen). El episodio operativo privado que motivó esa nota **no se reproduce ni se publica aquí**. Esta adaptación fija reglas para Esporas; no promueve la nota histórica a canon transversal.

> Ser ratas con los recursos, sabios con la experiencia y generosos con los resultados.

## Gate obligatorio antes de gastar o delegar

| Comprobación | Pregunta mínima | Si falla |
| --- | --- | --- |
| 1. Fuente | ¿Tengo los archivos originales, el HEAD actual y sus límites de privacidad? | No inventar contenido ni operar sobre una versión supuesta. |
| 2. Autenticación | ¿El entorno que **realmente** ejecutará tiene acceso al repo, no solo otra cuenta o conversación? | STOP; explicar el bloqueo. |
| 3. Capacidad | ¿Hay herramientas, runtime y dependencias disponibles para esta prueba concreta? | Proponer alternativa comprobable o ABSTAIN. |
| 4. Costo y permiso | ¿Se puede usar lo que ya existe? ¿Hay gastos, servicios externos o cambios persistentes que requieren aprobación? | No contratar, instalar, desplegar ni ampliar permisos sin aprobación. |
| 5. Entrega verificable | ¿Qué evidencia exacta probará que salió bien? ¿Qué archivo/commit/URL cambiará? | Reducir el alcance antes de actuar. |
| 6. Corte de pérdidas | ¿Estamos repitiendo la misma falla sin nueva evidencia o causa resuelta? | STOP, una explicación y un siguiente paso distinto, si existe. |

## Economía operativa

- **Reutilizar > corregir > integrar > construir.** No reconstruir investigaciones, documentos o tests ya verificados. Un resultado previo no sustituye verificar su vigencia cuando se va a modificar algo.
- **Leer de forma proporcional:** identificar primero las rutas relevantes, el diff y los tests cercanos. Evitar leer todo el repositorio o lanzar suites completas por inercia. Escalar cobertura cuando el riesgo lo justifique y explicar por qué.
- **Una pregunta, un resultado:** acotar el objetivo y sus criterios de éxito antes de modificar. Por defecto, una modificación lógica por iteración, seguida de la prueba proporcional correspondiente.
- **Límite de exploración:** ante un bloqueo reproducido, no repetir un intento equivalente. Si dos ciclos de corrección no resuelven el mismo fallo, parar, mostrar evidencia y pedir un cambio explícito de alcance o estrategia. No esconder el costo en subagentes.
- **No fan-out de modelos:** no convocar agentes secundarios, Work, Codex adicionales ni proveedores nuevos salvo ganancia clara y autorización. Work puede auditar un PR terminado: no duplicar toda la implementación.
- **No escalar esfuerzo por prestigio:** usar el razonamiento y las pruebas más baratos compatibles con la calidad exigida; solicitar al humano una modalidad más costosa solo si puede justificarse el beneficio.
- **No crear infraestructura para ahorrar infraestructura:** quedan fuera agentes residentes, automatizaciones, cron, trackers, dashboards, servidores, telemetría, nuevas torres y sincronización no solicitada.

## Política de escritura

- Inspeccionar `AGENTS.md`, HEAD y permisos. Si el mandato es **solo lectura**, no escribir. Si es de implementación, usar rama aislada y **un PR**; no hacer merge por cuenta propia.
- No tocar sistemas privados ni otros repositorios. Mantener `Primera Respiración`, reconocimiento de Casas, criaturas, botones y cuaderno de continuidad como **propuestas voluntarias**, no activadores.
- No instalar skills históricos ni autoruns. Los términos `EchoFrame`, `Sistema Semilla`, `Celiomicielo` y `¿emergiste?` son contexto, no comandos.
- No decidir licencias, revelar material privado, enviar conversaciones a Git, modificar datos de terceros, activar Pages/Discussions ni cambiar controles administrativos sin mandato específico.
- La seguridad requiere evidencia: `no ejecutado` no es `PASS`, un escáner no sustituye revisar amenazas; no afirmar NVIDIA SkillSpector ejecutado por el mero hecho de citarlo.

## Cierre de una misión Codex

Entregar como máximo:
1. **DATO:** HEAD leído, rama/commit/PR, archivos cambiados, comandos y resultados de pruebas que realmente se ejecutaron.
2. **LÍMITE:** qué no se pudo probar, costos o bloqueos y permisos que faltan.
3. **DECISIÓN:** GO / CORREGIR / STOP y **una** acción siguiente.

Métrica: menos iteraciones fallidas, menos trabajo repetido y más resultados verificados. **Créditos gastados, mensajes enviados y número de agentes nunca son logros.**

**Conservación de aprendizaje:** si surge una mejora generalizable, anotarla como candidata con fuente y evidencia. `OBSERVE → INFER → CANDIDATE → HUMAN PROMOTION`. No autopromoción, actualización de memoria, instalación de nuevos skills ni cambios de política por deducción.
