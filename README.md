# Laboratorios de red ASIR
Laboratorio ordenado según prácticas / número de laboratorio.
# Laboratorios
## Laboratorio 1
### Configuración básica

Configuración inicial de los routers con la topología preestablecida de 6 routers sin ningún host. Ping habilitado de punto a punto (pee to peer, P2P)

Configuración de archivos:
- Archivos de configuración: `laboratorio 1/inicial/configs/*`
- Archivo de containerlabs a ejecutar: `laboratorio 1/inicial/lab1.clab.yaml`
- Imagen de topología (drawio): `laboratorio 1/lab1.clab.drawio`
- Imagen de topología (png): `laboratorio 1/lab1.clab.png`
- Imagen de topología (svg): `laboratorio 1/lab1.clab.svg`

### Configuración de pings sin ECMP

Configuración en la cual se habilitan los pings de host1 a host2. En este caso los host son máquinas alpine de linux. Se debería de poder hacer ping desde el host1 (10.0.110.0) a host2 (10.0.120.0).

La ruta a seguir sin ECMP, siempre será: H1 <-> R3 <-> R4 <-> R5 <-> H2

En caso de que caiga el router3 el ping no funcionará, ya que la única ruta habilitada es esa. Se podría hacer un cambio manual, y sería entrando en el **routers1** y el **router4**, y poniendo estos comandos respectivamente: 

- En router1: `network-instance router1 next-hop-groups group nhg-primary admin-state enable nexthop 1 ip-address 10.0.10.1 resolve true` y para asignarla, ponemos el siguiente comando también: `network-instance router1 static-routes route 10.0.120.0/31 admin-state enable metric 1 preference 10 next-hop-group nhg-primary`.
- En router4: `network-instance router4 next-hop-groups group nhg-primary admin-state enable nexthop 1 ip-address 10.0.30.0 resolve true` y para asignarla, ponemos el siguiente comando también: `network-instance router4 static-routes route 10.0.110.0/31 admin-state enable metric 1 preference 10 next-hop-group nhg-primary`.

De esta manera el ping volvería a funcionar, pero no es muy útil.

Configuración de archivos:
- Archivos de configuración: `laboratorio 1/static_routes/configs/*`
- Archivo de containerlabs a ejecutar: `laboratorio 1/static_routes/lab1_static_routes.clab.yaml`
- Imagen de topología (drawio): `laboratorio 1/lab1_static_routes.clab.drawio`
- Imagen de topología (png): `laboratorio 1/lab1_static_routes.clab.png`
- Imagen de topología (svg): `laboratorio 1/lab1_static_routes.clab.svg`

### Configuración de pings con ECMP

Configuración en la cual se habilitan los pings de host1 a host2. En este caso los host son máquinas alpine de linux. Se debería de poder hacer ping desde el host1 (10.0.110.0) a host2 (10.0.120.0).

La ruta a seguir con ECMP, en un principio debería de ser: H1 <-> R3 <-> R4 <-> R5 <-> H2

En caso de que el router3 caiga, la nueva ruta automáticamente se cambiaría a: H1 <-> R2 <-> R4 <-> R5 <-> H2

Esto ocurre gracias a ECMP, ya que reparte la carga. Por lo tanto al ser equal cost, si están tanto router2 como router3 activados, el ping podría ir tanto como un router como por otro router. Es decir no existe el comportamiento de un router primario y otro router de backup.

Configuración de archivos:
- Archivos de configuración: `laboratorio 1/static_routes_ecmp/configs/*`
- Archivo de containerlabs a ejecutar: `laboratorio 1/static_routes_ecmp/lab1_static_routes_ecmp.clab.yaml`
- Imagen de topología (drawio): `laboratorio 1/lab1_static_routes.clab.drawio`
- Imagen de topología (png): `laboratorio 1/lab1_static_routes.clab.png`
- Imagen de topología (svg): `laboratorio 1/lab1_static_routes.clab.svg`