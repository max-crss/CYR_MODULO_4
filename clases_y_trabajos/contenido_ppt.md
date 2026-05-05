# Presentación: Configuración de Direcciones IP en Cisco Packet Tracer

> **Instrucciones para el docente:** Este archivo contiene el texto completo de cada diapositiva. Puedes copiar cada sección directamente a PowerPoint, Google Slides u otro programa de presentaciones.

---

## Diapositiva 1 — Portada

**Título:**  
Configuración de Direcciones IP en Cisco Packet Tracer

**Subtítulo:**  
Red 192.168.1.0/24 — Routers y Computadores

**Imagen sugerida:** logotipo de Cisco Packet Tracer o diagrama de red simple.

---

## Diapositiva 2 — Objetivos de la Clase

Al finalizar esta clase, el estudiante será capaz de:

- Comprender qué es una dirección IP y sus componentes básicos.
- Identificar la dirección de red, la máscara de subred y la puerta de enlace.
- Configurar direcciones IP en routers dentro de Packet Tracer.
- Configurar direcciones IP en computadores dentro de Packet Tracer.
- Verificar la conectividad entre dispositivos mediante el comando `ping`.

**Imagen sugerida:** lista con íconos de checkmark.

---

## Diapositiva 3 — ¿Qué es una Dirección IP?

Una **dirección IP** es un identificador lógico único que permite que un dispositivo se comunique dentro de una red.

Formato: cuatro grupos de números del 0 al 255, separados por puntos.

Ejemplos:
- `192.168.1.1`
- `192.168.1.10`
- `10.0.0.1`

Cada dispositivo en la red **debe tener una IP única**.

**Imagen sugerida:** diagrama de red con IPs visibles en cada dispositivo.

---

## Diapositiva 4 — Componentes de una Configuración IP

Para configurar correctamente un dispositivo se requiere:

| Campo | Descripción | Ejemplo |
|---|---|---|
| Dirección IP | Identifica al dispositivo | `192.168.1.10` |
| Máscara de subred | Define el tamaño de la red | `255.255.255.0` |
| Puerta de enlace (Gateway) | IP del router para salir a otras redes | `192.168.1.1` |

> Sin estos tres valores bien configurados, no hay comunicación.

**Imagen sugerida:** ventana de configuración IP de Windows o de Packet Tracer.

---

## Diapositiva 5 — La Red 192.168.1.0/24

Trabajaremos con la siguiente red:

- **Dirección de red:** `192.168.1.0`
- **Máscara:** `255.255.255.0` (equivale a `/24`)
- **Primera IP útil:** `192.168.1.1`
- **Última IP útil:** `192.168.1.254`
- **Broadcast:** `192.168.1.255`
- **Total de hosts disponibles:** 254

> `192.168.1.0` es la **dirección de red** — no se asigna a ningún dispositivo.  
> `192.168.1.255` es el **broadcast** — tampoco se asigna.

**Imagen sugerida:** tabla o diagrama de rango de IPs.

---

## Diapositiva 6 — Regla de Asignación para Esta Práctica

Se establece la siguiente organización para la red `192.168.1.0/24`:

| Rango | Uso |
|---|---|
| `192.168.1.0` | Dirección de red — **no se asigna** |
| `192.168.1.1` – `192.168.1.9` | **Reservadas para routers** |
| `192.168.1.10` en adelante | **Computadores y dispositivos finales** |
| `192.168.1.255` | Broadcast — **no se asigna** |

Esta organización facilita la administración y reduce errores.

**Imagen sugerida:** barra de rango de IPs con colores diferenciados.

---

## Diapositiva 7 — ¿Por Qué Reservar IPs para Routers?

Los routers actúan como **puertas de enlace** (gateway).  
Al reservar las primeras IPs útiles para ellos:

✔ Es fácil identificar qué IP corresponde a un router.  
✔ La administración de la red es más ordenada.  
✔ Se evitan conflictos de IP entre routers y equipos finales.  
✔ Se puede escalar la red sin reconfigurar todo.

Rango reservado en esta práctica:
- `192.168.1.1` → Router principal
- `192.168.1.2` → Router secundario
- `192.168.1.3` – `192.168.1.9` → Disponibles para más routers

**Imagen sugerida:** ícono de router con la IP `192.168.1.1`.

---

## Diapositiva 8 — IPs para Computadores y Dispositivos Finales

Las IPs para computadores, impresoras, teléfonos IP y otros dispositivos finales comienzan desde:

**`192.168.1.10`**

Ejemplos de asignación:

| Dispositivo | IP |
|---|---|
| PC-A | `192.168.1.10` |
| PC-B | `192.168.1.11` |
| PC-C | `192.168.1.12` |
| Impresora | `192.168.1.20` |

Máscara para todos: `255.255.255.0`  
Gateway para todos: `192.168.1.1`

**Imagen sugerida:** íconos de computadores con sus IPs asignadas.

---

## Diapositiva 9 — Configurar IP en un Computador (Packet Tracer)

**Pasos:**

1. Clic sobre el computador.
2. Ir a la pestaña **Desktop**.
3. Seleccionar **IP Configuration**.
4. Completar los campos:

| Campo | Valor |
|---|---|
| IP Address | `192.168.1.10` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `192.168.1.1` |

5. Cerrar la ventana (se guarda automáticamente).

**Imagen sugerida:** captura de pantalla de la ventana IP Configuration de Packet Tracer.

---

## Diapositiva 10 — Configurar IP en un Router (Packet Tracer) — Parte 1

**Pasos iniciales:**

1. Clic sobre el router.
2. Ir a la pestaña **CLI**.
3. Si aparece el diálogo de configuración inicial, responder **no**.
4. En el prompt, ingresar:

```
enable
configure terminal
```

Después del primer comando, el prompt cambia de `>` a `#`.  
Después del segundo, cambia a `(config)#`.

**Imagen sugerida:** ventana CLI de Packet Tracer con el prompt visible.

---

## Diapositiva 11 — Configurar IP en un Router (Packet Tracer) — Parte 2

**Continuar en el CLI:**

```
interface gigabitEthernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

**Verificar:**

```
show ip interface brief
```

**Guardar:**

```
copy running-config startup-config
```

> El comando `no shutdown` es **obligatorio**: las interfaces de router están apagadas por defecto.

**Imagen sugerida:** CLI con los comandos escritos y el estado "up/up" en la verificación.

---

## Diapositiva 12 — Tabla de Comandos del Router

| Comando | Función |
|---|---|
| `enable` | Modo privilegiado |
| `configure terminal` | Modo configuración global |
| `interface gigabitEthernet 0/0` | Seleccionar interfaz |
| `ip address [IP] [Máscara]` | Asignar IP y máscara |
| `no shutdown` | Activar la interfaz |
| `exit` | Salir del modo actual |
| `show ip interface brief` | Ver estado de interfaces |
| `copy running-config startup-config` | Guardar configuración |

**Imagen sugerida:** tabla con fondo oscuro, texto en verde (estilo terminal).

---

## Diapositiva 13 — Importancia del Gateway

La **puerta de enlace (gateway)** es la IP del router que conecta la red local con otras redes.

- Sin gateway, un computador **no puede comunicarse fuera de su red**.
- El gateway debe estar en la **misma red** que el computador.

Ejemplo:
- PC tiene IP `192.168.1.10`
- Router tiene IP `192.168.1.1`
- ✔ Ambos están en la red `192.168.1.0/24` → el gateway **sí es válido**

Si el gateway fuera `192.168.2.1`:
- ✖ No está en la misma red → la comunicación **fallará**

**Imagen sugerida:** diagrama mostrando PC → Router → Internet.

---

## Diapositiva 14 — Verificación de Conectividad con Ping

Después de configurar los dispositivos:

1. En el PC, ir a **Desktop** → **Command Prompt**.
2. Escribir:

```
ping 192.168.1.1
```

**Resultado exitoso:**
```
Reply from 192.168.1.1: bytes=32 time<1ms TTL=128
```

**Resultado fallido:**
```
Request timed out.
```

También se puede hacer ping entre PCs:
```
ping 192.168.1.11
```

**Imagen sugerida:** ventana de Command Prompt con ping exitoso.

---

## Diapositiva 15 — Errores Comunes

| Error | Causa | Solución |
|---|---|---|
| Ping falla | Interfaz del router apagada | Ejecutar `no shutdown` |
| Ping falla | IP duplicada | Revisar tabla y asignar IPs únicas |
| Ping falla | Gateway incorrecto | Corregir la IP del gateway en el PC |
| Ping falla | Máscara incorrecta | Verificar que todos usen `255.255.255.0` |
| Ping falla | Cable mal conectado | Revisar tipo de cable y puertos |
| Error en CLI | Modo de configuración equivocado | Verificar el prompt: `>` / `#` / `(config)#` |

**Imagen sugerida:** ícono de advertencia con lista de errores.

---

## Diapositiva 16 — Ejemplo Completo de Direccionamiento

Topología: 1 router, 2 PCs, 1 switch.

| Dispositivo | IP | Máscara | Gateway |
|---|---|---|---|
| Router | `192.168.1.1` | `255.255.255.0` | — |
| PC-A | `192.168.1.10` | `255.255.255.0` | `192.168.1.1` |
| PC-B | `192.168.1.11` | `255.255.255.0` | `192.168.1.1` |

Pruebas de conectividad:
- PC-A → ping `192.168.1.1` ✔
- PC-A → ping `192.168.1.11` ✔
- PC-B → ping `192.168.1.1` ✔

**Imagen sugerida:** diagrama de topología con IPs visibles.

---

## Diapositiva 17 — Actividad Práctica

**Instrucciones:**

1. Abrir Cisco Packet Tracer.
2. Insertar: 1 Router, 1 Switch, 2 PCs.
3. Conectar los dispositivos con el cable adecuado.
4. Configurar el router: IP `192.168.1.1`, máscara `255.255.255.0`.
5. Configurar PC-A: IP `192.168.1.10`, máscara `255.255.255.0`, gateway `192.168.1.1`.
6. Configurar PC-B: IP `192.168.1.11`, máscara `255.255.255.0`, gateway `192.168.1.1`.
7. Hacer ping desde PC-A al router y a PC-B.
8. Documentar los resultados.

**Tiempo estimado:** 20 minutos.

**Imagen sugerida:** captura de la topología terminada en Packet Tracer.

---

## Diapositiva 18 — Conclusiones

✔ Una dirección IP identifica a cada dispositivo en la red.  
✔ La red `192.168.1.0/24` tiene 254 hosts disponibles.  
✔ `192.168.1.0` es dirección de red — **no se asigna**.  
✔ Las IPs `192.168.1.1` a `192.168.1.9` están **reservadas para routers**.  
✔ Los computadores y dispositivos finales usan IPs desde **`192.168.1.10`**.  
✔ La puerta de enlace debe coincidir con la IP del router.  
✔ El comando `ping` verifica la conectividad.  
✔ El orden en la asignación de IPs mejora la administración de la red.

**Imagen sugerida:** diagrama de red completo con todos los dispositivos etiquetados.

---

## Diapositiva 19 — ¿Preguntas?

**Gracias por su atención.**

Práctica: configurar su propia topología siguiendo la regla de asignación vista hoy.

> Recuerden: `192.168.1.1 – .9` → routers | `192.168.1.10` en adelante → computadores y equipos finales.
