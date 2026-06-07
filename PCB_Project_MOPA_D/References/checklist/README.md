# Pacote de Checklist Profissional para Revisão de Esquemático e PCB

Este pacote contém:

1. `CHECKLIST_VERIFICACAO_ESQUEMATICO_PCB.md`  
   Documento principal com checklist rígido desde biblioteca até liberação final.

2. `TEMPLATES_NOTAS_FABRICACAO_MONTAGEM.md`  
   Modelos de notas para inserir no esquemático, desenhos de fabricação, camadas mecânicas e montagem.

3. `MANIFESTO_RELEASE_FABRICACAO.md`  
   Modelo de manifesto de release com lista de arquivos, hash/checksum, gates e aprovações.

4. `MATRIZ_RASTREABILIDADE_DFM_DRC.md`  
   Matriz para rastrear requisitos de fabricação, DRC, ERC, impedância, segurança e evidências.

Uso recomendado:

- Copie os arquivos para a pasta `docs/pcb_review/` do projeto.
- Adapte os valores de capacidade do fabricante antes de iniciar o layout.
- Não libere fabricação com itens `BLOCKER` em aberto.
- Gere um novo manifesto a cada revisão enviada para fabricação.
