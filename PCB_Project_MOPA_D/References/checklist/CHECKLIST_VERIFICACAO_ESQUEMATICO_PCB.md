# Checklist Profissional de Verificação de Esquemático e PCB

**Documento:** Checklist de revisão rígida de esquemático, biblioteca, PCB, documentação de fabricação e pacote de liberação  
**Aplicação:** placas eletrônicas em geral, incluindo projetos industriais, embarcados, instrumentação, IoT, produtos com requisitos de EMC, segurança elétrica e produção seriada  
**Ferramenta de referência:** Altium Designer, mas o checklist é aplicável a outros ECADs  
**Nível de rigor recomendado:** revisão formal por pares, com evidência objetiva e aprovação por gate  
**Versão:** 1.0  
**Data:** 2026-06-07  

---

## 1. Objetivo

Este checklist define uma rotina profissional e rígida para revisar:

- biblioteca de componentes;
- símbolos esquemáticos;
- footprints;
- parâmetros de BOM;
- encapsulamentos e part numbers;
- esquemático;
- regras elétricas;
- stackup;
- regras de projeto do PCB;
- impedância controlada;
- espaçamentos de segurança, clearance e creepage;
- planos de referência;
- documentação em camadas mecânicas do PCB;
- documentação no esquemático;
- arquivos finais de fabricação, montagem e teste.

O objetivo é impedir a liberação de uma placa para fabricação quando houver incerteza relevante sobre componente, encapsulamento, footprint, restrição de fabricante, stackup, impedância, segurança elétrica, montagem ou rastreabilidade.

---

## 2. Princípio de uso

Cada item deve receber um dos seguintes estados:

| Estado | Significado |
|---|---|
| `OK` | Verificado com evidência objetiva. |
| `N/A` | Não aplicável ao projeto, com justificativa. |
| `NCR` | Não conformidade aberta. Bloqueia ou condiciona a liberação. |
| `RISK_ACCEPTED` | Risco técnico aceito formalmente, com responsável e justificativa. |
| `OPEN` | Ainda não verificado. Não liberar fabricação. |

Nenhum item crítico pode permanecer como `OPEN` ou `NCR` no release final.

---

## 3. Classificação de severidade

| Severidade | Critério | Ação |
|---|---|---|
| `BLOCKER` | Pode causar placa infabricável, curto, falha de segurança, componente incompatível, montagem impossível ou não conformidade regulatória. | Não liberar. |
| `MAJOR` | Pode causar retrabalho, queda de rendimento, falha intermitente, dificuldade de teste ou baixa confiabilidade. | Corrigir antes do lote piloto ou justificar formalmente. |
| `MINOR` | Afeta documentação, estética, padronização ou melhoria de manutenção. | Corrigir antes da revisão final quando possível. |
| `INFO` | Observação técnica sem impacto imediato. | Registrar. |

---

## 4. Gates de liberação

### Gate 0 — Preparação do projeto

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G0-001 | Requisitos elétricos, mecânicos, ambientais e regulatórios definidos. | BLOCKER | Documento de requisitos ou PRD técnico. |
| G0-002 | Classe de aplicação definida: protótipo, industrial, médico, automotivo, segurança, RF, alta tensão, alta corrente etc. | BLOCKER | Declaração no projeto. |
| G0-003 | Fabricante de PCB candidato definido antes do fechamento das regras. | BLOCKER | Link/documento de capacidades do fabricante. |
| G0-004 | Montadora/EMS candidata definida quando houver SMT/THT em produção. | MAJOR | Regras de montagem, stencil e painelização. |
| G0-005 | Critérios IPC ou equivalentes definidos: classe de desempenho, aceitabilidade e montagem. | BLOCKER | Nota no esquemático e desenho de fabricação. |
| G0-006 | Critérios de segurança elétrica definidos quando houver tensão perigosa, isolamento, rede elétrica, paciente, usuário ou acessibilidade. | BLOCKER | Tabela de insulation coordination. |
| G0-007 | Premissas de ambiente: temperatura, umidade, altitude, poluição, vibração, corrente, dissipação e vida útil. | MAJOR | Tabela de premissas. |

### Gate 1 — Biblioteca aprovada

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G1-001 | Todo componente possui datasheet original do fabricante, com revisão identificada. | BLOCKER | Link ou PDF controlado. |
| G1-002 | Todo componente possui Manufacturer Part Number, fabricante e package code exato. | BLOCKER | Parâmetros na biblioteca/BOM. |
| G1-003 | Footprint validado contra desenho mecânico do datasheet, não apenas contra biblioteca genérica. | BLOCKER | Print ou registro de conferência. |
| G1-004 | Símbolo validado contra pinout oficial do datasheet. | BLOCKER | Revisão por pares. |
| G1-005 | Componente possui ciclo de vida verificado: active, NRND, obsolete, EOL ou alternativa. | MAJOR | Registro de suprimentos. |
| G1-006 | Componentes críticos possuem segunda fonte ou risco de single-source aceito. | MAJOR | AVL/AML. |
| G1-007 | EPAD, exposed pad, thermal pad, center pad ou power pad foram tratados no footprint e no esquemático. | BLOCKER | Pad, net e notas de montagem. |
| G1-008 | Componentes polarizados possuem marcação inequívoca de pin 1, ânodo/cátodo, positivo/negativo ou orientação. | BLOCKER | Silkscreen, assembly layer e 3D. |
| G1-009 | Altura máxima do componente foi registrada quando houver gabinete, shield, dissipador ou empilhamento. | MAJOR | Modelo 3D ou parâmetro Height. |
| G1-010 | Parâmetros de componentes passivos incluem valor, tolerância, potência, tensão, dielétrico, coeficiente térmico, package e tecnologia. | MAJOR | BOM completa. |

### Gate 2 — Esquemático aprovado

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G2-001 | ERC executado sem erro crítico. | BLOCKER | Relatório ERC arquivado. |
| G2-002 | Todas as páginas possuem título, número, revisão, autor e descrição funcional. | MINOR | PDF do esquemático. |
| G2-003 | Topologia do sistema clara: blocos, domínios de alimentação, domínios de terra, interfaces e isolamento. | MAJOR | Página de arquitetura. |
| G2-004 | Power tree revisada com tensão nominal, faixa, corrente máxima, dissipação e sequência de power-up. | BLOCKER | Tabela de power budget. |
| G2-005 | Pinos EN, RESET, BOOT, MODE, strap, address select e interrupt possuem estados definidos. | BLOCKER | Pull-up/down ou justificativa. |
| G2-006 | Todos os pinos NC, DNC, exposed pad e thermal pad seguem o datasheet. | BLOCKER | Conferência do datasheet. |
| G2-007 | Desacoplamento por IC revisado: valor, tensão, dielétrico, distância esperada e loop de corrente. | MAJOR | Notas próximas ao IC ou review. |
| G2-008 | Interfaces externas possuem proteção adequada: ESD, TVS, filtro, série, common-mode choke, fusível, PTC ou proteção equivalente quando necessário. | MAJOR | Esquemático revisado. |
| G2-009 | Todos os conectores possuem pinout, orientação, corrente por pino, chaveamento mecânico e pinagem reversa revisados. | BLOCKER | Tabela de cabos/conectores. |
| G2-010 | Nets críticos possuem classes definidas: alta corrente, alta tensão, RF, 50 Ω, diferencial, ADC, clock, isolamento etc. | BLOCKER | Net classes/constraints. |

### Gate 3 — Stackup e regras de fabricação aprovados

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G3-001 | Stackup é compatível com o fabricante escolhido. | BLOCKER | Stackup do fabricante ou aprovado pelo CAM. |
| G3-002 | Número de camadas, espessura total, cobre externo/interno, prepreg/core e Tg definidos. | BLOCKER | Tabela de stackup. |
| G3-003 | Regras mínimas de trilha, espaçamento, drill, annular ring, máscara e serigrafia vêm do fabricante real, não do default do ECAD. | BLOCKER | Tabela de capacidades DFM. |
| G3-004 | Impedâncias controladas foram calculadas com stackup real e tolerância do fabricante. | BLOCKER | Tabela de impedância. |
| G3-005 | Planos de referência contínuos sob sinais de 50 Ω e pares diferenciais foram verificados. | BLOCKER | Revisão visual + DRC. |
| G3-006 | Via structure validada: PTH, blind, buried, microvia, via-in-pad, filled, capped, tented, plugged. | MAJOR | Notas de fabricação. |
| G3-007 | Clearance e creepage possuem regra específica por classe de tensão e isolamento. | BLOCKER | DRC + tabela de isolamento. |
| G3-008 | Recortes, slots e keepouts de isolamento foram modelados corretamente em todas as camadas necessárias. | BLOCKER | Camadas mecânicas + DRC. |
| G3-009 | PTH, NPTH e furos mecânicos possuem tolerância e plating definidos. | MAJOR | Drill table. |
| G3-010 | Regras de solda/máscara/pasta foram revisadas por tecnologia: QFN, BGA, TQFP, 0402/0201, conectores, EPAD. | MAJOR | Footprint + paste layer. |

### Gate 4 — Layout aprovado

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G4-001 | DRC completo executado sem violação crítica. | BLOCKER | Relatório DRC arquivado. |
| G4-002 | Placement revisado por função, fluxo de sinal, dissipação, manutenção, montagem e inspeção. | MAJOR | Review de placement. |
| G4-003 | Componentes críticos próximos aos pinos corretos: desacoplamento, cristal, filtros, shunts, ADC reference, bootstrap, snubber. | MAJOR | Revisão visual. |
| G4-004 | Planos de terra e alimentação não possuem ilhas órfãs, gargalos ou retornos interrompidos. | BLOCKER | Revisão de planos. |
| G4-005 | Trilhas de alta corrente dimensionadas por corrente, temperatura e cobre. | BLOCKER | Cálculo ou simulação. |
| G4-006 | Interfaces de 50 Ω possuem largura, gap, referência, transições, vias e retorno controlados. | BLOCKER | Regras + inspeção. |
| G4-007 | Pares diferenciais possuem impedância, acoplamento, comprimento, skew e retorno controlados. | BLOCKER | Relatório de constraints. |
| G4-008 | Separação de domínios ruidosos/sensíveis foi respeitada: power, digital, analógico, RF, sensores, isolado. | MAJOR | Review por domínio. |
| G4-009 | Furos de fixação possuem clearance mecânico, anel, keepout, cobre afastado e conexão ao terra definida. | MAJOR | Camada mecânica. |
| G4-010 | Serigrafia não invade pads, vias expostas indevidas, área de solda ou componente. | MINOR | DRC + Gerber viewer. |

### Gate 5 — Pacote de fabricação/montagem aprovado

| ID | Item | Severidade | Evidência esperada |
|---|---|---:|---|
| G5-001 | Gerbers, Gerber X2/X3, ODB++ ou IPC-2581 gerados conforme exigência do fabricante. | BLOCKER | Pacote de saída. |
| G5-002 | NC Drill/Route gerado com unidades, formato, PTH/NPTH e slots corretos. | BLOCKER | Drill drawing e CAM viewer. |
| G5-003 | Desenho de fabricação inclui stackup, acabamento, cobre, material, tolerâncias e notas. | BLOCKER | Fab drawing. |
| G5-004 | Desenho de montagem inclui top/bottom, polaridade, pin 1, DNP, variantes e referências. | BLOCKER | Assembly drawing. |
| G5-005 | BOM contém MPN, fabricante, designators, quantidade, valor, package, tensão/potência/tolerância e alternativos. | BLOCKER | BOM revisada. |
| G5-006 | Pick-and-place contém coordenadas, rotação, lado, designator e origem consistente com a montadora. | BLOCKER | Centroid/CPL revisado. |
| G5-007 | Netlist de teste, preferencialmente IPC-D-356 quando suportado, gerada para comparação CAM/teste elétrico. | MAJOR | Netlist arquivada. |
| G5-008 | Arquivos finais foram abertos em viewer independente, não apenas no ECAD. | BLOCKER | Registro de inspeção CAM. |
| G5-009 | Pacote possui manifesto, hash/checksum e revisão congelada. | MAJOR | Manifesto de release. |
| G5-010 | Projeto fonte, PDF esquemático, PDF PCB e relatórios estão arquivados junto do release. | MAJOR | Pasta de release. |

---

## 5. Checklist de biblioteca de componentes

### 5.1 Datasheet, identificação e rastreabilidade

| ID | Verificação | Severidade |
|---|---|---:|
| LIB-001 | O datasheet utilizado é do fabricante original, não de distribuidor ou página agregadora. | BLOCKER |
| LIB-002 | A revisão/data do datasheet foi registrada. | MAJOR |
| LIB-003 | O MPN completo inclui sufixos de package, temperatura, reel/tray, acabamento, tensão, precisão e variante. | BLOCKER |
| LIB-004 | O fabricante foi registrado em campo separado, sem abreviação ambígua. | MAJOR |
| LIB-005 | O componente possui categoria: resistor, capacitor, IC, conector, mecânico, proteção, indutor etc. | MINOR |
| LIB-006 | O status de lifecycle foi verificado em distribuidor/fabricante. | MAJOR |
| LIB-007 | Foi registrada alternativa compatível ou indicação de single-source. | MAJOR |
| LIB-008 | RoHS/REACH/halogen-free/lead-free foram verificados quando exigidos pelo produto. | MAJOR |
| LIB-009 | MSL foi registrado para componentes sensíveis à umidade. | MAJOR |
| LIB-010 | Temperatura operacional do componente é compatível com ambiente e dissipação do projeto. | MAJOR |

### 5.2 Símbolo esquemático

| ID | Verificação | Severidade |
|---|---|---:|
| SYM-001 | Pinout conferido pino a pino contra datasheet. | BLOCKER |
| SYM-002 | Numeração dos pinos bate exatamente com o package escolhido. | BLOCKER |
| SYM-003 | Nomes dos pinos seguem datasheet, incluindo barras de negação, sufixos P/N, +/− e função alternativa. | MAJOR |
| SYM-004 | Pinos de alimentação estão visíveis ou documentados; evitar power pins ocultos em componentes críticos. | MAJOR |
| SYM-005 | Pinos NC e DNC estão explicitamente tratados. | BLOCKER |
| SYM-006 | Pinos passivos, power input, output, open drain, tri-state e bidirectional possuem tipo elétrico correto para ERC. | MAJOR |
| SYM-007 | Componentes multi-unit possuem unidades consistentes e pinos de power/gate separados quando apropriado. | MAJOR |
| SYM-008 | EPAD/thermal pad aparece como pino no esquemático quando precisa de net definida. | BLOCKER |
| SYM-009 | Símbolo indica função, polaridade e orientação suficiente para revisão humana. | MINOR |
| SYM-010 | Símbolos de conectores indicam lado, sentido, pin 1 e interface externa. | MAJOR |

### 5.3 Footprint e encapsulamento

| ID | Verificação | Severidade |
|---|---|---:|
| FPT-001 | Footprint foi criado com base no package exato do datasheet ou norma de land pattern aplicável. | BLOCKER |
| FPT-002 | Dimensões de pads, pitch, span, courtyard, assembly outline e body outline foram conferidas. | BLOCKER |
| FPT-003 | Pad numbering confere com símbolo e datasheet. | BLOCKER |
| FPT-004 | Pin 1 está marcado no top overlay e assembly layer, sem ambiguidade. | BLOCKER |
| FPT-005 | Solder mask expansion e paste mask expansion foram revisadas. | MAJOR |
| FPT-006 | Para QFN/DFN/LGA com EPAD, paste window foi particionada quando necessário para reduzir voiding. | MAJOR |
| FPT-007 | Thermal vias em EPAD possuem diâmetro, tenting, plugging/filling e distância compatíveis com fabricante e montagem. | MAJOR |
| FPT-008 | Via-in-pad só é usado quando o fabricante/montadora suporta filled/capped/plated conforme necessidade. | BLOCKER |
| FPT-009 | Courtyard respeita espaço para montagem, inspeção e retrabalho. | MAJOR |
| FPT-010 | 3D model, altura e origem mecânica conferidos quando houver restrição de gabinete, shield ou conector. | MAJOR |
| FPT-011 | Pads THT possuem drill, tolerância, annular ring e plating compatíveis com corrente, mecânica e fabricante. | BLOCKER |
| FPT-012 | NPTH está definido como non-plated e em camada/arquivo correto. | BLOCKER |
| FPT-013 | Furos oblongos, slots, castellation ou edge plating estão documentados em camada mecânica e drill/route. | BLOCKER |
| FPT-014 | Componentes polarizados e conectores possuem prevenção contra montagem invertida quando possível. | MAJOR |
| FPT-015 | Footprint possui camadas corretas: copper, mask, paste, overlay, assembly, courtyard, 3D/mechanical. | MAJOR |

### 5.4 Parâmetros de BOM

| ID | Verificação | Severidade |
|---|---|---:|
| BOM-001 | Campo `Manufacturer` preenchido. | BLOCKER |
| BOM-002 | Campo `Manufacturer Part Number` preenchido. | BLOCKER |
| BOM-003 | Valor e unidade padronizados: Ω, kΩ, µF, nF, V, A, W, %, ppm/°C. | MAJOR |
| BOM-004 | Capacitores possuem tensão nominal, dielétrico, tolerância e package. | MAJOR |
| BOM-005 | Resistores possuem potência, tolerância, tecnologia e package. | MAJOR |
| BOM-006 | Indutores possuem corrente de saturação, DCR, tolerância e package. | MAJOR |
| BOM-007 | Diodos/TVS possuem tensão, corrente, potência, capacitância quando aplicável e package. | MAJOR |
| BOM-008 | Reguladores/conversores possuem package térmico e corrente compatível. | MAJOR |
| BOM-009 | Itens DNP/DNI possuem campo de montagem explícito. | MAJOR |
| BOM-010 | Alternativos não são apenas “equivalentes”; têm footprint, pinout, parâmetros críticos e disponibilidade validados. | BLOCKER |

---

## 6. Checklist de esquemático

### 6.1 Organização, páginas e revisão

| ID | Verificação | Severidade |
|---|---|---:|
| SCH-001 | Todas as folhas têm título, número, revisão e identificação do projeto. | MINOR |
| SCH-002 | Hierarquia e conectores entre folhas estão claros. | MAJOR |
| SCH-003 | Não existem labels genéricos ambíguos como `VCC`, `GND1`, `SIGNAL`, `DATA` sem contexto. | MAJOR |
| SCH-004 | Nets de potência seguem convenção explícita: `+3V3`, `+5V_ISO`, `AGND`, `DGND`, `PGND`, `CHASSIS`, `EARTH`. | MAJOR |
| SCH-005 | Existe página de blocos ou índice para circuitos médios/grandes. | MINOR |
| SCH-006 | Conexões off-sheet/harness/ports possuem direção e nome consistentes. | MAJOR |
| SCH-007 | ERC foi executado após anotação, compilação e ECO final. | BLOCKER |
| SCH-008 | Não há componentes sem designator. | BLOCKER |
| SCH-009 | Não há footprints ausentes nos componentes montáveis. | BLOCKER |
| SCH-010 | Variantes de montagem foram revisadas. | MAJOR |

### 6.2 Alimentação e proteção

| ID | Verificação | Severidade |
|---|---|---:|
| PWR-001 | Faixa de tensão de entrada documentada. | BLOCKER |
| PWR-002 | Proteção contra inversão, surto, ESD, sobrecorrente e transiente avaliada. | MAJOR |
| PWR-003 | Diodos, fusíveis, PTCs e TVS possuem ratings compatíveis com worst-case. | BLOCKER |
| PWR-004 | Reguladores possuem margem térmica, corrente de pico e estabilidade com capacitores escolhidos. | BLOCKER |
| PWR-005 | Sequenciamento de rails foi analisado quando ICs exigem ordem de alimentação. | MAJOR |
| PWR-006 | Rails externos possuem limitação de corrente ou proteção adequada. | MAJOR |
| PWR-007 | Pinos EN/UVLO possuem divisores/pull-ups compatíveis com thresholds e tolerâncias. | BLOCKER |
| PWR-008 | Pinos bootstrap, compensation, soft-start e feedback seguem layout recomendado pelo fabricante. | MAJOR |
| PWR-009 | Plano de potência e retorno de corrente são compatíveis com layout planejado. | MAJOR |
| PWR-010 | Há power budget com corrente típica, máxima e margem. | MAJOR |

### 6.3 Sinais digitais, clocks e comunicação

| ID | Verificação | Severidade |
|---|---|---:|
| DIG-001 | Níveis lógicos compatíveis entre ICs. | BLOCKER |
| DIG-002 | Interfaces I²C possuem pull-ups adequados por tensão, capacitância e velocidade. | MAJOR |
| DIG-003 | SPI/UART/CAN/RS-485/Ethernet/USB possuem terminação e proteção quando necessário. | MAJOR |
| DIG-004 | Clocks e cristais seguem circuito recomendado: capacitores, resistor, drive level e aterramento. | MAJOR |
| DIG-005 | Strapping pins de microcontroladores e SoCs estão definidos para boot seguro. | BLOCKER |
| DIG-006 | Linhas de reset/programação/debug estão acessíveis em produção. | MAJOR |
| DIG-007 | Sinais de alta velocidade possuem net class e regras específicas antes do layout. | BLOCKER |
| DIG-008 | Não há entradas digitais flutuantes. | BLOCKER |
| DIG-009 | Sinais que saem da placa têm proteção ou filtragem definida quando expostos. | MAJOR |
| DIG-010 | Sinais diferenciais possuem polaridade P/N consistente em símbolo, conector e layout. | BLOCKER |

### 6.4 Analógico, sensores e referências

| ID | Verificação | Severidade |
|---|---|---:|
| ANA-001 | Referência de ADC/DAC tem fonte, desacoplamento, ruído e impedância revisados. | MAJOR |
| ANA-002 | Front-end analógico possui filtragem anti-aliasing quando aplicável. | MAJOR |
| ANA-003 | Sensores resistivos/capacitivos/indutivos possuem polarização e proteção compatíveis. | MAJOR |
| ANA-004 | Entradas analógicas externas possuem proteção contra ESD/sobretensão. | MAJOR |
| ANA-005 | Caminhos de retorno analógico foram planejados. | MAJOR |
| ANA-006 | Shunts e sense resistors possuem Kelvin sense quando necessário. | MAJOR |
| ANA-007 | Amplificadores operacionais respeitam common-mode, output swing, GBW, offset e ruído. | MAJOR |
| ANA-008 | Capacitores em sinais analógicos têm dielétrico apropriado para estabilidade e linearidade. | MAJOR |
| ANA-009 | Separação de domínios analógico/digital está documentada. | MAJOR |
| ANA-010 | Pontos de teste foram previstos para calibração e diagnóstico. | MAJOR |

### 6.5 Segurança elétrica, isolamento, creepage e clearance

| ID | Verificação | Severidade |
|---|---|---:|
| SAFE-001 | Máxima tensão contínua, transitória e impulso entre domínios foi definida. | BLOCKER |
| SAFE-002 | Tipo de isolamento definido: funcional, básico, suplementar, duplo ou reforçado. | BLOCKER |
| SAFE-003 | Grau de poluição, categoria de sobretensão, altitude e material group/CTI definidos quando aplicável. | BLOCKER |
| SAFE-004 | Clearance mínimo foi calculado pela norma aplicável. | BLOCKER |
| SAFE-005 | Creepage mínimo foi calculado pela norma aplicável. | BLOCKER |
| SAFE-006 | Slots/rasgos de isolamento foram considerados quando necessário. | MAJOR |
| SAFE-007 | Regras de clearance no ECAD refletem os cálculos, não apenas o mínimo do fabricante. | BLOCKER |
| SAFE-008 | Barreira de isolamento está visível no esquemático e no PCB. | MAJOR |
| SAFE-009 | Componentes de isolamento possuem certificação/rating compatível. | BLOCKER |
| SAFE-010 | Distância de cobre a borda, furos, parafusos, dissipadores, chassis e conectores foi verificada. | BLOCKER |
| SAFE-011 | Conformal coating não foi usado como justificativa automática sem norma/processo qualificado. | BLOCKER |
| SAFE-012 | Camadas internas também respeitam distância entre potenciais perigosos e domínios SELV/PELV ou acessíveis. | BLOCKER |

---

## 7. Checklist de stackup, regras e impedância

### 7.1 Capacidades do fabricante

Preencher a tabela abaixo antes de iniciar ou congelar o layout.

| Parâmetro | Valor do fabricante | Valor usado no projeto | OK/NCR |
|---|---:|---:|---|
| Número de camadas |  |  |  |
| Espessura total |  |  |  |
| Tolerância de espessura |  |  |  |
| Cobre externo acabado |  |  |  |
| Cobre interno |  |  |  |
| Mínima trilha/espaço |  |  |  |
| Mínimo drill mecânico |  |  |  |
| Mínimo drill laser |  |  |  |
| Annular ring mínimo |  |  |  |
| Aspect ratio máximo |  |  |  |
| Solder mask dam mínimo |  |  |  |
| Solder mask registration |  |  |  |
| Silkscreen line/height mínimo |  |  |  |
| Tolerância de furo PTH |  |  |  |
| Tolerância de furo NPTH |  |  |  |
| Tolerância de contorno |  |  |  |
| Acabamento superficial disponível |  |  |  |
| Impedância controlada disponível |  |  |  |
| Tolerância de impedância |  |  |  |
| Via tenting/plug/fill/cap disponível |  |  |  |
| Via-in-pad disponível |  |  |  |
| Edge plating/castellation disponível |  |  |  |
| CTI/material group disponível |  |  |  |
| Tg e material base |  |  |  |

### 7.2 Stackup

| ID | Verificação | Severidade |
|---|---|---:|
| STK-001 | Stackup é simétrico ou o desbalanceamento foi aprovado pelo fabricante. | MAJOR |
| STK-002 | Camadas possuem nomes funcionais claros: `L1_TOP_SIGNAL`, `L2_GND`, `L3_PWR`, `L4_BOTTOM_SIGNAL`. | MINOR |
| STK-003 | Cada camada de sinal crítica tem plano de referência adjacente. | BLOCKER |
| STK-004 | Planos de GND são preferencialmente contínuos sob clocks, RF, USB, Ethernet, SPI rápido e ADC sensível. | MAJOR |
| STK-005 | Separação entre planos de potência e GND considera capacitância distribuída e retorno. | MAJOR |
| STK-006 | Espessuras de dielétrico e cobre correspondem ao fabricante. | BLOCKER |
| STK-007 | Material, Dk, Df e frequência de referência definidos para impedância. | BLOCKER |
| STK-008 | Stackup foi congelado antes do cálculo final de impedância. | BLOCKER |
| STK-009 | Regras de plano interno incluem antipads suficientes para drills e alta tensão. | BLOCKER |
| STK-010 | Cross-section/desenho do stack foi inserido no pacote de fabricação. | BLOCKER |

### 7.3 Impedância controlada e 50 Ω

| ID | Verificação | Severidade |
|---|---|---:|
| IMP-001 | Toda net de 50 Ω está identificada em net class específica. | BLOCKER |
| IMP-002 | Tipo de geometria definido: microstrip, stripline, coplanar waveguide, differential pair etc. | BLOCKER |
| IMP-003 | Largura e clearance calculados com stackup real. | BLOCKER |
| IMP-004 | Tolerância de fabricação considerada: espessura dielétrica, cobre, etch compensation, solder mask. | MAJOR |
| IMP-005 | Plano de referência não possui fendas, splits, recortes ou mudanças bruscas sob a trilha. | BLOCKER |
| IMP-006 | Transições por via possuem vias de retorno/stitching próximas. | MAJOR |
| IMP-007 | Neckdowns em pads/conectores foram avaliados e minimizados. | MAJOR |
| IMP-008 | Stubs de vias em sinais críticos foram avaliados. | MAJOR |
| IMP-009 | Acoplamento com outras trilhas respeita espaçamento para evitar crosstalk. | MAJOR |
| IMP-010 | Tabela de impedâncias foi incluída no desenho de fabricação. | BLOCKER |
| IMP-011 | Cupom de impedância solicitado quando exigido por produção/qualidade. | MAJOR |
| IMP-012 | O fabricante confirmou que controlará impedância por geometria especificada ou por ajuste de processo. | BLOCKER |

---

## 8. Checklist de layout PCB

### 8.1 Placement

| ID | Verificação | Severidade |
|---|---|---:|
| PLC-001 | Conectores posicionados conforme restrições mecânicas, cabo e acesso. | BLOCKER |
| PLC-002 | Componentes com dissipação térmica têm área de cobre, vias térmicas e afastamento adequados. | MAJOR |
| PLC-003 | Componentes críticos de fontes chaveadas seguem loop mínimo: switch node, diode/FET, input cap, output cap, ground return. | BLOCKER |
| PLC-004 | Cristais e clocks estão próximos ao IC, com área protegida e retorno controlado. | MAJOR |
| PLC-005 | ADC, referência, amplificadores e sensores estão afastados de fontes de ruído. | MAJOR |
| PLC-006 | Componentes altos não conflitam com gabinete, shield, dissipador, display ou outra placa. | BLOCKER |
| PLC-007 | Polaridade e pin 1 visíveis após montagem sempre que possível. | MAJOR |
| PLC-008 | Fiduciais globais e locais foram previstos conforme necessidade SMT. | MAJOR |
| PLC-009 | Test points acessíveis por lado, altura e fixture. | MAJOR |
| PLC-010 | Componentes THT respeitam processo de solda, wave/selective/manual. | MAJOR |

### 8.2 Roteamento

| ID | Verificação | Severidade |
|---|---|---:|
| RTE-001 | Larguras de trilha foram definidas por corrente, impedância, queda de tensão e aquecimento. | BLOCKER |
| RTE-002 | Gargalos de cobre em trilhas de potência foram eliminados. | MAJOR |
| RTE-003 | Retorno de corrente de sinais rápidos é contínuo e próximo. | BLOCKER |
| RTE-004 | Não há roteamento crítico cruzando split de plano. | BLOCKER |
| RTE-005 | Pares diferenciais mantêm acoplamento, simetria e polaridade. | BLOCKER |
| RTE-006 | Comprimentos casados quando exigidos por interface. | MAJOR |
| RTE-007 | Vias em sinais críticos são minimizadas e acompanhadas de retorno. | MAJOR |
| RTE-008 | Trilhas de alta tensão possuem afastamento e barreira física quando necessário. | BLOCKER |
| RTE-009 | Trilhas de alta corrente não passam sob componentes sensíveis sem análise. | MAJOR |
| RTE-010 | Ângulos, teardrops e neckdowns foram avaliados conforme processo. | MINOR |

### 8.3 Planos, polígonos e terras

| ID | Verificação | Severidade |
|---|---|---:|
| PLN-001 | Polygons foram repourados antes do DRC e geração de saída. | BLOCKER |
| PLN-002 | Não há ilhas de cobre desconectadas críticas. | MAJOR |
| PLN-003 | Conexões a pads usam thermal relief ou conexão sólida conforme corrente, soldabilidade e dissipação. | MAJOR |
| PLN-004 | Separação AGND/DGND/PGND/ISO_GND tem estratégia documentada; não é separada por hábito. | MAJOR |
| PLN-005 | Planos internos possuem antipads suficientes em furos e slots. | BLOCKER |
| PLN-006 | Planos de alta corrente possuem múltiplas vias quando mudam de camada. | MAJOR |
| PLN-007 | Stitching vias conectam planos de GND em bordas, conectores e transições de camada quando apropriado. | MAJOR |
| PLN-008 | Chassis/earth/shield possuem conexão controlada ao GND funcional. | MAJOR |
| PLN-009 | Cobre próximo à borda respeita fabricação, segurança e risco de exposição. | MAJOR |
| PLN-010 | Não há cobre indevido em área de antena, RF keepout ou sensor sensível. | BLOCKER |

### 8.4 Mecânica, montagem e painelização

| ID | Verificação | Severidade |
|---|---|---:|
| MEC-001 | Board outline está fechado, sem segmentos duplicados ou gaps. | BLOCKER |
| MEC-002 | Dimensões externas e tolerâncias estão no desenho de fabricação. | BLOCKER |
| MEC-003 | Furos de montagem têm PTH/NPTH correto e clearances. | BLOCKER |
| MEC-004 | Keepouts mecânicos aplicados em todas as camadas relevantes. | MAJOR |
| MEC-005 | Altura máxima de componentes foi checada em 3D. | MAJOR |
| MEC-006 | Painelização, fiduciais, tooling holes e rails foram definidos quando necessário. | MAJOR |
| MEC-007 | V-score, mouse bites, tabs e breakaway não interferem em componentes ou trilhas. | BLOCKER |
| MEC-008 | Conectores de borda, castellations ou edge plating possuem notas específicas. | BLOCKER |
| MEC-009 | Orientação de montagem top/bottom está clara. | MAJOR |
| MEC-010 | Áreas de manuseio, teste e programação foram consideradas. | MAJOR |

---

## 9. Documentação a incluir no esquemático

Recomenda-se adicionar folhas de documentação ao esquemático, especialmente em projetos profissionais.

### 9.1 Folha de capa

Incluir:

- nome do projeto;
- código da placa;
- revisão;
- autor/responsável;
- data;
- histórico de revisão;
- status: `DRAFT`, `REVIEW`, `RELEASED`, `OBSOLETE`;
- classe IPC pretendida;
- aplicação do produto;
- tensão de entrada;
- consumo máximo;
- interfaces externas;
- observações de segurança.

### 9.2 Folha de arquitetura

Incluir:

- diagrama de blocos;
- domínios de alimentação;
- domínios de terra;
- domínios isolados;
- interfaces externas;
- sinais de alta velocidade;
- caminhos de potência;
- pontos de teste principais.

### 9.3 Folha de requisitos elétricos

Tabela recomendada:

| Requisito | Valor | Tolerância | Evidência |
|---|---:|---:|---|
| Tensão de entrada |  |  |  |
| Corrente máxima |  |  |  |
| Temperatura operacional |  |  |  |
| Altitude |  |  |  |
| Grau de poluição |  |  |  |
| Isolamento requerido |  |  |  |
| Impedâncias controladas |  |  |  |
| Interfaces externas |  |  |  |

### 9.4 Folha de power budget

| Rail | Fonte | Cargas | Tensão | Corrente típica | Corrente máxima | Margem | Observações |
|---|---|---|---:|---:|---:|---:|---|
| +5V |  |  |  |  |  |  |  |
| +3V3 |  |  |  |  |  |  |  |
| +1V8 |  |  |  |  |  |  |  |

### 9.5 Folha de interfaces e cabos

| Conector | Pino | Net | Direção | Tensão | Corrente | Proteção | Cabo/externo |
|---|---:|---|---|---:|---:|---|---|
| J1 | 1 |  |  |  |  |  |  |

### 9.6 Folha de isolamento e segurança

| Domínio A | Domínio B | Tensão de trabalho | Isolamento | Clearance requerido | Creepage requerido | Norma/base | Observação |
|---|---|---:|---|---:|---:|---|---|
|  |  |  |  |  |  |  |  |

---

## 10. Documentação a incluir em camadas do PCB

A nomenclatura exata depende do ECAD, mas recomenda-se manter camadas mecânicas dedicadas e documentadas.

### 10.1 Camadas recomendadas

| Camada sugerida | Conteúdo |
|---|---|
| `MECH_BOARD_OUTLINE` | Contorno oficial da placa. |
| `MECH_FAB_DRAWING` | Dimensões, tolerâncias, notas de fabricação. |
| `MECH_STACKUP` | Tabela e corte do stackup. |
| `MECH_DRILL_TABLE` | Tabela de furos PTH, NPTH, slots e tolerâncias. |
| `MECH_ASSEMBLY_TOP` | Contorno dos componentes top, designators e polaridade. |
| `MECH_ASSEMBLY_BOTTOM` | Contorno dos componentes bottom, designators e polaridade. |
| `MECH_COURTYARD` | Área de montagem e keepout por componente. |
| `MECH_CRITICAL_NOTES` | Notas críticas: impedância, acabamento, IPC class, vias especiais. |
| `MECH_PANEL` | Painelização, rails, tooling holes, fiduciais e tabs. |
| `MECH_3D_HEIGHT` | Altura máxima e regiões proibidas. |

### 10.2 Notas mínimas de fabricação no PCB

Incluir no desenho de fabricação:

1. Código da placa, revisão e status.
2. Dimensões externas e tolerância.
3. Espessura total da placa e tolerância.
4. Número de camadas.
5. Material base e Tg.
6. Espessura de cobre interno e externo.
7. Acabamento superficial: ENIG, HASL, OSP, immersion silver etc.
8. Cor da solder mask.
9. Cor da legenda/silkscreen.
10. Classe IPC desejada.
11. Requisito RoHS/lead-free, se aplicável.
12. Requisito UL94 V-0, CTI ou material group, se aplicável.
13. Tabela de stackup.
14. Tabela de impedância controlada.
15. Tolerância de impedância.
16. Cupom de impedância, quando aplicável.
17. Via treatment: tented, plugged, filled, capped, via-in-pad.
18. Requisito de teste elétrico.
19. Requisito de inspeção.
20. Indicação de PTH, NPTH, slots e routs.
21. Indicação de edge plating/castellation, se aplicável.
22. Restrição de warpage, se crítica.
23. Painelização, se definida pelo designer.
24. Proibição de alteração de stackup sem aprovação de engenharia.
25. Solicitação de revisão CAM antes de produção.

### 10.3 Notas mínimas de montagem

Incluir no desenho de montagem:

1. Designators visíveis.
2. Orientação de pin 1.
3. Polaridade de diodos, LEDs, eletrolíticos e conectores.
4. Lista de componentes DNP/DNI.
5. Variantes de montagem.
6. Lado top/bottom.
7. Requisitos de solda lead-free.
8. Requisitos de limpeza/no-clean.
9. Requisitos de inspeção AOI/X-ray para BGA, QFN, DFN, LGA ou bottom-terminated components.
10. Requisitos de torque para conectores/parafusos, quando aplicável.
11. Requisitos de conformal coating, se aplicável.
12. Requisitos de programação e teste funcional.
13. Referência ao arquivo BOM e pick-and-place do mesmo release.

---

## 11. Pacote final de fabricação e montagem

### 11.1 Estrutura recomendada de pasta

```text
RELEASE_PCB_<PN>_<REV>_<YYYYMMDD>/
├─ 00_README/
│  ├─ RELEASE_MANIFEST.md
│  ├─ CHANGELOG.md
│  └─ APPROVAL_RECORD.md
├─ 01_SCHEMATIC/
│  ├─ schematic_<PN>_<REV>.pdf
│  └─ erc_report_<PN>_<REV>.pdf
├─ 02_PCB_FABRICATION/
│  ├─ gerbers_or_ipc2581_or_odbpp/
│  ├─ nc_drill/
│  ├─ fab_drawing_<PN>_<REV>.pdf
│  ├─ stackup_<PN>_<REV>.pdf
│  ├─ impedance_table_<PN>_<REV>.pdf
│  └─ ipc_d_356_netlist_<PN>_<REV>.ipc
├─ 03_ASSEMBLY/
│  ├─ bom_<PN>_<REV>.xlsx
│  ├─ pick_and_place_<PN>_<REV>.csv
│  ├─ assembly_top_<PN>_<REV>.pdf
│  ├─ assembly_bottom_<PN>_<REV>.pdf
│  └─ stencil_notes_<PN>_<REV>.pdf
├─ 04_MECHANICAL/
│  ├─ step_3d_<PN>_<REV>.step
│  ├─ dxf_outline_<PN>_<REV>.dxf
│  └─ enclosure_check_<PN>_<REV>.pdf
├─ 05_REPORTS/
│  ├─ drc_report_<PN>_<REV>.pdf
│  ├─ diff_pair_report_<PN>_<REV>.pdf
│  ├─ length_tuning_report_<PN>_<REV>.pdf
│  └─ cam_viewer_review_<PN>_<REV>.pdf
└─ 06_SOURCE_SNAPSHOT/
   ├─ ecad_project_archive_<PN>_<REV>.zip
   └─ library_snapshot_<PN>_<REV>.zip
```

### 11.2 Arquivos obrigatórios por tipo

| Arquivo | Protótipo | Produção | Observação |
|---|:---:|:---:|---|
| PDF do esquemático | Sim | Sim | Deve corresponder à revisão fabricada. |
| Relatório ERC | Sim | Sim | Sem erro crítico. |
| Gerbers X2/X3 ou equivalente | Sim | Sim | Conferir com CAM viewer. |
| NC Drill/Route | Sim | Sim | PTH/NPTH separados quando necessário. |
| Desenho de fabricação | Sim | Sim | Obrigatório em produção. |
| Stackup | Sim | Sim | Obrigatório se >2 camadas ou impedância. |
| Tabela de impedância | Se aplicável | Se aplicável | Obrigatória para 50 Ω/RF/diff. |
| BOM | Sim | Sim | Preferir MPN fechado. |
| Pick-and-place | Se montado | Sim | Revisar rotações. |
| Desenho de montagem | Se montado | Sim | Top e bottom. |
| STEP 3D | Recomendado | Sim | Especialmente com gabinete. |
| IPC-D-356/netlist | Recomendado | Sim | Quando fabricante suportar. |
| DRC report | Sim | Sim | Sem blocker. |
| Source snapshot | Sim | Sim | Para rastreabilidade. |

---

## 12. Critérios rígidos de bloqueio

Não liberar fabricação se qualquer uma das condições abaixo for verdadeira:

1. Componente sem MPN completo.
2. Footprint não validado contra datasheet.
3. Pinout do símbolo não revisado.
4. EPAD/thermal pad sem net definida ou sem decisão formal.
5. Stackup não confirmado com fabricante para placa multicamada crítica.
6. Regra de DRC usando valores default incompatíveis com o fabricante.
7. Impedância de 50 Ω sem stackup real.
8. Plano de referência cortado sob sinal crítico.
9. Creepage/clearance sem cálculo para tensão perigosa ou isolamento.
10. Arquivo de furação não conferido em CAM viewer.
11. Board outline inconsistente.
12. DRC com violação crítica aberta.
13. ERC com violação crítica aberta.
14. BOM sem fabricante e MPN.
15. Pick-and-place não revisado quando houver montagem automática.
16. Notas de fabricação ausentes em placa com requisito especial.
17. Furos PTH/NPTH ambíguos.
18. Via-in-pad sem processo de preenchimento/capeamento aprovado.
19. Componente obsoleto ou NRND sem aprovação.
20. Projeto fonte não arquivado na revisão do release.

---

## 13. Revisão por pares

### 13.1 Papéis

| Papel | Responsabilidade |
|---|---|
| Projetista eletrônico | Corrigir esquemático, biblioteca, PCB e documentação. |
| Revisor eletrônico | Verificar circuito, pinout, ERC, power, proteção e interfaces. |
| Revisor PCB | Verificar layout, DRC, stackup, fabricação e montagem. |
| Mecânico | Verificar outline, altura, conectores, fixação e gabinete. |
| Produção/EMS | Verificar montagem, BOM, pick-and-place, stencil e testabilidade. |
| Qualidade | Verificar rastreabilidade, release, critérios normativos e evidências. |

### 13.2 Evidência mínima

Cada revisão deve registrar:

- nome do revisor;
- data;
- revisão analisada;
- arquivos analisados;
- lista de não conformidades;
- decisão: aprovado, aprovado com restrição ou reprovado;
- assinatura ou aprovação eletrônica.

---

## 14. Referências técnicas recomendadas

Estas referências devem ser usadas como base de consulta, não como substituto da norma oficial adquirida/licenciada quando o projeto exigir conformidade formal.

| Referência | Uso típico |
|---|---|
| IPC-2221 | Requisitos genéricos de design de placas impressas. |
| IPC-7351 | Land patterns para componentes SMD. |
| IPC-6012 | Qualificação e desempenho de placas rígidas. |
| IPC-A-600 | Critérios de aceitabilidade de placas nuas. |
| IPC-A-610 | Critérios de aceitabilidade de montagens eletrônicas. |
| IPC-J-STD-001 | Requisitos para montagem soldada. |
| IPC-2152 | Dimensionamento de condutores por corrente e elevação de temperatura. |
| IPC-D-356 | Netlist para teste elétrico/fabricação. |
| IPC-2581 | Transferência digital de dados de fabricação/montagem. |
| Gerber X2/X3 | Transferência de dados de camadas, atributos e, no X3, dados de componentes. |
| ODB++ | Estrutura inteligente para troca de dados de fabricação, montagem e teste. |
| IEC 60664-1 | Clearance, creepage e coordenação de isolamento para baixa tensão. |
| IEC 60601-1 | Segurança básica e desempenho essencial para equipamentos médicos elétricos, quando aplicável. |
| UL 796 | Placas impressas e requisitos associados de segurança, quando aplicável. |
| Datasheets dos fabricantes | Fonte principal para pinout, package, layout recomendado e ratings. |
| Capabilities do fabricante de PCB | Fonte obrigatória para regras reais de fabricação. |
| Regras da EMS/montadora | Fonte obrigatória para montagem, stencil, painel e inspeção. |

### Links públicos úteis

- IPC-2221C: https://shop.ipc.org/ipc-2221/ipc-2221-standard-only/Revision-c/english  
- IPC-7351B: https://shop.ipc.org/ipc-7351/ipc-7351-standard-only/Revision-b/english  
- IPC-6012F: https://shop.ipc.org/ipc-6012/ipc-6012-standard-only/Revision-f/english  
- IPC-A-600M: https://shop.ipc.org/ipc-a-600/ipc-a-600-standard-only/Revision-m/english  
- IPC-2152: https://shop.ipc.org/ipc-2152/ipc-2152-standard-only  
- IPC-2581 Consortium: https://www.ipc2581.com/  
- IEC 60664-1:2020: https://webstore.iec.ch/en/publication/59671  
- Ucamco Gerber: https://www.ucamco.com/en/gerber  
- Ucamco Gerber X3: https://www.ucamco.com/en/gerber/gerber-x3  
- Siemens ODB++: https://www.siemens.com/en-us/products/pcb/odb-plus-plus/  
- Altium controlled impedance routing: https://www.altium.com/documentation/altium-designer/pcb/high-speed-design/interactively-routing-controlled-impedance  
- Altium layer stack: https://www.altium.com/documentation/altium-designer/pcb/defining-layer-stack  
- Altium design rule types: https://www.altium.com/documentation/altium-designer/pcb/design-rule-types  

---

## 15. Modelo de registro de não conformidade

| Campo | Conteúdo |
|---|---|
| ID | NCR-YYYY-NNN |
| Data |  |
| Projeto |  |
| Revisão |  |
| Origem | Biblioteca / Esquemático / PCB / Fabricação / Montagem / Teste |
| Severidade | BLOCKER / MAJOR / MINOR / INFO |
| Descrição |  |
| Evidência | Print, arquivo, página do datasheet, relatório DRC/ERC |
| Impacto |  |
| Ação corretiva |  |
| Responsável |  |
| Prazo |  |
| Status | OPEN / FIXED / VERIFIED / ACCEPTED |
| Verificador |  |
| Data de fechamento |  |

---

## 16. Modelo de aprovação final

| Aprovação | Nome | Data | Status | Observações |
|---|---|---|---|---|
| Engenharia eletrônica |  |  |  |  |
| Engenharia PCB |  |  |  |  |
| Mecânica |  |  |  |  |
| Produção/EMS |  |  |  |  |
| Qualidade |  |  |  |  |
| Gerência técnica |  |  |  |  |

Declaração recomendada:

> Confirmamos que o pacote de fabricação e montagem correspondente ao PN/revisão informados foi revisado contra as regras de biblioteca, esquemático, PCB, DFM, DFA, DFT, documentação técnica e critérios de aceitação definidos para este projeto. Qualquer alteração posterior deve gerar nova revisão e novo pacote de liberação.

---

## 17. Observações finais

Este checklist deve ser tratado como documento vivo. Para cada projeto, as regras devem ser adaptadas conforme:

- tecnologia do PCB;
- classe IPC;
- ambiente de operação;
- tensão/corrente;
- frequência;
- certificações;
- fabricante de PCB;
- montadora;
- volume de produção;
- criticidade de segurança;
- criticidade de disponibilidade.

O ponto mais importante é manter rastreabilidade entre requisito, datasheet, biblioteca, esquemático, constraints, layout, documentação, pacote de saída e aprovação formal.
