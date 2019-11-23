---
layout: post
title: Processamento de dados de alta performance com NumPy e Numba
---

Python é uma linguagem muito utilizada para processamento de dados por ser efetiva e de rápido desenvolvimento, porém possui um grande problema: python puro é lento. Por ser uma linguagem interpretada e de alto nível, cada linha de código deve ser traduzida para binário cada vez que é executada, e para um desenvolvimento mais rápido o gerenciamento de memória é abstraído.

Para comprovar isso, usaremos duas ferramentas:

**Numpy** (https://numpy.org) é um pacote para computação científica utilizando Python com sua maior parte escrita na linguagem C, e pode ser utilizada para trabalhar com vetores N-dimensionais com alto desempenho.

**Numba** (http://numba.pydata.org) é responsável por traduzir código Python em código de máquina otimizada utilizando o compilador LLVM (https://llvm.org), possibilitando atingir a velocidade da linguagem C ou Fortran em operações numéricas.

Métodos utilizados para o teste:

![](https://raw.githubusercontent.com/ghhernandes/dataperformance-tests/master/img/test_code.png)

No código acima possuímos três métodos que possuem o mesmo resultado final, porém um utiliza python puro, o outro Numba e posteriormente é utilizado o NumPy, respectivamente.

Na imagem abaixo conseguimos ver que após realizar 64 milhões de operações, o tempo de processamento de um código em Python puro foi 6 vezes maior em comparação com o Numba.

![](https://raw.githubusercontent.com/ghhernandes/dataperformance-tests/master/img/tempo_decorrido_numba.png)

Em outra análise, podemos constatar que o aumento do tempo de execução do Python puro conforme o número de operações aumenta, é muito maior comparado as demais ferramentas:

![](https://raw.githubusercontent.com/ghhernandes/dataperformance-tests/master/img/tempo_decorrido_numba_2.png)

Como esperado, o código Python puro foi mais lento nesse caso. Porém vale lembrar que existe casos onde ele pode ser mais rápido para poucas operações, não necessitando de ferramentas adicionais.