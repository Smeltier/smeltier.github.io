---
layout: projects
title: Xadrez em Java
description: Implementação de um jogo de xadrez em linha de comando, desenvolvido em Java com foco em modelagem orientada a objetos.
date: 2025-12-15
tags: [Java, dev]
github: https://github.com/Smeltier/xadrez
---

## Visão Geral

Este projeto é uma implementação completa de um **jogo de xadrez em linha de comando (CLI)**, desenvolvido inteiramente em Java. O foco principal está na **modelagem orientada a objetos**, na validação rigorosa das regras do jogo e na separação clara de responsabilidades entre as camadas do sistema.

O motor do jogo implementa as regras oficiais da FIDE, incluindo verificação de movimentos legais, detecção de **xeque, xeque-mate e afogamento**, além do suporte a movimentos especiais como **roque, en passant e promoção de peões**.

A arquitetura segue uma organização inspirada em **MVC**, permitindo evolução e manutenção do código de forma organizada e previsível.

<div class="center-image-wrapper">
  <img src="/assets/images/xadrez-cli.png" alt="Foto do jogo rodando no terminal" class="center-image" />
</div>

---

## Objetivos do Projeto

O desenvolvimento deste projeto teve como principais objetivos:

- Praticar modelagem orientada a objetos em um domínio com regras complexas
- Aplicar validação consistente de estados e transições do jogo
- Explorar separação entre lógica de negócio e interface (CLI)
- Consolidar o uso de Java moderno (JDK 17+)
- Desenvolver um motor de xadrez funcional sem dependência de interfaces gráficas

---

## Requisitos

Para executar o projeto, é necessário:

- **Java Development Kit (JDK)** versão 17 ou superior
- **Terminal de comando** (Bash, PowerShell ou CMD)

---

## Executando o Projeto

O repositório inclui scripts de automação que simplificam a compilação e execução do jogo.

### Windows

Na raiz do projeto, execute: `cmd play.bat`

### Linux/macOS

Conceda permissão de execução (apenas na primeira vez):

```sh
chmod +x play.sh
```

Em seguida, execute:

```sh
./play.sh
```

## Configurações da Partida

Ao iniciar o jogo, o sistema solicitará:

1. **Nome dos jogadores**
2. **Definição das peças brancas**, escolhendo qual jogador inicia a partida
    - Digite `1` para o Jogador 1
    - Digite `2` para o Jogador 2

## Interface e Comandos

O tabuleiro é renderizado diretamente no terminal utilizando **caracteres Unicode**.
As coordenadas seguem o padrão internacional do xadrez:

- **Colunas:** letras de `a` a `h`
- **Linhas:** números de `1` a `8`

### Movimentação das Peças

Os comandos de jogada seguem o formato:

```css
[origem] [destino]
```

#### Exemplo: `e2 e4`

O sistema valida automaticamente:

- Existência da peça na casa de origem
- Cor da peça em relação ao turno atual
- Geometria válida do movimento
- Ausência de obstruções no trajeto (exceto para o Cavalo)
- Segurança do Rei (movimentos que resultem em auto-xeque são bloqueados)

### Movimentos Especiais

#### Roque (Castling)

Permite o movimento simultâneo do Rei e da Torre.

- **Execução:** O jogador deve comandar o movimento do **Rei** por duas casas em direção à Torre escolhida.
- **Comando (Brancas):** `e1 g1` (Roque Menor) ou `e1 c1` (Roque Maior).
- **Comando (Pretas):** `e8 g8` (Roque Menor) ou `e8 c8` (Roque Maior).
- _Nota: A Torre será movida automaticamente pelo sistema se a manobra for válida e o caminho estiver seguro._

#### En Passant

Captura especial de peões.

- **Condição:** Ocorre quando um peão adversário avança duas casas a partir da posição inicial, parando ao lado do seu peão.
- **Execução:** O jogador deve mover seu peão para a casa diagonal vazia imediatamente atrás do peão adversário.
- **Comando:** Inserir as coordenadas de origem e da casa de destino (vazia).

#### Promoção (Promotion)

Transformação obrigatória de um peão que atinge a última fileira do tabuleiro.

- **Condição:** Um peão (Branco na linha 8 ou Preto na linha 1) conclui seu movimento.
- **Execução:** O sistema interromperá o fluxo automaticamente e apresentará um menu de seleção.
- **Opções:** O jogador deve digitar o número correspondente à peça desejada:
- `1` - Rainha (Queen)
- `2` - Torre (Rook)
- `3` - Cavalo (Knight)
- `4` - Bispo (Bishop)

- **Resultado:** O peão é imediatamente substituído pela peça escolhida na mesma casa.

## Estados do Jogo

O sistema fornece feedback em tempo real sobre o estado da partida:

- **Xeque:** Indica que o Rei está sob ataque imediato. O jogador é obrigado a realizar um movimento defensivo.
- **Erro de movimento:** Informa tentativas de jogadas ilegais (geometria incorreta, obstrução ou exposição do Rei ao perigo).
- **Xeque-mate:** Ocorre quando o Rei está em xeque e não existem movimentos legais disponíveis. O sistema encerra a execução e declara o vencedor.
- **Empate por afogamento (Stalemate):** Ocorre quando o jogador que tem a vez de jogar não possui movimentos legais, mas seu Rei não está em xeque. O sistema encerra a partida declarando empate.

## Problemas Comuns e Soluções

### Problema de Fonte (Retângulos/Quadrados)

Caso as peças apareçam como retângulos vazios (`□`), o terminal está usando uma fonte que não suporta símbolos de xadrez Unicode.

- **Solução:** Nas propriedades do terminal (Prompt de Comando ou PowerShell), altere a fonte para **MS Gothic**, **NSimSun** ou use um terminal moderno como o **Windows Terminal**.

### Problema de Codificação (Interrogações)

Caso as peças apareçam como interrogações (`?`), o terminal não está interpretando UTF-8 corretamente.

- **Solução:** Antes de iniciar o jogo, execute o seguinte comando no terminal:

```powershell
chcp 65001
```

### Compilação Manual (Método Alternativo)

Caso opte por não utilizar os scripts de automação, utilize os comandos abaixo na raiz do projeto para compilar e executar manualmente:

**No Linux / macOS:**

```bash
mkdir -p bin
javac -d bin -encoding UTF-8 $(find src/main/java -name "*.java")
java -Dfile.encoding=UTF-8 -cp bin main.java.com.work.chess.application.Main
```

**No Windows (PowerShell):**

```powershell
if (!(Test-Path bin)) { New-Item -ItemType Directory -Force -Path bin }
Get-ChildItem -Recurse -Filter *.java | ForEach-Object { javac -d bin -encoding UTF-8 $_.FullName }
java -Dfile.encoding=UTF-8 -cp bin main.java.com.work.chess.application.Main
```

