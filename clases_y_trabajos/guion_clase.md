# Guion de Clase: Configuración de Direcciones IP en Cisco Packet Tracer

**Duración estimada:** 60 – 90 minutos  
**Nivel:** Básico – Intermedio  
**Herramienta:** Cisco Packet Tracer  
**Red de trabajo:** `192.168.1.0/24`

---

## 1. Introducción (10 min)

### Qué decir al inicio:

> "Hoy vamos a aprender a configurar direcciones IP dentro de Cisco Packet Tracer. Trabajaremos con una red real que se usa en entornos domésticos y de pequeñas empresas: la red 192.168.1.0/24.
> El objetivo es que al final de la clase sean capaces de asignar IPs tanto a routers como a computadores, y verificar que se comunican entre sí."

### Punto de partida — preguntar al grupo:
- ¿Qué es una dirección IP?
- ¿Han visto alguna vez una dirección IP en su computador?
- ¿Saben para qué sirve el gateway o puerta de enlace?

---

## 2. Conceptos clave (15 min)

### 2.1 Dirección IP

Una dirección IP (Internet Protocol) es un identificador lógico único que se asigna a cada dispositivo en una red para que pueda enviar y recibir datos.

Formato: cuatro grupos de números separados por puntos, cada uno entre 0 y 255.

Ejemplo:
```
192.168.1.10
```

### 2.2 Máscara de subred

Indica qué parte de la IP corresponde a la red y qué parte corresponde al host (dispositivo).

En esta clase usaremos:
```
255.255.255.0
```
Esto equivale a `/24` en notación CIDR.

Con esta máscara, la porción de red es `192.168.1` y la porción de host es el último octeto (`.1` hasta `.254`).

### 2.3 Red 192.168.1.0/24

| Concepto | Valor |
|---|---|
| Dirección de red | `192.168.1.0` |
| Primera IP útil | `192.168.1.1` |
| Última IP útil | `192.168.1.254` |
| Broadcast | `192.168.1.255` |
| Máscara | `255.255.255.0` |
| Total de hosts disponibles | 254 |

> **Importante:** `192.168.1.0` es la dirección de red, no se asigna a ningún dispositivo. `192.168.1.255` es el broadcast, tampoco se asigna.

### 2.4 Puerta de enlace (Gateway)

Es la IP del router al que se conectan los equipos para salir hacia otras redes.  
Ejemplo: si el router tiene la IP `192.168.1.1`, esa será la puerta de enlace de todos los computadores de esa red.

---

## 3. Regla de asignación práctica (5 min)

Para esta clase y para las prácticas del módulo, se establece el siguiente orden:

| Rango | Uso |
|---|---|
| `192.168.1.0` | Dirección de red — **no se asigna** |
| `192.168.1.1` – `192.168.1.9` | **Reservadas para routers** |
| `192.168.1.10` en adelante | **Computadores y dispositivos finales** |
| `192.168.1.255` | Broadcast — **no se asigna** |

Esto facilita la administración: si ves una IP `.1` a `.9` sabes que es un router; si ves `.10` en adelante, es un PC u otro dispositivo final.

Ejemplo de tabla de direccionamiento:

| Dispositivo | IP | Máscara | Gateway |
|---|---|---|---|
| Router principal | `192.168.1.1` | `255.255.255.0` | — |
| Router secundario | `192.168.1.2` | `255.255.255.0` | — |
| PC-A | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| PC-B | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |
| PC-C | `192.168.1.12` | `255.255.255.0` | `192.168.1.1` |

---

## 4. Configuración de IP en Computadores en Packet Tracer (10 min)

### Pasos a seguir (demostración en pantalla):

1. Abrir Packet Tracer y agregar un computador.
2. Hacer clic sobre el computador.
3. Ir a la pestaña **Desktop**.
4. Seleccionar **IP Configuration**.
5. Completar los campos:

| Campo | Valor ejemplo |
|---|---|
| IP Address | `192.168.1.10` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |

6. Cerrar la ventana. La configuración queda guardada automáticamente.

> **Nota:** En Packet Tracer no es necesario presionar "Guardar" en la configuración de PC; el valor se aplica al momento de ingresarlo.

---

## 5. Configuración de IP en Routers en Packet Tracer (15 min)

### Pasos a seguir (demostración con CLI):

1. Hacer clic sobre el router.
2. Ir a la pestaña **CLI**.
3. Si aparece el mensaje `"Would you like to enter the initial configuration dialog?"`, responder **no**.
4. Ingresar los siguientes comandos:

```
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

5. Para verificar que la interfaz está activa:

```
show ip interface brief
```

6. Para guardar la configuración:

```
copy running-config startup-config
```

### Explicación de cada comando:

| Comando | Qué hace |
|---|---|
| `enable` | Entra al modo privilegiado |
| `configure terminal` | Entra al modo de configuración global |
| `interface gigabitEthernet 0/0` | Selecciona la interfaz a configurar |
| `ip address 192.168.1.1 255.255.255.0` | Asigna la IP y la máscara a esa interfaz |
| `no shutdown` | Activa la interfaz (por defecto está apagada) |
| `exit` | Sale del modo de interfaz |
| `show ip interface brief` | Muestra el estado de todas las interfaces |
| `copy running-config startup-config` | Guarda la configuración en la memoria permanente |

---

## 6. Verificación de conectividad — Ping (10 min)

Una vez configurados todos los dispositivos, se verifica la conectividad usando el comando `ping`.

### Desde un computador en Packet Tracer:

1. Hacer clic en el PC.
2. Ir a **Desktop** → **Command Prompt**.
3. Escribir:

```
ping 192.168.1.1
```

Si responde con mensajes como:
```
Reply from 192.168.1.1: bytes=32 time<1ms TTL=128
```
La configuración es correcta.

### También se puede hacer ping entre PCs:

```
ping 192.168.1.11
```

---

## 7. Errores comunes y cómo resolverlos (10 min)

| Error | Causa probable | Solución |
|---|---|---|
| Ping sin respuesta | IP del gateway incorrecta | Verificar la IP del router y del gateway en el PC |
| Ping sin respuesta | Interfaz del router apagada | Ejecutar `no shutdown` en la interfaz |
| Ping sin respuesta | IP duplicada | Revisar la tabla de direccionamiento y asignar IPs únicas |
| Ping sin respuesta | Máscara incorrecta | Corregir la máscara en todos los dispositivos |
| Ping sin respuesta | Cable mal conectado | Verificar el tipo de cable y el puerto |
| Error en CLI del router | Modo de configuración incorrecto | Verificar el símbolo del prompt: `>` (usuario), `#` (privilegiado), `(config)#` (configuración global) |

---

## 8. Cierre (5 min)

### Resumen de lo aprendido:

- Una IP identifica a cada dispositivo en la red.
- La red `192.168.1.0/24` tiene 254 hosts disponibles.
- `192.168.1.0` es la dirección de red y no se asigna a ningún dispositivo.
- El rango `192.168.1.1` a `192.168.1.9` se reserva para routers en esta práctica.
- Los computadores y dispositivos finales usan IPs desde `192.168.1.10`.
- La puerta de enlace debe apuntar a la IP del router.
- Se verifica la conectividad con el comando `ping`.

### Pregunta de cierre al grupo:

> "Si un PC tiene la IP `192.168.1.11` y el gateway `192.168.1.1`, ¿a qué IP debe asignarse la interfaz del router para que haya comunicación?"

---

## Recursos adicionales

- Cisco Packet Tracer (descarga gratuita con cuenta Cisco NetAcad)
- Documentación de comandos IOS: [cisco.com](https://www.cisco.com)
