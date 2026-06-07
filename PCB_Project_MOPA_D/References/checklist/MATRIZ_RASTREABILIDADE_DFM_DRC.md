# Matriz de Rastreabilidade DFM/DRC/ERC

Use esta matriz para conectar requisito, regra de ECAD, evidência e resultado de inspeção.

| ID | Categoria | Requisito | Regra no ECAD | Valor | Fonte | Evidência | Status |
|---|---|---|---|---:|---|---|---|
| DFM-001 | Fabricação | Mínima trilha | Width Constraint |  | Capabilities fabricante | DRC report |  |
| DFM-002 | Fabricação | Mínimo espaçamento | Clearance Constraint |  | Capabilities fabricante | DRC report |  |
| DFM-003 | Furação | Drill mínimo | Routing Via Style / Drill Rules |  | Capabilities fabricante | Drill table |  |
| DFM-004 | Furação | Annular ring | Manufacturing / Annular Ring |  | Capabilities fabricante | DRC report |  |
| DFM-005 | Máscara | Solder mask dam | Mask Expansion |  | Capabilities fabricante | Gerber viewer |  |
| DFM-006 | Serigrafia | Largura/altura mínima | Silk to solder mask / text |  | Capabilities fabricante | Gerber viewer |  |
| IMP-001 | Impedância | 50 Ω single-ended | Impedance Profile | 50 Ω | Stackup fabricante | Impedance report |  |
| IMP-002 | Impedância | Par diferencial | Differential Pair Routing |  | Interface/datasheet | Diff pair report |  |
| SAFE-001 | Segurança | Clearance HV | Electrical Clearance |  | IEC/norma aplicável | DRC report |  |
| SAFE-002 | Segurança | Creepage HV | Physical path/manual + DRC |  | IEC/norma aplicável | Insulation table |  |
| PWR-001 | Potência | Trilha de corrente | Width/Current rule |  | IPC-2152/cálculo | Cálculo anexado |  |
| ASM-001 | Montagem | Courtyard | Component clearance |  | EMS/IPC-7351 | DRC report |  |
| ASM-002 | Montagem | Pin 1/polaridade | Assembly/Silkscreen |  | Datasheet/EMS | Assembly drawing |  |
| TEST-001 | Teste | Test points | Testpoint rule |  | Plano de teste | DRC report |  |
