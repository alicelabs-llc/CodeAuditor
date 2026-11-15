# Auditoría de agentes — AliceLabs LLC

## Alcance
Workflow: [agent-security-audit.yml](.github/workflows/agent-security-audit.yml)

- `alicelabs-llc/universal-trust-adapter`: implementación principal UTA/ATC.
- `alicelabs-llc/atc-verifier`: repositorio de transición; el README indica que se trasladó a UTA.
- `alicelabs-llc/MARKETNOW`: plataforma MarketNow.

## Qué comprueba
- Semgrep: análisis estático y búsqueda de secretos. Se usa `--error` para fallar ante hallazgos.
- pip-audit: dependencias Python **solo cuando existe requirements.txt en la raíz**.
- npm audit: dependencias JavaScript **solo cuando existe package-lock.json en la raíz**.
- Guarda resultados JSON, resumen y SHA de checkout del repositorio auditado como artefactos de Actions.

## Cómo ejecutarlo
Abrir [Actions](https://github.com/alicelabs-llc/CodeAuditor/actions), elegir **AliceLabs agent security audit** y pulsar **Run workflow**. También se programa cada lunes a las 07:15 UTC, y se activa al modificar su propio workflow en main.

## Interpretación
- Que un job termine correctamente **no certifica la seguridad**.
- Si falta un archivo de dependencias en la raíz, ese análisis se omite; no significa ausencia de vulnerabilidades.
- El escaneo no cubre automáticamente subproyectos anidados, pruebas dinámicas, ataques contra prompts ni servidores MCP en ejecución.
- La instalación de escáneres y acciones externas todavía requiere fijar versiones inmutables y revisar la cadena de suministro.
- Antes de declarar la auditoría completa, verificar cada ejecución, sus artefactos y el SHA exacto del objetivo. Un informe técnico debe distinguir resultados limpios, hallazgos, errores y análisis omitidos.

© 2026 AliceLabs LLC
