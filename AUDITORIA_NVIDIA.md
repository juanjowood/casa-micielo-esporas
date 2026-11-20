# Auditoría previa y entrega para Work · 20-11-2026

**Recomendación: CORREGIR antes de promover o fusionar.** Una ejecución real, sin baselines ni reintentos del mismo fallo. El PR propone una mejora acotada; no certifica seguridad ni activa Pages.

## Procedencia y ejecución

- Repositorio objetivo: `juanjowood/casa-micielo-esporas`.
- HEAD analizado, antes de implementar: `77bc8ab5bfb79d5e751afbff3140f0f6935a976e`.
- Fuente oficial: [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector/tree/48e0f942ea1f5fdb7aa096a6f65a0adeda2ecc4e), commit `48e0f942ea1f5fdb7aa096a6f65a0adeda2ecc4e`.
- Versión ejecutada: `SkillSpector v2.12.0`; `--version` y `scan --help` salieron con código 0. Los cinco flags del comando se comprobaron en la ayuda real.
- Instalación exclusiva en `/tmp/casa-skillspector-venv`, desde código oficial descargado en `/tmp/casa-skillspector-source`, mediante `python3 -m venv` y `python -m pip --isolated --disable-pip-version-check --no-cache-dir install /tmp/casa-skillspector-source`. Sin extras MCP, herramientas globales ni instalación de skills. Las dependencias Python fueron resueltas en ese entorno temporal; no se certificó su cadena de suministro.
- Ejecución con entorno vacío salvo PATH, HOME/TMPDIR temporales y tracing LangSmith/LangChain desactivado. Sin credenciales heredadas, proveedor de pago ni servidor MCP. `metadata.llm_requested=false`, `inference_usage=[]`. Los nombres de modelos en el JSON son configuración, no inferencias ejecutadas.

```sh
PATH=/tmp/casa-skillspector-venv/bin:/usr/bin:/bin
# Desde la raíz del checkout del HEAD indicado, con entorno aislado:
skillspector scan . --no-llm --format json --output /tmp/skillspector-report.json --fail-on-findings --fail-on-incomplete
```

**Salida: 1.** `Report saved to: /tmp/skillspector-report.json`.

[JSON original íntegro](evidencia/skillspector-report.json) · [Comando, salida y procedencia](evidencia/ejecucion.json).

SHA-256 del JSON original: `57d61c90b7e74ccc7ea748cbd7148a71dff5d6fa9e9556fb8a0c869bbe5eca98`.

## Aplicabilidad, cobertura y hallazgos

El directorio no contiene `SKILL.md` ni `skill.md`. La versión ejecutada **sí acepta** este directorio: `execution_successful=true`, nombre `unknown`. Su parser devuelve un manifiesto vacío cuando no existe. Por ello el análisis estático documental es válido como ejecución, aunque parcial. **NO APLICABLE:** evaluación de instalación/permisos de un skill y analizadores dependientes de un manifiesto ausente. No se fabricó un skill.

| Dato del informe | Resultado |
| --- | --- |
| Riesgo | 18, LOW; recomendación del escáner CAUTION |
| Severidad máxima de hallazgo | HIGH |
| Componentes en cobertura | 19 (18 archivos versionados + `.git/config`) |
| Completos / parciales / sin inspección | 18 / 1 / 0 |
| Cobertura | 94,7 %, `is_complete=false`, `status=partial` |
| Hallazgos antes/después del filtro heurístico interno | 1 / 1 |
| Suprimidos | 0; sin baseline ni exclusiones solicitadas |

1. **TM2 · Chaining Abuse · HIGH · confianza 0,75**, `PROCEDENCIA.md:29`, columna 142. Fragmento: `; su `. El párrafo explica que el hash no demuestra autoría, eficacia ni licencia; no contiene una cadena de herramientas ejecutable. **Interpretación de esta revisión:** probable falso positivo léxico en prosa española, pendiente de validación independiente. No se cambia esa prosa para silenciar el escáner ni se suprime el hallazgo.
2. **Cobertura incompleta:** `static_patterns_tool_misuse` degradado, `static_parse_limit` / `boundary_unresolved` en `index.html:42–44` del HEAD original (argumentos de comandos). Se conserva el límite completo en el JSON. La revisión manual del script no equivale a reparar la cobertura del escáner.

El JSON inventaría hooks de ejemplo ejecutables creados por `git clone` y declara `has_executable_scripts=true`; su ledger excluye esos hooks y otros metadatos VCS. **No son ejecutables versionados del proyecto.** `.git/config` sí entra en los 19 componentes: no presentar el porcentaje como cobertura de solo los archivos públicos. No se ejecutaron hooks.

No se declara PASS de NVIDIA. Las reglas internas de filtrado son las predeterminadas del escáner, no una baseline aplicada por esta revisión. No se repite el escaneo con el mismo fallo ni se promete cobertura del árbol modificado: el JSON corresponde únicamente al HEAD previo.

## Auditoría estática complementaria y cambio público

Se leyeron los 18 archivos versionados originales, incluidos reglas, JSON, hashes y HTML. Los 17 hashes iniciales coincidieron. No hay manifiesto instalable, dependencias declaradas de aplicación, workflows ni ejecutables versionados. El HTML tiene un solo script: copia texto al portapapeles tras clic; la revisión no encontró llamadas de red, almacenamiento, formularios de envío ni carga de recursos externos. Los enlaces de navegación requieren una acción del visitante.

Los documentos mantienen adopción voluntaria, separación entre lectura y autoridad, permiso distinto para guardar/publicar, y ZIP históricos como datos. No se contrastaron fuentes privadas ni autoría/licencias históricas. Esta revisión estática no prueba comportamiento de otros asistentes, ausencia universal de secretos ni seguridad absoluta.

Cambio lógico de experiencia: hacer compartible la entrada web. Los 12 enlaces documentales apuntan a la vista renderizada de GitHub, utilizable desde una vista local o un futuro hosting estático. El bloque visible incluye la URL pública estable y la invitación; el botón copia ese bloque, evitando compartir `file://`, localhost o una URL de vista previa. Si falta JavaScript o portapapeles, el texto queda seleccionable. Se actualiza únicamente el estado de evaluación en documentación/manifiesto, sin resolver licencia ni alterar controles administrativos.

## Verificación y límites de entrega

- Comprobaciones estáticas: destinos de enlaces HTML cotejados con archivos del checkout, enlaces Markdown locales existentes, JSON válido, IDs y referencias del script presentes; sin recursos externos automáticos. [Resultados](evidencia/verificacion.json).
- Tres escenarios del botón ejecutados con Node `vm` y DOM/portapapeles simulados: éxito, permiso denegado y API ausente. En los tres se comprobó ausencia de escritura antes del clic; éxito copia el bloque exacto, los errores muestran alternativa manual. No equivale a prueba en un navegador real. [Resultados](evidencia/copia-resultados.json).
- Integridad del árbol final: `shasum -a 256 -c SHA256SUMS.txt`; formato del diff: `git diff --check`. La lista de hashes cubre todos los archivos de la entrega salvo ella misma.
- No se probó visualmente en navegador, ni con usuarios externos, ni en Pages desplegado. Las referencias `blob/main` verán la versión fusionada si un humano aprueba el PR; el checkout permite revisar los cambios antes.
- El conector GitHub confirmó permisos `push`; GitHub CLI devolvió 401 y se abandonó esa vía. Un único PR en rama aislada, sin merge ni force push. No se modifican licencias, otros repositorios, Pages, Discussions ni configuración administrativa.

**Una acción siguiente:** Work debe revisar independientemente el PR y resolver el TM2 y el límite de cobertura con evidencia antes de recomendar GO. Esta entrega recomienda **CORREGIR**, no trasladar el CAUTION del escáner a una aprobación humana automática.
