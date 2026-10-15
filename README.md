# kvm

Bootstrap de **acceso inicial** para un Proxmox recién instalado: instala Tailscale y une el nodo al
tailnet **con el tag del sitio**, para poder seguir el despliegue por SSH en vez de tipear en una
consola KVM web.

## Uso

Una sola línea, sin comillas (pensada para pegarse en una consola web, que suele malinterpretar
comillas y caracteres especiales):

```
apt-get update -qq; apt-get install -y -qq curl; curl -fsSL https://raw.githubusercontent.com/invi4/kvm/main/kvm | TSKEY=tskey-auth-XXXX sh -s <cliente>
```

- El `apt` adelante es porque un Proxmox pelado puede no tener `curl`. Va con `;` y no con `&&`: sin
  suscripción, `apt-get update` sale con error (el repo enterprise devuelve 401) y con `&&` el `install`
  no correría nunca.
- La key va por **entorno** (`TSKEY=...` antes del `sh`): es lo que ninguna consola malinterpreta.
- **Sin la key no hace nada** —por eso este repositorio puede ser público—: valida el sitio y la key,
  imprime lo que entendió **antes** de tocar el sistema, y termina diciendo el comando de SSH.
- Un nodo **con tag no expira**. Sin el tag, Tailscale le pone vencimiento a la llave y el sitio se
  pierde sin avisar.

## De dónde sale

Se publica solo desde el repositorio privado (una sola fuente) y el workflow **corre la suite antes de
publicar**, que es la que verifica que este archivo no contenga secretos: claves, identificadores de
cuenta, nombres de clientes. Lo que se publica en git queda para siempre.

Si encontrás este repositorio y no sos parte del equipo: no hay nada acá que sirva sin una auth key
válida de la tailnet correspondiente.
