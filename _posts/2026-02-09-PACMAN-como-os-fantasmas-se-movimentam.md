---
layout: post
title: "PACMAN: Como funciona o movimento dos fantasmas?"
description: "Explicação básica de como os fantasmas do jogo Pac-Man se movimentam."
date: 2026-02-09 00:00:00 -0300
tags: [games, dev]
---

### Introdução

Pac-Man é um dos maiores clássicos dos jogos arcade. Desde o seu lançamento, inúmeras versões foram criadas, milhões de pessoas jogaram e, principalmente, milhões se apaixonaram pelo jogo.

Quando estamos jogando, raramente paramos para pensar em como certas coisas realmente funcionam. Não é comum iniciar uma partida e ficar se perguntando sobre a lógica por trás de cada mecânica, e aqui falo de aspectos técnicos, não de balanceamento ou de M.E.T.A. (Most Effective Tactics Available).

No Pac-Man, é fácil perceber que cada fantasma se comporta de maneira diferente. Um é mais agressivo, perseguindo o jogador sem hesitar; outros parecem mais estratégicos; e há ainda aquele que parece agir de forma imprevisível, quase medroso.

O mais interessante é que o Pac-Man original não utiliza uma Inteligência Artificial complexa ou sofisticada para controlar esses comportamentos. Na verdade, o jogo se apoia em cálculos e regras relativamente simples para criar toda essa sensação de personalidade e estratégia.

Então, bora entender como funciona o comportamento de cada um dos fantasmas?

Um pequeno parêntese: não escrevo isso como um especialista, mas como parte do meu processo de aprendizado. Escrever e explicar esses conceitos é a melhor forma que encontrei para consolidar o que venho estudando.

### A Lógica do Grid e dos Estados

Antes de tudo, precisamos entender que toda a lógica do jogo acontece em um **grid** (uma grade, ou matriz), onde o Pac-Man e os fantasmas são representados por posições `(x,y)`.

Os fantasmas baseiam-se em estados. Os mais recorrentes são: **SCATTER** (Dispersão); **CHASE** (Perseguição); e **FRIGHTENED** (Assustado).

A movimentação é totalmente focada no **TARGET TILE**, que é a posição do alvo no grid. Uma observação importante: o alvo não necessariamente é o Pac-Man; pode ser apenas uma posição vazia, como veremos adiante.

### Como eles escolhem o caminho?

Ao chegar em uma encruzilhada, o fantasma precisa decidir uma direção. Ele sempre escolherá a que reduz a distância até o seu alvo. Como eles se movem em 4 direções (cima, baixo, esquerda e direita), o jogo calcula a distância em linha reta (Euclidiana) de cada posição até o alvo e escolhe a menor.

A fórmula usada é: `dist = (x1 - x2)^2 + (y1 - y2)^2`

Onde `(x1, y1)` é a posição que o fantasma ocuparia e `(x2, y2)` é a posição do alvo.

**Nota**: Quando eles estão no estado **FRIGHTENED**, essa lógica morre. Eles passam a escolher direções aleatórias em cada cruzamento.

### O alvo de cada fantasma (SCATTER)

Durante o estado **SCATTER**, cada fantasma se movimenta rumo a um canto específico do grid. Cada um tem sua posição pré-estabelecida, fazendo com que eles circulem áreas isoladas do mapa.

### O alvo de cada fantasma (CHASE)

Cada fantasma tem uma lógica diferente para calcular seu **TARGET TILE** durante o estado **CHASE**, e é isso que muda o comportamento deles:

- **Blinky (Vermelho)**: É o mais simples e agressivo. O seu alvo é, o tempo todo, a posição atual do Pac-Man. Por isso, ele parece estar sempre "na sua cola".

- **Pinky (Rosa)**: Ela tenta antecipar o seu movimento. O alvo da Pinky é definido como **4 casas à frente** da posição atual do Pac-Man (baseado na direção que ele está olhando). Isso cria uma sensação de que ela está tentando te cercar ou cortar seu caminho.

- **Inky (Ciano)**: É o mais complexo, pois ele depende de dois fatores: a posição do Pac-Man e a posição do Blinky. Primeiro, o jogo seleciona uma posição **2 casas à frente** do Pac-Man. Depois, ele traça um vetor que começa no Blinky e vai até essa posição, dobrando o comprimento desse vetor para frente. Isso faz com que ele tente "encurralar" o jogador junto com o fantasma vermelho.

- **Clyde (Laranja)**: Ele é o "medroso". A lógica dele muda conforme a distância. Se ele estiver a mais de 8 casas de distância de você, o alvo dele é a posição atual do Pac-Man (igual ao Blinky). Porém, assim que ele se aproxima e fica a menos de 8 casas, o alvo dele muda repentinamente para o seu canto de SCATTER. Isso faz com que ele pareça desistir do ataque bem quando está prestes a te pegar.

### Conclusão

Viu só? A lógica de movimentação, no fim das contas, é bem simples. O que traz a complexidade ao jogo não é uma tecnologia de ponta, mas sim como essas pequenas regras individuais interagem entre si para criar um desafio constante.

Caso queira ver como tudo isso se traduz em código, fique à vontade para acessar o meu repositório. Lá, eu desenvolvi o meu próprio [Pac-Man do zero usando Python](https://github.com/Smeltier/pac-man) com a biblioteca PyGame. Todos os estados e as regras de movimento que discutimos aqui podem ser visualizados na prática por lá.

E se estiver interessado em apenas jogar, você também pode baixar uma versão alpha básica para se divertir e testar se consegue prever o movimento deles!

