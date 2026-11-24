# Claude



- Claude Code is already installed. You can go to your project/repo directory and type "claude"

```
cd /path/to/repo
claude
```

- Tambien se puede usar desde otra maquina con la aplicacion desktop, conectandose por ssh.


## atlas-utils plugin

Incluye herramientas e instrucciones compartidas para ATLAS:

- **Tareas de PanDA:** estado, progreso, jobs fallidos agrupados por error, retry/kill (Claude siempre pregunta antes).
- **Outputs:** nombres de los containers de salida de las tareas terminadas y la lista para descargar.
- **Rucio:** tamaños, cantidad de archivos, eventos, réplicas y reglas, con el servidor MCP `rucio-atlas` (solo lectura).
- **AMI:** metadatos de datasets, secciones eficaces y AMI tags, con el servidor MCP `ami`.
- **Problemas conocidos:** chequeo del proxy VOMS y tareas trabadas en `pending` ("brokerage failed").

### Instalación

1. Agregá el plugin `atlas-utils`. Abrí <https://claude.ai/customize/plugins/plugin_017rkacj7nB91rajL94jA2Zd> y agregalo ahí, o
   desde una terminal:

   ```bash
   claude plugin marketplace add --claudeai claudeai-organization-library
   claude plugin install atlas-utils@claudeai-organization-library
   ```


2. Si ya habías configurado vos los servidores MCP de Rucio/AMI, borrá tus copias para que las herramientas no se carguen dos veces (el plugin ya los registra):

   ```bash
   claude mcp remove rucio-atlas -s user
   claude mcp remove ami -s user
   ```

3. Abrí una sesión nueva. Los plugins y sus actualizaciones se cargan al iniciar la sesión.

### Antes de usarlo

- **Proxy VOMS (para Rucio y AMI):**

  ```bash
  setupATLAS
  voms-proxy-init -voms atlas -valid 96:00
  ```

  Claude revisa el proxy antes de usar Rucio/AMI y te pide que lo renueves, pero no puede
  escribir tu contraseña. Si Rucio dice "Cannot connect to the Rucio server", casi seguro que
  el proxy está vencido.
- **Login en bigpanda (de vez en cuando):** la primera consulta de tareas muestra un link
  `https://atlas-auth.cern.ch/device?...`. Corré en una terminal el comando que te da Claude,
  abrí el link, iniciá sesión y respondé `y`. El token se guarda en `~/.pathena/.token`.
- **Cuenta de Rucio:** si no coincide con tu usuario de jupiter, definí `RUCIO_ACCOUNT` antes
  de abrir Claude.

### Ejemplos de uso:

- "Revisá mis jobs de la grid"
- "¿Por qué falló la tarea 12345678?"
- "¿Cuánto ocupan los ntuples v02 y dónde están?"
- "Dame la lista para descargar con rucio de las tareas terminadas"
- "¿Por qué esta tarea sigue en pending?"


## MCPs


### Rucio y AMI para usuarios de ATLAS

!! warning ""
    * Ya estan incluidos en atlas-utils plugin, no instalar de nuevo

Hay dos servidores MCP instalados que le permiten a Claude Code consultar **Rucio** (datasets, réplicas, reglas) y **AMI** (metadata, secciones eficaces, tags). Los dos son de solo lectura.

- Agregá los MCP a Claude Code (una sola vez):

    ```bash
    claude mcp add --scope user rucio-atlas -- rucio-mcp-atlas
    ```

    ```bash
    claude mcp add --scope user ami -- ami-mcp-atlas
    ```

!!! note ""
    Si tu cuenta de Rucio no es igual a tu usuario de `jupiter`, agregá `-e RUCIO_ACCOUNT=<tu_cuenta>` en el primer `claude mcp add`.

- Antes de usarlos generar el proxy o actualizarlo (y repertir cada vez que este vencido):

    ```bash
    voms-proxy-init -voms atlas
    ```


### mgpd

```bash
claude mcp add --scope user mgpd -- mgpd-mcp --allow-config-write --allow-prepare --allow-merge --allow-execute --allow-analysis
```

| Options | Actions |
| --- | --- |
| `--allow-config-write` | Create/copy projects, create analysis starters and save reviewed YAML edits |
| `--allow-prepare` | Prepare productions and selected recoveries |
| `--allow-execute` | Submit prepared productions to Condor |
| `--allow-merge` | Merge validated outputs |
| `--allow-analysis` | Run reviewed analyses of existing outputs (never generation or submission) |

### RooAgent

```bash
claude mcp add --scope user rooagent -- rooagent-mcp
```