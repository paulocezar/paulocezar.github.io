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

O primeiro passo é notar que a quantidade de iterações necessária até que os ciclos de vida coincidam é o mínimo múltiplo comum dos ciclos de todas as populações em questão. Como queremos que o resultado respeite o limite superior $L$ não faz sentido que a nova população tenha um ciclo de vida maior que $L$. Assim, basta calcular o mínimo múltiplo comum das populações existentes com todos os valores de 1 a $L$ e imprimir o valor que gerou o melhor resultado.

## D

Dada a fatoração em números primos de um valor $N = p_1^{e_1} \times p_2^{e_2} \times \dots \times p_k^{e_k}$. Um número $D$ é divisor de $N$ se e somente se em sua fatoração não existe um número primo que não está presente nos fatores de $N$ e os expoentes dos fatores de $D$ são todos menores ou iguais ao expoente do fator correspondente de $N$.

Assim, considerando a definição de número despojado, podemos ver as fatorizações dos divisores despojados de $N$ como números da forma $p_1^{d_1} \times p_2^{d_2} \times \dots \times p_k^{d_k}$, onde $d_i \in \\{0, 1\\}$. Com isso basta calcular o número de fatores primos de $N$ e computar o número de combinações equivalentes a divisores despojados. Esse valor, se a quantidade de fatores primos distintos for igual a $K$, é dado por $2^K - (K+1)$. Ou seja, calculamos todas as combinações e desconsideramos aquelas com apenas 0 ou 1 elementos.

## E

Para começar, simplificamos a entrada, transformando cada uma das notas da música na nota básica correspondente.
Cada uma das 12 notas básicas pode ser usada para definir um tom maior.
Cada tom maior é composto por 7 notas, que podem ser encontradas seguindo o padrão descrito no enunciado do problema.
Para verificar se a música está ou não em um tom maior devemos conferir se todas as notas que aparecem na música fazem parte do mesmo.
Isso quer dizer que nem sequer precisamos armazenar todas as notas da música, basta marcar quais notas foram vistas.
Podemos então testar cada uma das notas básicas, em ordem, como base para o tom maior, imprimindo assim que encontramos o primeiro tom maior em que a música se encontra ou _desafinado_ caso a música não esteja em nenhum tom maior.

## F

## G

## H

## I

## J

## K

Como só estamos interessados na parte inteira de $X^N$ onde $X = A + \sqrt{B}$, se conseguirmos nos livrar da raiz quadrada e trabalhar apenas com inteiros, podemos calcular $X^N \bmod 10^5$. Dessa forma seria possível usar apenas tipos de dados básicos para encontrar a resposta. Uma primeira tentativa é usar o [Binómio de Newton][binomio-newton] para tentar se livrar da raiz quadrada. O resultado é $\sum_{K=0}^{N}{\binom{N}{K}A^{N-K}\sqrt{B}^K}$. Infelizmente isso não ajuda muito já que ainda temos $\sqrt{B}^K$ com valores impares de $K$. 

Uma outra restrição no enunciado que certamente não está lá sem motivo é que $-1 < A -  \sqrt{B} < 1$. Será como essa restrição pode nos ajudar? Ao olharmos pra expansão de $(A - \sqrt{B})^N$ obtemos $\sum_{K=0}^{N}{\binom{N}{K}A^{N-K}(-1)^K\sqrt{B}^K}$. Aqui podemos observar algo interessante, ao olhar para a soma $(A + \sqrt{B})^N + (A - \sqrt{B})^N$, se expandirmos as potências dos binómios os termos com $K$ ímpar irão se cancelar, já para valores impares de $K$ temos que $-1^K = -1$. Assim chegamos a $Z = (A + \sqrt{B})^N + (A - \sqrt{B})^N = 2\sum_{K=0}^{\lfloor\frac{N}{2}\rfloor}{\binom{N}{2K}A^{N-2K}B^K}$. $Z$ é um valor inteiro que esperamos ser capazes de calcular sem dificuldade, isso já ajuda um pouco. Outro ponto é que $-1 < A -  \sqrt{B} < 1 \implies -1 < (A - \sqrt{B})^N < 1$, logo a parte inteira de $(A + \sqrt{B})^N$ é igual a $Z$ ou $Z-1$, o que pode ser determinado apenas olhando para a paridade de $N$ e os valores de $A$ e $B$.

A abordagem parece promissora, tirando o fato de que $N \leq 10^9$ não permite que calculemos $Z = (A + \sqrt{B})^N + (A - \sqrt{B})^N$ com complexidade de tempo linear. Para contornar essa dificuldade podemos tentar encontrar uma recorrência linear tal que $F(N) = (A + \sqrt{B})^N + (A - \sqrt{B})^N$ e com isso usar [exponenciação de matrizes][matrix-expo] para calcular $F(N)$  em tempo logarítmico. 

Se calcularmos os primeiros valores de $F(N)$ em função de $A$ e $B$ temos que:

$$F(0) = 2$$

$$F(1) = 2A$$

$$F(2) = 2(A^2 + B)$$

$$F(3) = 2(A^3 + AB)$$

Nesse ponto podemos dar um chute de que nossa recorrência é da forma $F(N) = C \times F(N-1) + D \times F(N-2)$ (ou primeiro chutamos $F(N) = C \times F(N-1) + D$ e partimos pra segunda tentativa ao não chegar a lugar algum).
Aqui conseguimos um sistema de equações onde:

$$F(2) = C \times F(1) + D \times F(0)\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ F(3) = C \times F(2) + D \times F(1)$$

$$2(A^2 + B) =  C \times 2A + D \times 2\ \ \ \ \ \ \ \ \ \ \ 2(A^3 + AB) = C \times 2(A^2 + B) + D \times 2A$$

Com isso encontramos $C$ e $D$ em função de $A$ e $B$, sendo que $C = 2A$ e $D = B - A^2$. Agora basta utilizar exponenciação de matrizes para calcular o resultado de $F(N)$.


## L

## M


E alguns exemplos de implementação:

{% gist paulocezar/8d317179d662fbb9407bd84ef8285520 %}

[maratona]: http://maratona.ime.usp.br/
[resultado-maratona]: http://maratona.ime.usp.br/vagas17.html
[tutorial-segtree]: https://www.hackerearth.com/practice/notes/segment-tree-and-lazy-propagation/
[uri-1477-homem]: https://www.urionlinejudge.com.br/judge/pt/problems/view/1477
[casa-pombos]: https://pt.wikipedia.org/wiki/Princ%C3%ADpio_da_casa_dos_pombos
[binomio-newton]: https://pt.wikipedia.org/wiki/Bin%C3%B3mio_de_Newton
[matrix-expo]: http://fusharblog.com/solving-linear-recurrence-for-programming-contest/
