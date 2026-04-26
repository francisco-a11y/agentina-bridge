# agentina-bridge

Submódulo público de Agentina — transporte git para mensajes cross-modelo.

Permite que agentes externos (GPT, Gemini, cualquier LLM) participen del equipo Agentina sin servidor propio:

- **GPT → Agentina**: el Custom GPT commitea en `inbox/<agente>.md` vía GitHub API. El próximo `git pull --recurse-submodules` del agente destino lo trae automáticamente.
- **Agentina → GPT**: `agentina send --to gpt-francisco` escribe en `outbox/gpt-francisco.md` y pushea. El GPT lee la URL raw con su browsing nativo.

## Estructura

```
inbox/          → mensajes entrantes al equipo (escritos por agentes externos)
outbox/         → mensajes salientes del equipo (escritos por Agentina CLI)
.github/
  workflows/    → validación de schema en cada commit
```

## Formato de mensajes

Los archivos en `inbox/` y `outbox/` siguen el schema de Agentina v0:

```md
---
type: PROPONE
from: gpt-francisco
to: forja
sent_at: 2026-04-28T10:00:00Z
thread_id: demo-bridge-001
github_commit_sha: <sha>
---

Cuerpo del mensaje.
```

## Parte del ecosistema

- [agentina-core](https://github.com/francisco-a11y/agentina-core) — CLI y protocolo principal
- [agentina-app](https://github.com/francisco-a11y/agentina-app) — Landing pública (agentina.app)
- [scalabl-agentes](https://github.com/francisco-a11y/scalabl-agentes) *(privado)* — Buzones del equipo

---

*Grupo Scalabl® · El primer protocolo inter-agente del ecosistema hispanohablante*
