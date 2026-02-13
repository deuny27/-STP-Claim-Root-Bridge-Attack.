# STP-Claim-Root-Bridge-Attack.

Este proyecto demuestra la implementación de un ataque STP Root Bridge Claim, desarrollado en Python 3 utilizando la librería Scapy.

El objetivo del laboratorio es mostrar cómo un atacante puede inyectar BPDU (Bridge Protocol Data Units) maliciosas en una red conmutada para forzar la reconvergencia del protocolo STP y convertirse en el nuevo Root Bridge.

Este proyecto fue desarrollado exclusivamente con fines académicos en un entorno controlado de laboratorio.

# Descripción del Ataque

El protocolo Spanning Tree Protocol (STP) evita bucles en redes conmutadas eligiendo un Root Bridge basado en el Bridge ID más bajo.

- El ataque consiste en:

Enviar BPDU de configuración falsas.

Establecer una prioridad de bridge extremadamente baja (ej: 0).

Forzar a los switches a reconocer al atacante como el nuevo Root Bridge.

Provocar reconvergencia de la red.

- Como resultado:

El tráfico puede redirigirse hacia el atacante.

Puede generarse interrupción del servicio.

Se pueden habilitar ataques posteriores (MITM).

# Tecnologías Utilizadas

- Python 3

- Scapy Project

- Linux

- Entorno de laboratorio virtual (switches y hosts virtualizados)

# Video de Ataque
https://youtu.be/yJ7hKjDsUJk

Topologia en Pnet


<img width="975" height="762" alt="image" src="https://github.com/user-attachments/assets/286ecb34-9a1e-4d46-8e35-afc5465590fd" />


# Parámetros del Script

El script permite modificar los siguientes valores:

- ATTACK_INTERFACE = "eth0"

- ATTACKER_BRIDGE_PRIORITY = 0


# Funcionamiento del Script

El script realiza las siguientes acciones:

1️⃣ Obtiene la dirección MAC de la interfaz atacante.

2️⃣ Construye un Bridge ID compuesto por:

2 bytes de prioridad

6 bytes de dirección MAC

3️⃣ Crea una BPDU de configuración STP (802.1D) con:

Root ID igual al Bridge ID del atacante

Root Path Cost = 0

Flags de Topology Change

Hello Time = 2 segundos

Forward Delay = 15 segundos

4️⃣ Envía continuamente BPDU cada 2 segundos (Hello Time).

5️⃣ Obliga a los switches a reconverger la topología y aceptar al atacante como Root Bridge.
