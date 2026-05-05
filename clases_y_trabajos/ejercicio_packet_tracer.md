# Actividad Práctica: Configuración de IPs en Cisco Packet Tracer

**Tema:** Configuración de Direcciones IP  
**Red de trabajo:** `192.168.1.0/24`  
**Herramienta:** Cisco Packet Tracer  
**Duración estimada:** 20 – 30 minutos  
**Modalidad:** Individual o en parejas

---

## Objetivo

Configurar correctamente las direcciones IP de un router y dos computadores en Cisco Packet Tracer, aplicando la regla de asignación de la clase, y verificar la conectividad entre los dispositivos mediante el comando `ping`.

---

## Topología a Construir

```
[PC-A] ──┐
          ├──[Switch]──[Router]
[PC-B] ──┘
```

**Dispositivos necesarios:**
- 1 Router (por ejemplo: Cisco 2911)
- 1 Switch (por ejemplo: Cisco 2960)
- 2 Computadores (PC genérico)

**Cables:**
- Usar cable **Copper Straight-Through** para conectar PCs y Switch.
- Usar cable **Copper Straight-Through** para conectar Switch y Router.

---

## Tabla de Direccionamiento

| Dispositivo | Interfaz | Dirección IP | Máscara de Subred | Gateway |
|---|---|---|---|---|
| Router | GigabitEthernet 0/0 | `192.168.1.1` | `255.255.255.0` | — |
| PC-A | NIC | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| PC-B | NIC | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |

> **Nota:** `192.168.1.0` es la dirección de red y **no** se asigna a ningún dispositivo. El rango `192.168.1.1 – 192.168.1.9` está reservado para routers; los computadores comienzan desde `192.168.1.10`.

---

## Paso 1 — Construir la Topología

1. Abrir Cisco Packet Tracer.
2. En la barra inferior, seleccionar los dispositivos y arrastrarlos al área de trabajo:
   - 1 Router
   - 1 Switch
   - 2 PCs
3. Conectar los dispositivos con el cable indicado en la sección anterior.
4. Verificar que los puntos de conexión queden de color verde (enlace activo) o ámbar (enlace en proceso de activarse).

---

## Paso 2 — Configurar el Router

1. Hacer clic sobre el router.
2. Ir a la pestaña **CLI**.
3. Si aparece el mensaje `"Would you like to enter the initial configuration dialog? [yes/no]:"`, escribir **no** y presionar **Enter**.
4. Ingresar los siguientes comandos uno por uno:

```
enable
configure terminal
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

5. Verificar el estado de la interfaz:

```
show ip interface brief
```

La columna **Status** debe mostrar `up` y la columna **Protocol** debe mostrar `up`.

6. Guardar la configuración:

```
copy running-config startup-config
```

---

## Paso 3 — Configurar PC-A

1. Hacer clic sobre **PC-A**.
2. Ir a la pestaña **Desktop**.
3. Seleccionar **IP Configuration**.
4. Ingresar los siguientes valores:

| Campo | Valor |
|---|---|
| IP Address | `192.168.1.10` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |

5. Cerrar la ventana.

---

## Paso 4 — Configurar PC-B

1. Hacer clic sobre **PC-B**.
2. Ir a la pestaña **Desktop**.
3. Seleccionar **IP Configuration**.
4. Ingresar los siguientes valores:

| Campo | Valor |
|---|---|
| IP Address | `192.168.1.11` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |

5. Cerrar la ventana.

---

## Paso 5 — Verificar la Conectividad con Ping

### Desde PC-A:

1. Hacer clic sobre **PC-A**.
2. Ir a **Desktop** → **Command Prompt**.
3. Realizar los siguientes pings:

```
ping 192.168.1.1
```
→ Debe responder (conectividad con el router ✔)

```
ping 192.168.1.11
```
→ Debe responder (conectividad con PC-B ✔)

### Desde PC-B:

```
ping 192.168.1.1
```
→ Debe responder (conectividad con el router ✔)

```
ping 192.168.1.10
```
→ Debe responder (conectividad con PC-A ✔)

**Resultado esperado:**
```
Reply from 192.168.1.1: bytes=32 time<1ms TTL=128
```

---

## Preguntas de Análisis

Responde las siguientes preguntas en tu cuaderno o en un documento:

1. ¿Qué ocurre si asignas la IP `192.168.1.10` a **ambas** PCs? ¿Qué observas al hacer ping?

2. ¿Qué sucede si configuras el gateway de PC-A como `192.168.1.2` en vez de `192.168.1.1`? ¿Por qué?

3. ¿Por qué la dirección `192.168.1.0` **no** puede asignarse a ningún dispositivo?

4. ¿Por qué la dirección `192.168.1.255` **no** puede asignarse a ningún dispositivo?

5. Si agregas una tercera PC a la red, ¿qué IP le asignarías? ¿Cuál sería su gateway?

6. ¿Cuál sería la IP del segundo router en esta red, siguiendo la regla de asignación de la clase?

---

## Actividad de Extensión (Opcional)

Si terminas antes de tiempo, realiza lo siguiente:

1. Agrega una tercera PC a la topología.
2. Asígnale la IP `192.168.1.12` con los mismos valores de máscara y gateway.
3. Verifica conectividad entre las tres PCs y el router.
4. En el router, ejecuta el comando `show arp` y explica qué información muestra.

---

## Lista de Verificación Final

Antes de entregar, revisa que hayas completado lo siguiente:

- [ ] Topología construida con los tres dispositivos y el switch.
- [ ] Cables correctamente conectados.
- [ ] Router configurado con IP `192.168.1.1` en la interfaz GigabitEthernet 0/0.
- [ ] Interfaz del router en estado `up/up`.
- [ ] PC-A configurada con IP `192.168.1.10`, máscara `255.255.255.0`, gateway `192.168.1.1`.
- [ ] PC-B configurada con IP `192.168.1.11`, máscara `255.255.255.0`, gateway `192.168.1.1`.
- [ ] Ping exitoso desde PC-A al router (`192.168.1.1`).
- [ ] Ping exitoso desde PC-A a PC-B (`192.168.1.11`).
- [ ] Preguntas de análisis respondidas.
