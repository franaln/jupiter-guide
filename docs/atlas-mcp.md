# MCP de ATLAS para Claude Code

En `jupiter` hay dos servidores MCP que le permiten a Claude Code consultar
**Rucio** (datasets, réplicas, reglas) y **AMI** (metadata, secciones eficaces, tags).
Los dos son de solo lectura.

## Configuración

1. Generá tu proxy (no hace falta `setupATLAS`):

    ```bash
    voms-proxy-init -voms atlas
    ```

2. Agregá los MCP a Claude Code (una sola vez):

    ```bash
    claude mcp add --scope user rucio-atlas -- rucio-mcp-atlas
    ```

    ```bash
    claude mcp add --scope user ami -- ami-mcp-atlas
    ```

!!! note
    Si tu cuenta de Rucio no es igual a tu usuario de `jupiter`, agregá
    `-e RUCIO_ACCOUNT=<tu_cuenta>` en el primer `claude mcp add`.

Cuando venza el proxy, repetí el paso 1.
