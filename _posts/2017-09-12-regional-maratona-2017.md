---
title: "Etapa Regional da Maratona 2017"
layout: post
use_math: true
---

No último final de semana mais de 800 times, representando 232 escolas, participaram da primeira fase da [Maratona de Programação][maratona]. O resultado, assim como as questões da prova e os arquivos de entrada/saída, podem ser conferidos [aqui][resultado-maratona].

Abaixo se encontram algumas dicas para resolver os problemas da prova.

## A

Podemos usar uma [segment tree com lazy propagation][tutorial-segtree] para simular de forma eficiente cada acorde. Armazenamos em cada nó a frequência que cada nota no intervalo representado pelo nó. Podemos então, a cada acorde tocado, computar qual a nota mais frequente e atualizar o entervalo em seguida. Um problema similar apareceu na regional de 2011: [Homem, Elefante e Rato][uri-1477-homem].

## B

Uma maneira bastante popular de calcular somas de intervalos em vetores estáticos é usando somas de prefixos. Para simplificar, assumimos que o vetor $A$ é indexado a partir de 1. Definimos então um vetor $P$, tal que $P_0 = 0$  e $P_i = \sum_{j=1}^{i}A_j$. Desse modo podemos obter a soma do intervalo $[i, j]$ como $P_j - P_{i-1}$. Usando essa representação e o [Princípio da casa dos pombos][casa-pombos] podemos provar que sempre existe uma subsequência contígua cuja soma dos elementos é divisível por $X$.

Se calcularmos os valores $P_i$ módulo $X$ existem apenas $X$ possíveis valores. Logo, a partir do elemento $P_X$, garantidamente teremos valores repetidos. Isso significa que sempre seremos capazes de encontrar dois índices $L$ e $R$ distintos tais que $P_L = P_R$. Sendo assim sempre poderemos encontrar um intervalo $[L+1, R]$ cuja soma dos elementos é divisível por $X$, visto que $P_R - P_{L+1-1 = L} = 0$.

Basta, então, gerar os elementos da sequência e manter a soma do prefixo (módulo $X$) visto até o momento, armazenando a posição da primeira ocorrência de cada valor. Ao encontrarmos um valor que já foi visto antes, verificamos se a distância entre as posições é maior ou igual a $Y$, imprimindo tais índices em caso positivo. Com essa estratégia garantimos também que vamos obter o menor valor para os inteiros $I$ e $F$ que representam os índices do primeiro e do último elementos da subsequência contígua escolhida.

## C

## D

## E

## F

## G

## H

## I

## J

## K

## L

## M


E alguns exemplos de implementação:

{% gist paulocezar/8d317179d662fbb9407bd84ef8285520 %}

[maratona]: http://maratona.ime.usp.br/
[resultado-maratona]: http://maratona.ime.usp.br/vagas17.html
[tutorial-segtree]: https://www.hackerearth.com/practice/notes/segment-tree-and-lazy-propagation/
[uri-1477-homem]: https://www.urionlinejudge.com.br/judge/pt/problems/view/1477
[casa-pombos]: https://pt.wikipedia.org/wiki/Princ%C3%ADpio_da_casa_dos_pombos
