# Conductor para OpenCode

**Measure twice, code once.**

Conductor é uma extensão para OpenCode que permite **Desenvolvimento Orientado por Contexto**. Ele transforma o OpenCode em um gerente de projeto proativo que segue um protocolo rigoroso para especificar, planejar e implementar recursos de software.

Em vez de apenas escrever código, o Conductor garante um ciclo de vida consistente e de alta qualidade para cada tarefa: **Contexto -> Especificação & Plano -> Implementação**.

A filosofia por trás do Conductor é simples: controle seu código. Ao tratar o contexto como um artefato gerenciado junto com seu código, você transforma seu repositório em uma única fonte de verdade que impulsiona todas as interações do agente com conhecimento profundo e persistente do projeto.

## Funcionalidades

- **Planeje antes de construir**: Crie especificações e planos que guiem o agente para códigos novos e existentes.
- **Mantenha contexto**: Garanta que a IA siga guias de estilo, escolhas de pilha técnica e metas do produto.
- **Itere com segurança**: Revise planos antes da escrita de código, mantendo você firmemente no controle.
- **Trabalhe em equipe**: Defina contexto no nível do produto para suas preferências de produto, pilha técnica e fluxo de trabalho que se tornam uma base compartilhada para sua equipe.
- **Construa em projetos existentes**: Inicialização inteligente para projetos Greenfield (novos) e Brownfield (existentes).
- **Reversão inteligente**: Um comando de reversão com reconhecimento de git que entende unidades lógicas de trabalho (tracks, fases, tarefas) em vez de apenas hashes de commit.

## Instalação

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/conductor-opencode.git
   cd conductor-opencode
   ```

2. Copie os comandos para o diretório de comandos do OpenCode:
   - Para instalação global: copie os arquivos `.md` de `opencode-commands/` para `~/.config/opencode/command/`
   - Para projeto específico: copie para `.opencode/command/` no diretório do projeto

3. Reinicie o OpenCode ou recarregue os comandos.

## Uso

O Conductor é projetado para gerenciar todo o ciclo de vida de suas tarefas de desenvolvimento.

### 1. Configure o Projeto (Execute Uma Vez)

Quando você executa `/conductor:setup`, o Conductor ajuda a definir os componentes principais do contexto do projeto. Este contexto é usado para construir novos componentes ou recursos por você ou qualquer um da sua equipe.

- **Produto**: Defina contexto do projeto (ex.: usuários, metas do produto, recursos de alto nível).
- **Diretrizes do produto**: Defina padrões (ex.: estilo de prosa, mensagens de marca, identidade visual).
- **Pilha técnica**: Configure preferências técnicas (ex.: linguagem, banco de dados, frameworks).
- **Fluxo de trabalho**: Defina preferências da equipe (ex.: TDD, estratégia de commit).

**Artefatos Gerados:**
- `conductor/product.md`
- `conductor/product-guidelines.md`
- `conductor/tech-stack.md`
- `conductor/workflow.md`
- `conductor/code_styleguides/`
- `conductor/tracks.md`

```bash
/conductor-setup
```

### 2. Inicie uma Nova Track (Recurso ou Bug)

Quando estiver pronto para assumir um novo recurso ou correção de bug, execute `/conductor:newTrack`. Isso inicializa uma **track** — uma unidade de trabalho de alto nível. O Conductor ajuda a gerar dois artefatos críticos:

- **Especificações**: Os requisitos detalhados para o trabalho específico. O que estamos construindo e por quê?
- **Plano**: Uma lista de tarefas acionáveis contendo fases, tarefas e subtarefas.

**Artefatos Gerados:**
- `conductor/tracks/<track_id>/spec.md`
- `conductor/tracks/<track_id>/plan.md`
- `conductor/tracks/<track_id>/metadata.json`

```bash
/conductor-newtrack
# OU com uma descrição
/conductor-newtrack "Adicionar um botão de modo escuro na página de configurações"
```

### 3. Implemente a Track

Uma vez aprovado o plano, execute `/conductor:implement`. Seu agente de codificação trabalha através do arquivo `plan.md`, marcando tarefas conforme avança.

**Artefatos Atualizados:**
- `conductor/tracks.md` (Atualizações de status)
- `conductor/tracks/<track_id>/plan.md` (Atualizações de status)

```bash
/conductor-implement
```

O Conductor irá:
1. Selecionar a próxima tarefa pendente.
2. Seguir o fluxo de trabalho definido (ex.: TDD: Escrever Teste -> Falhar -> Implementar -> Passar).
3. Atualizar o status no plano conforme progride.
4. **Verificar Progresso**: Orientá-lo através de uma etapa de verificação manual no final de cada fase para garantir que tudo funcione conforme esperado.

Durante a implementação, você também pode:
- **Verificar status**: Obtenha uma visão geral de alto nível do progresso do seu projeto.
  ```bash
  /conductor-status
  ```
- **Reverter trabalho**: Desfaça um recurso ou tarefa específica se necessário.
  ```bash
  /conductor-revert
  ```

## Referência de Comandos

| Comando | Descrição | Artefatos |
| --- | --- | --- |
| `/conductor-setup` | Estrutura o projeto e configura o ambiente Conductor. Execute uma vez por projeto. | `conductor/product.md`<br>`conductor/product-guidelines.md`<br>`conductor/tech-stack.md`<br>`conductor/workflow.md`<br>`conductor/tracks.md` |
| `/conductor-newtrack` | Inicia uma nova track de recurso ou bug. Gera `spec.md` e `plan.md`. | `conductor/tracks/<id>/spec.md`<br>`conductor/tracks/<id>/plan.md`<br>`conductor/tracks.md` |
| `/conductor-implement` | Executa as tarefas definidas no plano da track atual. | `conductor/tracks.md`<br>`conductor/tracks/<id>/plan.md` |
| `/conductor-status` | Exibe o progresso atual do arquivo de tracks e tracks ativas. | Lê `conductor/tracks.md` |
| `/conductor-revert` | Reverte uma track, fase ou tarefa analisando o histórico do git. | Reverte histórico do git |

## Origem

Este projeto é uma adaptação do [Conductor para Gemini CLI](https://github.com/gemini-cli-extensions/conductor) para funcionar com OpenCode.

## Licença

Apache License 2.0

---

Criado por Pedro Leon