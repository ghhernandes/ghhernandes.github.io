---
layout: post
title: Armadilha do valor padrão
---

Normalmente quando iremos criar algum argumento de função e métodos, definimos um **valor default** com o fim de tornar a utilização
do mesmo opcional. Muito útil! porém, Python possui uma pequena armadilha que pode se transformar em uma enorme dor de cabeça caso 
passe despercebido. Essa armadilha acontece quando utilizamos valores de tipo **mútaveis** *(calma, já vou explicar!)* como 
valor default do argumento.


#### Afinal, o que são os tipos mutáveis e imutáveis?

De acordo com a [documentação do Python](https://docs.python.org/3.4/reference/datamodel.html), os valores de objetos podem mudar.
Esses objetos que tem seus valores alterados após criados, são chamados de **mutáveis**. Facilitou agora, não?

E como você já deve ter percebido, os objetos que não podem ter seus valores alterados após serem criados, são chamados de... **imutáveis**!

###### Mas, qual os tipos são mutáveis e quais são imutáveis?
**- Tipos mutáveis:** Dicionários, listas e tipos definidos pelo usuário

**- Tipos imutáveis:** São os strings, números e tuplas;


Algumas pessoas tem dúvidas sobre o que é uma **tupla**, na [documentação do Python](https://docs.python.org/2/tutorial/datastructures.html#tuples-and-sequences)
você irá encontrar a solução para seus problemas. Outro post que explica muito bem, é o [post do Luciano Ramalho](http://pythonclub.com.br/tuplas-mutantes-em-python.html) *(recomendo)*.

#### Ação!

Se você é acostumado em utilizar valores default, estará familiarizado com algo desse tipo:

```
def test_function(list=[]):
    list.append(5)
    print(list)
```

Executando essa função 5 vezes, teremos o resultado abaixo:

```
>>> test_function()
[5]
>>> test_function()
[5, 5]
>>> test_function()
[5, 5, 5]
>>> test_function()
[5, 5, 5, 5]
>>> test_function()
[5, 5, 5, 5, 5]
```
Isso mesmo! o valor do argumento *list* foi alterado nas 5 vezes, sem ao menos passarmos algum valor ao mesmo.

Isso acontece porque o Python, por motivos de otimização, não cria a lista ``list`` com os argumentos vazios todas as
vezes que executamos a função. Ele reaproveita a lista criada no momento em que essa função foi chamada na primeira execução.
