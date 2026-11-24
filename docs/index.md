# JUPITER docs

**(mini-)cluster del grupo de Física de Altas Energías del IFLP**

!!! info ""
    Para conectarte necesitás acceso a la VPN y una cuenta en el cluster. Ver [Acceso](acceso.md).

    Ante cualquier problema o consulta, escribile al administrador del cluster.

## Recursos

- Nodo principal: login, GPU (RTX 3090), y envío de jobs a HTCondor
- Nodo de almacenamiento (RAID5 de 18 TB, montado en `/mnt/R5`)
- 6 nodos de cómputo para ejecutar jobs de HTCondor (~20 slots)

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
- [Claude](claude.md): Usar claude code y MCPs instalados
