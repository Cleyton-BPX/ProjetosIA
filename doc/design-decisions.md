# Design Decisions

Este arquivo registra decisões importantes de UX/UI do projeto.

Use este documento para evitar retrabalho, manter consistência entre telas e impedir que decisões já aprovadas sejam reabertas sem necessidade.

---

## Como usar este arquivo

Sempre que uma decisão de UX/UI for tomada, registre:

- data;
- contexto;
- decisão;
- motivo;
- impacto nas telas;
- status;
- responsável, se necessário;
- relação com fluxos, telas ou componentes.

O Codex deve consultar este arquivo antes de propor mudanças em fluxos, telas, componentes ou padrões visuais.

---

## Status possíveis

- `Proposta`: decisão sugerida, ainda não validada.
- `Em validação`: decisão em teste ou aguardando alinhamento.
- `Aprovada`: decisão vigente e deve ser respeitada.
- `Rejeitada`: decisão descartada e não deve ser sugerida novamente sem novo contexto.
- `Substituída`: decisão antiga mantida apenas como histórico.

---

## Regras de governança

- Decisões com status `Aprovada` não devem ser contraditas sem sinalização explícita.
- Se uma nova proposta entrar em conflito com decisão aprovada, registrar o conflito antes de sugerir alteração.
- Decisões antigas não devem ser apagadas; devem ser marcadas como `Substituída`, quando necessário.
- Toda decisão que impactar mais de uma tela deve ser registrada.
- Toda decisão que orientar handoff deve ser registrada.
- Preferir decisões objetivas e acionáveis, evitando justificativas vagas.

---

# Índice de decisões

| ID | Decisão | Status | Última atualização |
|---|---|---|---|
| DD-001 | Estrutura do Figma como pipeline visual | Aprovada |  |
| DD-002 | Páginas principais do Figma | Aprovada |  |
| DD-003 | Handoff sem página separada de pré-handoff | Aprovada |  |
| DD-004 | Apenas Ready for Dev é fonte da verdade para desenvolvimento | Aprovada |  |
| DD-005 | Uso de três papéis no Codex | Aprovada |  |
| DD-006 | Registro de decisões de design | Aprovada |  |
| DD-007 | Padrão de nome para frames | Aprovada |  |
| DD-008 | Card obrigatório por fluxo | Aprovada |  |
| DD-009 | Estados obrigatórios por tela | Proposta |  |
| DD-010 | Tratamento de erros em formulários | Proposta |  |
| DD-011 | Componentes reutilizáveis como padrão | Proposta |  |
| DD-012 | Clareza da ação principal | Proposta |  |

---

# Decisões

## DD-001 — Estrutura do Figma como pipeline visual

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Organização do Figma, handoff, governança de UX

### Contexto

O arquivo Figma estava ficando complexo, com muitas páginas e dificuldade para identificar o que estava em exploração, revisão ou pronto para desenvolvimento.

### Decisão

Organizar o Figma como uma pipeline visual de maturidade do trabalho, separando exploração, revisão, handoff e histórico.

### Motivo

Reduzir confusão, facilitar navegação do time, evitar implementação de telas erradas e melhorar a preparação para handoff.

### Impacto nas telas

- Fluxos em construção devem ficar em `Product Flows / Working`.
- Fluxos em validação devem ficar em `Product Flows / Review`.
- Fluxos candidatos ou prontos para desenvolvimento devem ficar em `Product Flows / Handoff`.
- Versões antigas devem ir para `Archive / Deprecated`.

### Riscos ou observações

A estrutura só funciona se os status forem mantidos atualizados e se o time respeitar a fonte da verdade.

---

## DD-002 — Páginas principais do Figma

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Organização do Figma

### Contexto

A estrutura anterior tinha muitas páginas separadas por tipo de conteúdo, o que aumentava o esforço de navegação e manutenção.

### Decisão

Usar a seguinte estrutura principal:

```txt
00 Cover / Index
01 Project Docs / Governance
02 Design System / Library
03 Product Flows / Working
04 Product Flows / Review
05 Product Flows / Handoff
90 Experiments / Playground
99 Archive / Deprecated
```

### Motivo

Reduzir número de páginas, manter organização por função e separar claramente documentação, biblioteca, fluxo de produto, experimentos e histórico.

### Impacto nas telas

- Documentação e governança ficam agrupadas.
- Design system, assets, patterns e templates ficam agrupados.
- Fluxos são separados por maturidade.
- Experimentos e arquivo ficam fora da fonte da verdade.

### Riscos ou observações

Ao reduzir páginas, é obrigatório usar seções internas bem nomeadas para evitar que as páginas unificadas virem depósitos.

---

## DD-003 — Handoff sem página separada de pré-handoff

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Handoff, organização do Figma

### Contexto

A estrutura com uma página separada para pré-handoff adicionaria mais uma página ao Figma, aumentando a complexidade de navegação.

### Decisão

Não criar uma página separada de pré-handoff. Usar a página `05 Product Flows / Handoff` com duas seções internas:

```txt
05.1 Handoff Candidates
05.2 Ready for Dev
```

### Motivo

Manter o processo profissional sem aumentar o número de páginas.

### Impacto nas telas

- Fluxos quase prontos entram em `Handoff Candidates`.
- Fluxos finalizados entram em `Ready for Dev`.
- O pré-handoff existe como etapa interna, não como página própria.

### Riscos ou observações

A seção `Handoff Candidates` não deve ser confundida com entrega final para desenvolvimento.

---

## DD-004 — Apenas Ready for Dev é fonte da verdade para desenvolvimento

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Handoff, desenvolvimento, governança

### Contexto

Quando há várias versões de telas no Figma, devs, PMs e stakeholders podem se confundir sobre qual versão implementar.

### Decisão

Apenas fluxos dentro de `05 Product Flows / Handoff > Ready for Dev` devem ser tratados como fonte da verdade para desenvolvimento.

### Motivo

Evitar implementação de versões erradas ou incompletas.

### Impacto nas telas

- Telas em `Working`, `Review`, `Handoff Candidates`, `Playground` ou `Archive` não são fonte da verdade para implementação.
- Toda tela pronta para dev precisa estar em `Ready for Dev`.
- Comentários críticos devem estar resolvidos antes de mover para `Ready for Dev`.

### Riscos ou observações

Se um fluxo em `Ready for Dev` sofrer alteração relevante, seu status deve voltar para `Handoff Candidate` ou `Review`.

---

## DD-005 — Uso de três papéis no Codex

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Codex, AGENTS.md, processo de UX

### Contexto

Havia a possibilidade de criar muitos agentes, mas isso poderia gerar complexidade antes de maturidade real no processo.

### Decisão

Usar apenas três papéis principais no Codex:

1. Orquestrador UX
2. Revisor Crítico
3. Especificador de Telas

### Motivo

Manter o uso do Codex simples, focado e fácil de explicar para o time.

### Impacto nas telas

- O Orquestrador UX organiza demandas e fluxos.
- O Revisor Crítico avalia problemas, inconsistências e riscos.
- O Especificador de Telas transforma fluxos em especificações para Figma.

### Riscos ou observações

Novos papéis só devem ser criados se uma tarefa repetitiva justificar essa separação.

---

## DD-006 — Registro de decisões de design

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Governança, documentação, Codex

### Contexto

Decisões importantes podem se perder em conversas, comentários do Figma ou reuniões, gerando retrabalho e inconsistência.

### Decisão

Manter um arquivo de decisões em:

```txt
docs/ux/design-decisions.md
```

E refletir as principais decisões no Figma em:

```txt
01 Project Docs / Governance > Design Decisions
```

### Motivo

Criar histórico verificável das decisões e impedir que discussões já resolvidas sejam reabertas sem necessidade.

### Impacto nas telas

- Decisões aprovadas devem orientar revisão de fluxos e telas.
- O Codex deve consultar esse arquivo antes de sugerir mudanças relevantes.
- Conflitos com decisões aprovadas devem ser sinalizados.

### Riscos ou observações

O arquivo precisa ser atualizado continuamente para não perder confiabilidade.

---

## DD-007 — Padrão de nome para frames

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Organização do Figma, handoff

### Contexto

Nomes genéricos como `Final`, `Final 2`, `Tela nova` e `Frame 203` dificultam navegação e handoff.

### Decisão

Usar o padrão:

```txt
[Fluxo] / [Etapa] / [Tela] / [Estado]
```

Exemplos:

```txt
Cadastro Lead / 01 / Dados básicos / Default
Cadastro Lead / 01 / Dados básicos / Validation error
Cadastro Lead / 02 / Revisão / Default
Cadastro Lead / 03 / Sucesso / Success
```

### Motivo

Facilitar busca, leitura, revisão e comunicação com devs e PMs.

### Impacto nas telas

- Todos os frames finais ou em revisão devem seguir esse padrão.
- Frames exploratórios podem ser menos formais, mas devem ser minimamente identificáveis.
- Frames em `Ready for Dev` obrigatoriamente seguem o padrão.

### Riscos ou observações

Nomes longos demais devem ser evitados, mas clareza é prioridade.

---

## DD-008 — Card obrigatório por fluxo

**Data:**  
**Status:** Aprovada  
**Responsável:**  
**Relacionado a:** Organização de fluxo, Figma, handoff

### Contexto

Fluxos no Figma podem ficar difíceis de entender sem contexto, status, responsável ou escopo.

### Decisão

Todo fluxo deve ter um card no topo com:

```txt
Fluxo:
Status:
Responsável UX:
Responsável Produto:
Responsável Dev:
Última atualização:

Objetivo:
Escopo:
Fora do escopo:

Dúvidas abertas:
Decisões relacionadas:
Link do ticket/backlog:
```

### Motivo

Permitir que qualquer pessoa entenda rapidamente o contexto e a maturidade do fluxo.

### Impacto nas telas

- Todo bloco de fluxo deve começar com um card de contexto.
- Fluxos em `Review` e `Handoff` devem ter o card completo.
- Fluxos em `Working` podem ter card parcial, mas precisam de objetivo e status.

### Riscos ou observações

O card precisa ser atualizado quando o fluxo muda de status.

---

## DD-009 — Estados obrigatórios por tela

**Data:**  
**Status:** Proposta  
**Responsável:**  
**Relacionado a:** Handoff, qualidade de UX, especificação de telas

### Contexto

Telas costumam ser desenhadas apenas no estado ideal, o que gera retrabalho no handoff e problemas durante implementação.

### Decisão

Toda tela relevante deve considerar estados alternativos antes de ser considerada pronta.

### Motivo

Reduzir retrabalho, melhorar qualidade do protótipo e preparar melhor a implementação futura.

### Impacto nas telas

Sempre que aplicável, prever:

- Default;
- Loading;
- Empty;
- Error;
- Success;
- Disabled;
- Validation;
- Confirmation;
- Cancellation;
- Permission/blocked;
- Edge cases.

### Riscos ou observações

Nem toda tela precisa de todos os estados, mas a ausência deles deve ser consciente e registrada.

---

## DD-010 — Tratamento de erros em formulários

**Data:**  
**Status:** Proposta  
**Responsável:**  
**Relacionado a:** Formulários, validação, acessibilidade

### Contexto

Erros em formulários precisam ser compreensíveis e fáceis de corrigir.

### Decisão

Mostrar erros próximos ao campo afetado e, quando houver múltiplos erros ou erro geral, exibir também um resumo ou alerta visível.

### Motivo

Facilitar correção rápida, reduzir frustração e melhorar acessibilidade.

### Impacto nas telas

- Campos com erro devem ter mensagem clara.
- Mensagens devem explicar o problema e, quando possível, como resolver.
- Não depender apenas de cor para indicar erro.
- Estados de erro precisam estar previstos no Figma.
- Em erro de envio, preservar dados preenchidos sempre que possível.

### Riscos ou observações

Evitar mensagens técnicas ou genéricas demais.

---

## DD-011 — Componentes reutilizáveis como padrão

**Data:**  
**Status:** Proposta  
**Responsável:**  
**Relacionado a:** Design System, componentes, consistência visual

### Contexto

Componentes duplicados ou variações sem necessidade aumentam inconsistência visual e dificultam manutenção.

### Decisão

Priorizar componentes reutilizáveis para elementos recorrentes.

### Motivo

Aumentar consistência, acelerar criação de telas e facilitar handoff futuro.

### Impacto nas telas

Componentes recorrentes devem ser tratados como padrão, especialmente:

- botões;
- inputs;
- selects;
- cards;
- modais;
- alerts;
- tabs;
- menus;
- navegação;
- estados de feedback.

### Riscos ou observações

Evitar criar variações visuais sem necessidade real. Quando uma variação for necessária, documentar o motivo.

---

## DD-012 — Clareza da ação principal

**Data:**  
**Status:** Proposta  
**Responsável:**  
**Relacionado a:** UX, telas, conversão, clareza de fluxo

### Contexto

Telas com múltiplas ações concorrentes podem gerar dúvida e reduzir conclusão de tarefas.

### Decisão

Cada tela deve ter uma ação principal evidente, alinhada ao objetivo daquela etapa do fluxo.

### Motivo

Reduzir ambiguidade e aumentar a chance de o usuário concluir a tarefa.

### Impacto nas telas

- Evitar múltiplas CTAs concorrendo com o mesmo peso visual.
- A ação principal deve estar visualmente destacada.
- Ações secundárias devem ter menor peso visual.
- Telas informativas devem deixar claro o próximo passo.
- Se uma tela tiver mais de uma ação principal, o objetivo da tela deve ser revisado.

### Riscos ou observações

Em telas de decisão, pode haver mais de uma ação relevante, mas a hierarquia entre elas precisa ser clara.

---

# Template para novas decisões

## DD-000 — Nome da decisão

**Data:**  
**Status:** Proposta / Em validação / Aprovada / Rejeitada / Substituída  
**Responsável:**  
**Relacionado a:** Fluxo, tela, componente ou documentação relacionada

### Contexto

Explique o problema, cenário ou necessidade que levou à decisão.

### Decisão

Descreva a decisão de forma objetiva.

### Motivo

Explique por que essa decisão foi tomada.

### Impacto nas telas

Liste o que muda ou deve ser observado nas telas.

### Riscos ou observações

Liste riscos, exceções ou pontos que podem exigir revisão futura.

---

# Checklist para registrar uma decisão

Antes de registrar uma decisão, verifique:

- [ ] A decisão impacta mais de uma tela?
- [ ] A decisão afeta handoff?
- [ ] A decisão evita retrabalho futuro?
- [ ] A decisão cria ou altera padrão?
- [ ] A decisão precisa ser conhecida por PM, dev ou outro designer?
- [ ] Existe decisão anterior que entra em conflito?
- [ ] O status está correto?
- [ ] O motivo está claro?
- [ ] O impacto nas telas está explícito?
