# Guía de usuarios de JUPITER

JUPITER es el cluster de Física de Altas Energías del IFLP, usado para
simulación, análisis y entrenamiento de modelos de machine learning en GPU.

!!! info "Acceso"
    Para conectarte necesitás la VPN y una cuenta en el cluster.
    Los datos de conexión te los envía el administrador cuando se crea tu cuenta.

## Recursos principales

| Recurso | Uso |
| --- | --- |
| `jupiter` | Nodo de login: Jupyter, GPU (RTX 3090) y envío de trabajos a HTCondor |
| Nodos de cómputo | Ejecutan los trabajos de HTCondor |
| `/mnt/R5` | Almacenamiento compartido en todos los nodos |
| `/scratch` | Espacio temporal por usuario (se limpia periódicamente) |
| `/opt/venvs-hep` | Entornos de Python compartidos |
| `/cvmfs` | Software de HEP (ATLAS, CERN) |
