# Templates de Notas de Fabricação, Montagem e Esquemático

## 1. Notas de fabricação para incluir em camada mecânica do PCB

> Ajustar valores conforme fabricante, projeto e normas aplicáveis.

```text
FABRICATION NOTES

1. BOARD PART NUMBER: <PN>
2. REVISION: <REV>
3. BOARD THICKNESS: <X.XX mm> ± <tolerance>
4. LAYER COUNT: <N>
5. BASE MATERIAL: FR-4 or <specified material>, Tg >= <value> °C
6. FINISHED COPPER: OUTER <X oz>, INNER <Y oz>
7. SURFACE FINISH: <ENIG/HASL/OSP/ImmAg/etc.>
8. SOLDER MASK: <color>, BOTH SIDES
9. SILKSCREEN: <color>, TOP/BOTTOM AS INDICATED
10. FINISHED HOLE TOLERANCE: PTH <tolerance>, NPTH <tolerance>
11. BOARD OUTLINE TOLERANCE: <tolerance>
12. FABRICATE TO IPC-6012 CLASS <2/3> OR APPROVED EQUIVALENT.
13. ACCEPTABILITY PER IPC-A-600 CLASS <2/3>.
14. ELECTRICAL TEST REQUIRED.
15. CONTROLLED IMPEDANCE REQUIRED FOR NET CLASSES: <list>.
16. IMPEDANCE TOLERANCE: <±10% or manufacturer confirmed>.
17. DO NOT MODIFY STACKUP WITHOUT ENGINEERING APPROVAL.
18. VIA TREATMENT: <tented/plugged/filled/capped>, AS SPECIFIED.
19. VIA-IN-PAD SHALL BE <filled and capped> WHERE INDICATED.
20. ALL DIMENSIONS ARE IN MILLIMETERS UNLESS OTHERWISE SPECIFIED.
21. ROHS/LEAD-FREE REQUIRED: <YES/NO>.
22. UL94 V-0 MATERIAL REQUIRED: <YES/NO>.
23. CTI/MATERIAL GROUP REQUIREMENT: <if applicable>.
24. CAM REVIEW REQUIRED BEFORE PRODUCTION.
```

## 2. Tabela de impedância para fabricação

```text
CONTROLLED IMPEDANCE TABLE

| Net Class | Layer | Type | Target | Width | Gap | Reference Plane | Tolerance |
|----------|-------|------|--------|-------|-----|-----------------|-----------|
| RF_50R   | L1    | Single-ended microstrip | 50 ohm | <mm> | <mm> | L2_GND | ±<%> |
| USB_DIFF | L1    | Differential microstrip | 90 ohm diff | <mm> | <mm> | L2_GND | ±<%> |
```

## 3. Stackup table para desenho de fabricação

```text
STACKUP TABLE

| Layer | Function | Material | Thickness | Copper | Notes |
|------|----------|----------|-----------|--------|-------|
| L1 | TOP SIGNAL | Cu | <um/oz> | <finished> | Controlled impedance |
| Dielectric | Prepreg | <material> | <mm> | - | Dk=<value> |
| L2 | GND PLANE | Cu | <um/oz> | - | Reference plane |
| Core | Core | <material> | <mm> | - |  |
| L3 | POWER/SIGNAL | Cu | <um/oz> | - |  |
| Dielectric | Prepreg | <material> | <mm> | - | Dk=<value> |
| L4 | BOTTOM SIGNAL | Cu | <um/oz> | <finished> |  |
```

## 4. Notas de montagem

```text
ASSEMBLY NOTES

1. ASSEMBLE PER BOM REVISION <REV>.
2. DO NOT POPULATE COMPONENTS MARKED DNP/DNI.
3. VERIFY POLARITY OF DIODES, LEDS, ELECTROLYTIC CAPACITORS AND IC PIN 1.
4. LEAD-FREE SOLDER PROCESS REQUIRED: <YES/NO>.
5. CLEANING PROCESS: <NO-CLEAN/CLEAN REQUIRED>.
6. X-RAY INSPECTION REQUIRED FOR: <BGA/QFN/DFN/LGA/etc.>.
7. AOI REQUIRED AFTER REFLOW: <YES/NO>.
8. PROGRAMMING REQUIRED BEFORE FUNCTIONAL TEST: <YES/NO>.
9. FUNCTIONAL TEST PROCEDURE: <document reference>.
10. CONFORMAL COATING: <YES/NO>, MASK CONNECTORS/TEST POINTS AS SPECIFIED.
11. TORQUE REQUIREMENTS FOR MECHANICAL HARDWARE: <if applicable>.
```

## 5. Notas no esquemático

```text
SCHEMATIC NOTES

1. ALL COMPONENT VALUES SHALL BE VERIFIED AGAINST BOM REVISION <REV>.
2. ALL IC PINOUTS SHALL BE VERIFIED AGAINST MANUFACTURER DATASHEETS.
3. POWER NETS ARE NAMED BY NOMINAL VOLTAGE AND DOMAIN.
4. ISOLATED DOMAINS SHALL NOT BE SHORTED EXCEPT AT APPROVED COMPONENTS.
5. ALL EXTERNAL INTERFACES SHALL BE REVIEWED FOR ESD/EMC PROTECTION.
6. ALL CONTROLLED IMPEDANCE NETS ARE LISTED IN THE PCB CONSTRAINTS.
7. CREEPAGE AND CLEARANCE ARE DEFINED BY THE INSULATION TABLE ON SHEET <N>.
8. DNP/DNI COMPONENTS ARE IDENTIFIED IN THE BOM AND VARIANT TABLE.
```
