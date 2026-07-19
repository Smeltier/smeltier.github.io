---
layout: projects
title: AICOMMIT
description: Automatizando minhas mensagens de commit com IA
date: 2025-12-15
tags: [cli, dev, tools]
github: https://github.com/Smeltier/aicommit
---

#### Introdução

Se tem uma coisa que todo programador já enfrentou é aquele momento de travamento na hora de escrever a mensagem de commit. Você acabou de resolver um bug complicado, fez o `git add .`, e aí para, olha pro terminal, e escreve algo como `fix: ajustes`, sem dizer nada de útil sobre o que realmente mudou.

Foi tentando resolver esse problema (pra mim mesmo, no dia a dia) que criei o `aicommit`. A ideia é simples: pegar o diff das mudanças que estão staged no Git, mandar pra um modelo de linguagem, e receber de volta uma mensagem de commit já formatada seguindo a especificação do Conventional Commits.

Hoje o pacote está publicado no npm como `@smeltier/aicommit`, e qualquer um pode instalar com `npm install -g @smeltier/aicommit`.

Como funciona na prática
O fluxo de uso é bem direto:

```
git add .
aicommit
```

Por trás disso, o programa faz três coisas: primeiro, roda um `git diff --staged` pra capturar exatamente o que vai entrar no commit. Depois, monta um prompt com esse diff e manda pra um provedor de IA. Por fim, mostra a mensagem sugerida no terminal e pergunta se você confirma antes de rodar o `git commit` de verdade.

Isso significa que você nunca perde o controle: a IA sugere, mas quem decide é você.

#### Múltiplos provedores

Uma coisa que fez questão de deixar flexível foi não prender o usuário a um único provedor de IA. O `aicommit` suporta três:

- **Anthropic** (usa o modelo `claude-haiku-4-5` por padrão)
- **OpenAI** (usa o `gpt-4o-mini` por padrão)
- **Ollama** (usa o `llama3` por padrão, e roda localmente, sem precisar de API key)

A escolha é feita por variável de ambiente, então dá pra configurar uma vez no `.zshrc` (ou `.bashrc`) e esquecer:

```
export AICOMMIT_PROVIDER=anthropic
export AICOMMIT_API_KEY=your-api-key
export AICOMMIT_LANG=en
```

Também dá pra trocar o modelo padrão de qualquer provedor com `AICOMMIT_MODEL`, caso você prefira, por exemplo, um modelo mais robusto como o `claude-opus-4-6` no lugar do `haiku`.

#### A escolha do padrão Conventional Commits

Não quis que a IA simplesmente "resumisse" o diff. O prompt que uso é bem específico: exige o formato `<tipo>(<escopo opcional>): <descrição curta>`, restringe os tipos aceitos (`feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`), limita o tamanho a 72 caracteres e proíbe emojis ou ponto final.

Isso garante consistência no histórico do repositório, independente de qual provedor de IA está gerando a mensagem, o que é essencial se o projeto for usado em equipe ou em múltiplos repositórios com convenções próprias.

#### Suporte a idiomas

Como escrevo e trabalho em português boa parte do tempo, fez sentido deixar o idioma da mensagem configurável via `AICOMMIT_LANG`. Isso é injetado direto no prompt, então a mensagem final sai no idioma escolhido, mas mantendo a estrutura do Conventional Commits, que é universal.

#### Conclusão

No fim das contas, o `aicommit` resolve um problema pequeno, mas recorrente: a fricção de escrever boas mensagens de commit no dia a dia. Não é sobre terceirizar a decisão pra IA, e sim sobre reduzir o atrito. A sugestão vem pronta, formatada, e você só confirma ou ajusta.

O código está disponível no meu GitHub, e o pacote publicado no npm como `@smeltier/aicommit`, sob a licença MIT.
