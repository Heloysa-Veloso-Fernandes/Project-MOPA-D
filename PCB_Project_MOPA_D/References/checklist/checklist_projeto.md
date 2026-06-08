# Projeto MOPA

## Objetivo

## Parametros

- Manufacturer_Name
- Manufacturer_Part_Number
- Supplier 1
- Supplier Part Number 1
- Value
- Datasheet Link

## Footprints

- Para componentes do tipo resistor 0402 - RESC1005X40N
- Para componentes do tipo capacitor 0402 - CAPC1005X40N
- Para componentes do tipo indutor 0402 - INDC1005X40N

- Para componentes do tipo resistor 0603 - RESC1608X06N
- Para componentes do tipo capacitor 0603 - CAPC1608X06N
- Para componentes do tipo indutor 0603 - INDC1608X06N

- Para componentes do tipo resistor 0805 - RESC2012X06N
- Para componentes do tipo capacitor 0805 - CAPC2012X06N
- Para componentes do tipo indutor 0805 - INDC2012X06N

- SODFL3618X143N - Pino 1 - Anodo



## I2C

- Pull-ups de 4K7 - 0402 em tudo
- Pull-ups de 3k3 - 0402 no RPI (de backup sem conexao)

## Vias 

 - Hole/Diameter: 0.3 mm / 0.7 mm
 - Hole/Diameter: 0.2 mm / 0.5 mm (Casos extremos)
 - Track mudança de plano: 0.3/0.7 mm (1mm de distancia)
 - Via para plano (0.3/0.7 mm)
 
 
 


# 3D Body

- No layer Mechanical 1

D0008B-IPC_A



## Componentes

### Raspberry Pi 4 Model B SC0194(9) - RPI

- O computador de placa única (SOC - System on Chip)
- Processador quad-core Broadcom BCM2711 ARM Cortex-A72 operando a 1,5 GHz.
- Equipado com 4 GB de RAM e uma variedade de conexões.
- Barramento de expansão de 40 pinos, header 2x20, 2.54 mm.
- https://www.snapeda.com/parts/SC0194(9)/Raspberry+Pi/view-part/?ref=snap
- Datasheet: https://www.snapeda.com/parts/SC0194(9)/Raspberry%20Pi/datasheet/
- Utilização do barramento I2C.
	- A RPI já possui pull-ups de 1K8
	- Colocar pull-ups de 3K3 de reserva mas sem colocar (backups)
	- SDA (GPIO2/SDA1, Pino 3) - Bidirecional
	- SCL (GPIO3/SCL1, Pino 5) - Bidirecional
	- Pull-ups
- Utilização do barramento SPI.
	- SDA (GPIO2/SDA1, Pino 3)
	- SDA (GPIO2/SDA1, Pino 3)
	- SDA (GPIO2/SDA1, Pino 3)
	- SDA (GPIO2/SDA1, Pino 3)


## Fabricação

- https://jlcpcb.com/capabilities/pcb-capabilities

### JLCPCB - Capacidades












