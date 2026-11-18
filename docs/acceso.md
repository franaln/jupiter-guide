# Acceso

El nodo principal es `jupiter`

!!! note ""
    - Para conectarte desde afuera de la red del IFLP tenés que usar la VPN.
    - Los datos de conexión (`<JUPITER-IP>`) te los envía el administrador cuando se crea tu cuenta.
    - Si no tenés usuario o tenés problemas para iniciar sesión la primera vez, avisale al administrador para resetear el password.

## Conectarse por SSH

```bash
ssh <user>@<JUPITER-IP>
```

Para no tener que escribir la IP cada vez, agregá esto a `~/.ssh/config`, reemplazando `<user>` por tu usuario en el cluster:

```
Host jupiter
    User <user>
    HostName <JUPITER-IP>
```

Y después te conectás con:

```bash
ssh jupiter
```

Otra opción es agregar esta línea a `/etc/hosts`:

```
<JUPITER-IP> jupiter
```

## tmux y screen

`tmux` y `screen` están instalados. Sirven para dejar una sesión abierta con algo corriendo aunque te desconectes.

- Referencia rápida de tmux: <https://tmux.app/cheat-sheet/>
