Logic Puzzles (segunda versão)
===

Esse exercício lógico conta com a apresentação de 3 pessoas, 3 casas e 3 pets diferentes, onde o algoritmo tem que encontrar a solução que defina a cor da casa, a dona da casa e o pet que lá reside, com base nos argumentos passados. 

---

### Argumentos:
- Existem 3 casas alinhadas, cada uma com uma cor diferente: vermelha, verde e azul.
- Em cada casa vive uma pessoa: Alice, Bob e Carla.
- Cada pessoa tem um pet: gato, cachorro, hamster.
- Bob vive na casa vermelha.
- A pessoa que tem um gato vive na casa do meio.
- Carla tem um hamster e vive na casa ao lado da casa azul.
- A primeira casa é verde.

Qual a cor, o morador e o pet de cada casa?
___

## ⚙️ Solução

```prolog
ao_lado(X, Y, List) :- nextto(X, Y, List). % X à esquerda de Y
ao_lado(X, Y, List) :- nextto(Y, X, List). % Y à esquerda de X

solucao(Casas) :-
  Casas = [casa(_,verde,_),casa(_,_,gato),_],
  member(casa(_,_,cachorro),Casas),
  member(casa(_,azul,_),Casas),
  member(casa(_,_,hamster),Casas),
  member(casa(alice,_,_),Casas),
  member(casa(bob,vermelha,_),Casas),
  member(casa(carla,_,hamster),Casas),
  ao_lado(casa(carla,_,_),casa(_,azul,_),Casas).  
```

### Funções:
1. A primeira função que nos é apresentada é o `ao_lado`, que usa uma função do próprio Prolog chamada `nextto`, a qual verifica se o primeiro argumento está ao lado do segundo na lista passada.

2. Depois temos a função `member`, a qual verifica se uma `casa()` com os atributos passados é válida para o resto da sequência do código.

### Explicação do código:

O Prolog vai executar linha por linha, tentando satisfazer a condição escrita, conforme a lista passada em `Casas`, associando os atributos as casas e voltando atrás se necessário. A cada verificação que retornar verdadeiro ele segue em sequência até finalizar todas elas, retornando a lista com as opções que satisfazem as condições escritas.

---

### Bibliografia:

- [PDF de introdução à prolog](https://dcm.ffclrp.usp.br/~augusto/teaching/ia/IA-Prolog-Introducao-Tutorial.pdf)
- Ferramentas de IA