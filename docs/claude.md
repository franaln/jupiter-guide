# Claude


## Claude Code

Claude Code is already installed. You can go to your project/repo directory and type "claude"

```
cd /path/to/repo
claude
```

Tambien se puede usar desde otra maquina conectandose por ssh.



## MCPs utiles


### Rucio y AMI para usuarios de ATLAS

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
claude mcp add --scope user mgpd -- mgpd-mcp --allow-config-write --allow-prepare --allow-analysis
```

### RooAgent

```bash
claude mcp add --scope user rooagent -- rooagent-mcp
```