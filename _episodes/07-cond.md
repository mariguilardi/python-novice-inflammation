---
title: Making Choices
teaching: 30
exercises: 0
questions:
- "How can my programs do different things based on data values?"
objectives:
- "Write conditional statements including `if`, `elif`, and `else` branches."
- "Correctly evaluate expressions containing `and` and `or`."
keypoints:
- "Use `if condition` to start a conditional statement, `elif condition` to
   provide additional tests, and `else` to provide a default."
- "The bodies of the branches of conditional statements must be indented."
- "Use `==` to test for equality."
- "`X and Y` is only true if both `X` and `Y` are true."
- "`X or Y` is true if either `X` or `Y`, or both, are true."
- "Zero, the empty string, and the empty list are considered false;
   all other numbers, strings, and lists are considered true."
- "`True` and `False` represent truth values."
---

In our last lesson, we discovered something suspicious was going on
in our inflammation data by drawing some plots.
How can we use Python to automatically recognize the different features we saw,
and take a different action for each? In this lesson, we'll learn how to write code that
runs only when certain conditions are true.

## Conditionals

We can ask Python to take different actions, depending on a condition, with an `if` statement:

~~~
num = 37
if num > 100:
    print('greater')
else:
    print('not greater')
print('done')
~~~
{: .language-python}

~~~
not greater
done
~~~
{: .output}

The second line of this code uses the keyword `if` to tell Python that we want to make a choice.
If the test that follows the `if` statement is true,
the body of the `if`
(i.e., the set of lines indented underneath it) is executed, and "greater" is printed.
If the test is false,
the body of the `else` is executed instead, and "not greater" is printed.
Only one or the other is ever executed before continuing on with program execution to print "done":

![A flowchart diagram of the if-else construct that tests if variable num is greater than 100](../fig/python-flowchart-conditional.png)

Conditional statements don't have to include an `else`.
If there isn't one,
Python simply does nothing if the test is false:

~~~
num = 53
print('before conditional...')
if num > 100:
    print(num,' is greater than 100')
print('...after conditional')
~~~
{: .language-python}

~~~
before conditional...
...after conditional
~~~
{: .output}

We can also chain several tests together using `elif`,
which is short for "else if".
The following Python code uses `elif` to print the sign of a number.

~~~
num = -3

if num > 0:
    print(num, 'is positive')
elif num == 0:
    print(num, 'is zero')
else:
    print(num, 'is negative')
~~~
{: .language-python}

~~~
-3 is negative
~~~
{: .output}

Note that to test for equality we use a double equals sign `==`
rather than a single equals sign `=` which is used to assign values.

We can also combine tests using `and` and `or`.
`and` is only true if both parts are true:

~~~
if (1 > 0) and (-1 > 0):
    print('both parts are true')
else:
    print('at least one part is false')
~~~
{: .language-python}

~~~
at least one part is false
~~~
{: .output}

while `or` is true if at least one part is true:

~~~
if (1 < 0) or (-1 < 0):
    print('at least one test is true')
~~~
{: .language-python}

~~~
at least one test is true
~~~
{: .output}

> ## `True` and `False`
> `True` and `False` are special words in Python called `booleans`,
> which represent truth values. A statement such as `1 < 0` returns
> the value `False`, while `-1 < 0` returns the value `True`.
{: .callout}

## Checking our Data

Now that we've seen how conditionals work,
we can use them to check for the suspicious features we saw in our inflammation data.
We are about to use functions provided by the `numpy` module again.
Therefore, if you're working in a new Python session, make sure to load the
module with:

~~~
import numpy
~~~
{: .language-python}

From the first couple of plots, we saw that maximum daily inflammation exhibits
a strange behavior and raises one unit a day.
Wouldn't it be a good idea to detect such behavior and report it as suspicious?
Let's do that!
However, instead of checking every single day of the study, let's merely check
if maximum inflammation in the beginning (day 0) and in the middle (day 20) of
the study are equal to the corresponding day numbers.

~~~
max_inflammation_0 = numpy.max(data, axis=0)[0]
max_inflammation_20 = numpy.max(data, axis=0)[20]

if max_inflammation_0 == 0 and max_inflammation_20 == 20:
    print('Suspicious looking maxima!')
~~~
{: .language-python}

We also saw a different problem in the third dataset;
the minima per day were all zero (looks like a healthy person snuck into our study).
We can also check for this with an `elif` condition:

~~~
elif numpy.sum(numpy.min(data, axis=0)) == 0:
    print('Minima add up to zero!')
~~~
{: .language-python}

And if neither of these conditions are true, we can use `else` to give the all-clear:

~~~
else:
    print('Seems OK!')
~~~
{: .language-python}

Let's test that out:

~~~
data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

max_inflammation_0 = numpy.max(data, axis=0)[0]
max_inflammation_20 = numpy.max(data, axis=0)[20]

if max_inflammation_0 == 0 and max_inflammation_20 == 20:
    print('Suspicious looking maxima!')
elif numpy.sum(numpy.min(data, axis=0)) == 0:
    print('Minima add up to zero!')
else:
    print('Seems OK!')
~~~
{: .language-python}

~~~
Suspicious looking maxima!
~~~
{: .output}

~~~
data = numpy.loadtxt(fname='inflammation-03.csv', delimiter=',')

max_inflammation_0 = numpy.max(data, axis=0)[0]
max_inflammation_20 = numpy.max(data, axis=0)[20]

if max_inflammation_0 == 0 and max_inflammation_20 == 20:
    print('Suspicious looking maxima!')
elif numpy.sum(numpy.min(data, axis=0)) == 0:
    print('Minima add up to zero!')
else:
    print('Seems OK!')
~~~
{: .language-python}

~~~
Minima add up to zero!
~~~
{: .output}

In this way,
we have asked Python to do something different depending on the condition of our data.
Here we printed messages in all cases,
but we could also imagine not using the `else` catch-all
so that messages are only printed when something is wrong,
freeing us from having to manually examine every plot for features we've seen before.

> ## Quantos Caminhos?
>
> Considere esse código:
>
> ~~~
> if 4 > 5:
>     print('A')
> elif 4 == 5:
>     print('B')
> elif 4 < 5:
>     print('C')
> ~~~
> {: .language-python}
>
> Qual das seguintes respostas seria impressa se você executar esse código?
> Por que você selecionou essa resposta?
>
> 1.  A
> 2.  B
> 3.  C
> 4.  B and C
>
> > ## Resposta 
> > C é impresso porque as duas primeiras condições, `4 > 5` e `4 == 5`, não são verdadeiras,
> > mas `4 < 5` é verdade.
> {: .solution}
{: .challenge}

> ## O Que É Verdade?
>
> Os booleanos `True` e `False` não são os únicos valores em Python que são verdadeiro e falso.
> De fato, *qualquer* valor pode ser usado em um `if` ou `elif`.
> Depois de ler e executar o código abaixo,
> explique qual a regra para quais valores são considerados `True` e quais valores são considerados `False`.
>
> ~~~
> if '':
>     print('empty string is true')
> if 'word':
>     print('word is true')
> if []:
>     print('empty list is true')
> if [1, 2, 3]:
>     print('non-empty list is true')
> if 0:
>     print('zero is true')
> if 1:
>     print('one is true')
> ~~~
> {: .language-python}
{: .challenge}

> ## Isso Não É O Que Eu Quis Dizer
>
> Algumas vezes é útil verificar se uma condição não é verdadeira. 
> O operador Booleano `not` pode fazer isso explicitamente.
> Após ler e executar o código abaixo,
> escreva comandos com `if` que usam `not` para testar a regra
> que você formulou no desafio anterior.
>
> ~~~
> if not '':
>     print('empty string is not true')
> if not 'word':
>     print('word is not true')
> if not not True:
>     print('not not True is true')
> ~~~
> {: .language-python}
{: .challenge}

> ## Perto O Suficiente
>
> Escreva algumas condições que imprimam `True` se a variável `a` está dentro de 10% da variável `b`
> e `False` de outra forma.
> Compare sua implementação com sua colega:
> ambas tiveram a mesma resposta para todos os pares de números possíveis?
>
> > ## Resposta 1
> > ~~~
> > a = 5
> > b = 5.1
> >
> > if abs(a - b) < 0.1 * abs(b):
> >     print('True')
> > else:
> >     print('False')
> > ~~~
> > {: .language-python}
> {: .solution}
>
> > ## Resposta 2
> > ~~~
> > print(abs(a - b) < 0.1 * abs(b))
> > ~~~
> > {: .language-python}
> >
> > Isso funciona porque os Booleanos `True` e `False`
> > tem representações como strings que podem ser impressas.
> {: .solution}
{: .challenge}

> ## Operadores No Local
>
> Python (e a maior parte das linguagens na família C) fornece 
> operadores no local - [operadores in-place]({{ page.root }}/reference/#in-place-operators)
> que funcionam da seguinte forma:
>
> ~~~
> x = 1  # original value
> x += 1 # add one to x, assigning result back to x
> x *= 3 # multiply x by 3
> print(x)
> ~~~
> {: .language-python}
>
> ~~~
> 6
> ~~~
> {: .output}
>
> Escreva um código que soma os números positivos e negativos em uma lista separadamente,
> usando o operadores in-place.
> Esse resultado é mais ou menos legível
> do que escrever o mesmo sem os operadores in-place?
>
> > ## Resposta
> > ~~~
> > positive_sum = 0
> > negative_sum = 0
> > test_list = [3, 4, 6, 1, -1, -5, 0, 7, -8]
> > for num in test_list:
> >     if num > 0:
> >         positive_sum += num
> >     elif num == 0:
> >         pass
> >     else:
> >         negative_sum += num
> > print(positive_sum, negative_sum)
> > ~~~
> > {: .language-python}
> >
> > Here `pass` means "don't do anything".
> In this particular case, it's not actually needed, since if `num == 0` neither
> > sum needs to change, but it illustrates the use of `elif` and `pass`.
> {: .solution}
{: .challenge}

> ## Classificando Uma Lista em Baldes
>
> Na pasta `data`, grandes datasets estão armazenados em arquivos com nomes que iniciam com
> "inflammation-" e pequenos datasets -- em arquivos com nomes que iniciam com "small-". Também
> temos outros arquivos que não nos preocuparemos neste momento. Gostaríamos que quebrar todos 
> esses arquivos em três listas chamadas `large_files`, `small_files`, e `other_files`,
> respectivamente.
>
> Adicione um código para o modelo abaixo que faça isso. Observe que o método de string
> [`startswith`](https://docs.python.org/3/library/stdtypes.html#str.startswith)
> retorna `True` se, e somente se, a string em que é chamada começa com a string passada
> passada como argumento, isso é:
>
> ~~~
> "String".startswith("Str")
> ~~~
> {: .language-python}
> ~~~
> True
> ~~~
> {: .output}
> Mas
> ~~~
> "String".startswith("str")
> ~~~
> {: .language-python}
> ~~~
> False
> ~~~
> {: .output}
> Use o código Python a seguir como seu ponto de partida:
> ~~~
> filenames = ['inflammation-01.csv',
>          'myscript.py',
>          'inflammation-02.csv',
>          'small-01.csv',
>          'small-02.csv']
> large_files = []
> small_files = []
> other_files = []
> ~~~
> {: .language-python}
>
> Sua solução deve conter:
>
> 1.  um loop sobre os nomes dos arquivos
> 2.  descobrir qual grupo cada nome de arquivo pertence
> 3.  acrescentar o nome do arquivo a essa lista
>
> Ao final as três listas devem ser:
>
> ~~~
> large_files = ['inflammation-01.csv', 'inflammation-02.csv']
> small_files = ['small-01.csv', 'small-02.csv']
> other_files = ['myscript.py']
> ~~~
> {: .language-python}
>
> > ## Resposta
> > ~~~
> > for filename in filenames:
> >     if filename.startswith('inflammation-'):
> >         large_files.append(filename)
> >     elif filename.startswith('small-'):
> >         small_files.append(filename)
> >     else:
> >         other_files.append(filename)
> >
> > print('large_files:', large_files)
> > print('small_files:', small_files)
> > print('other_files:', other_files)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Contando Vogais
>
> 1. Escreva um loop que conta o número de vogais em uma string de caracteres.
> 2. Teste em algumas palavras individuais  e sentenças completas.
> 3. Uma vez finalizado, compare sua solução com sua colega.
>    Vocês tomaram as mesmas decisões sobre como lidar com a letra "y" 
>    (que algumas pessoas pensam ser uma vogal e outras não)?
>
> > ## Resposta
> > ~~~
> > vowels = 'aeiouAEIOU'
> > sentence = 'Mary had a little lamb.'
> > count = 0
> > for char in sentence:
> >     if char in vowels:
> >         count += 1
> >
> > print("The number of vowels in this string is " + str(count))
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

{% include links.md %}
