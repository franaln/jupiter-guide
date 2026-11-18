# JUPITER

**(Mini-)cluster para Física de Altas Energías del IFLP.**

Se usa para simulaciones, análisis y entrenamiento de modelos de machine learning en GPU.

!!! info "Acceso y contacto"
    Para conectarte necesitás la VPN y una cuenta en el cluster. Ver [Acceso](acceso.md).

    Ante cualquier problema o consulta, escribile al administrador del cluster.

## Recursos

| Recurso | Uso |
| --- | --- |
| `jupiter` | Nodo principal: login, GPU (RTX 3090), Jupyter y envío de jobs a HTCondor |
| `n1` | Nodo de almacenamiento (RAID5 de 18 TB, montado en `/mnt/R5`) |
| 6 nodos de cómputo | Ejecutan los jobs de HTCondor (~20 slots) |

Todos los nodos tienen AlmaLinux 9, acceso a `/mnt/R5` y a CVMFS.

## Contenido

- [Acceso](acceso.md): conectarse por SSH, tmux y screen
- [Almacenamiento](almacenamiento.md): home, scratch, RAID y directorios compartidos
- [Apptainer](apptainer.md): containers
- [HTCondor](htcondor.md): mandar jobs a los nodos de cómputo
- [Python, GPU y Jupyter](python-gpu.md): virtual environments, conda, GPU y notebooks
- [ROOT](root.md)
- [ATLAS](atlas.md): CVMFS, proxy de la grid, MCP para Claude Code y SALT
- [Simulaciones](simulaciones.md): MadGraph + Pythia + Delphes y `mgpd`
