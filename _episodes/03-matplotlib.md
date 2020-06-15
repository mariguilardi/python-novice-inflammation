---
title: Visualizing Tabular Data
teaching: 30
exercises: 20
questions:
- "How can I visualize tabular data in Python?"
- "How can I group several plots together?"
objectives:
- "Plot simple graphs from data."
- "Group several graphs in a single figure."
keypoints:
- "Use the `pyplot` module from the `matplotlib` library for creating simple visualizations."
---

## Visualizing data
The mathematician Richard Hamming once said, "The purpose of computing is insight, not numbers," and
the best way to develop insight is often to visualize data.  Visualization deserves an entire
lecture of its own, but we can explore a few features of Python's `matplotlib` library here.  While
there is no official plotting library, `matplotlib` is the _de facto_ standard.  First, we will
import the `pyplot` module from `matplotlib` and use two of its functions to create and display a
heat map of our data:

~~~
import matplotlib.pyplot
image = matplotlib.pyplot.imshow(data)
matplotlib.pyplot.show()
~~~
{: .language-python}

![Heatmap of the Data](../fig/inflammation-01-imshow.svg)

Blue pixels in this heat map represent low values, while yellow pixels represent high values.  As we
can see, inflammation rises and falls over a 40-day period.  Let's take a look at the average inflammation over time:

~~~
ave_inflammation = numpy.mean(data, axis=0)
ave_plot = matplotlib.pyplot.plot(ave_inflammation)
matplotlib.pyplot.show()
~~~
{: .language-python}

![Average Inflammation Over Time](../fig/inflammation-01-average.svg)

Here, we have put the average inflammation per day across all patients in the variable `ave_inflammation`, then
asked `matplotlib.pyplot` to create and display a line graph of those values.  The result is a
roughly linear rise and fall, which is suspicious: we might instead expect a sharper rise and slower
fall.  Let's have a look at two other statistics:

~~~
max_plot = matplotlib.pyplot.plot(numpy.max(data, axis=0))
matplotlib.pyplot.show()
~~~
{: .language-python}

![Maximum Value Along The First Axis](../fig/inflammation-01-maximum.svg)

~~~
min_plot = matplotlib.pyplot.plot(numpy.min(data, axis=0))
matplotlib.pyplot.show()
~~~
{: .language-python}

![Minimum Value Along The First Axis](../fig/inflammation-01-minimum.svg)

The maximum value rises and falls smoothly, while the minimum seems to be a step function.  Neither
trend seems particularly likely, so either there's a mistake in our calculations or something is
wrong with our data.  This insight would have been difficult to reach by examining the numbers
themselves without visualization tools.

### Grouping plots
You can group similar plots in a single figure using subplots.
This script below uses a number of new commands. The function `matplotlib.pyplot.figure()`
creates a space into which we will place all of our plots. The parameter `figsize`
tells Python how big to make this space. Each subplot is placed into the figure using
its `add_subplot` [method]({{ page.root }}/reference/#method). The `add_subplot` method takes 3
parameters. The first denotes how many total rows of subplots there are, the second parameter
refers to the total number of subplot columns, and the final parameter denotes which subplot
your variable is referencing (left-to-right, top-to-bottom). Each subplot is stored in a
different variable (`axes1`, `axes2`, `axes3`). Once a subplot is created, the axes can
be titled using the `set_xlabel()` command (or `set_ylabel()`).
Here are our three plots side by side:

~~~
import numpy
import matplotlib.pyplot

data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))

axes1 = fig.add_subplot(1, 3, 1)
axes2 = fig.add_subplot(1, 3, 2)
axes3 = fig.add_subplot(1, 3, 3)

axes1.set_ylabel('average')
axes1.plot(numpy.mean(data, axis=0))

axes2.set_ylabel('max')
axes2.plot(numpy.max(data, axis=0))

axes3.set_ylabel('min')
axes3.plot(numpy.min(data, axis=0))

fig.tight_layout()

matplotlib.pyplot.show()
~~~
{: .language-python}

![The Previous Plots as Subplots](../fig/inflammation-01-group-plot.svg)

The [call]({{ page.root }}/reference/#function-call) to `loadtxt` reads our data,
and the rest of the program tells the plotting library
how large we want the figure to be,
that we're creating three subplots,
what to draw for each one,
and that we want a tight layout.
(If we leave out that call to `fig.tight_layout()`,
the graphs will actually be squeezed together more closely.)


> ## Escala de Plotagem
>
> Por que nossos gráficos terminam logo abaixo da extremidade superior?
>
> > ## Solução
>> Porque matplotlib normalmente define o limite do eixo x e Y de acordo com os valores mínimo e máximo dos nossos gráficos. 
> > (dependendo do intervalo de dados)
> {: .solution}
>
> Se quisermos alterar isto, podemos usar o método `set_ylim(min, max)`  para cada 'eixo',
> por exemplo:
>
> ~~~
> axes3.set_ylim(0,6)
> ~~~
> {: .language-python}
>
> Atualize seu código de plotagem para definir automaticamente uma escala mais apropriada.
> (Dica: Você pode user os métodos `max` e `min` para ajudar.)
>
> > ## Solução
> > ~~~
> > # Um método:
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0))
> > axes3.set_ylim(0,6)
> > ~~~
> > {: .language-python}
> {: .solution}
>
> > ## Solução
> > ~~~
> > # Um método mais automatizado:
> > min_data = numpy.min(data, axis=0)
> > axes3.set_ylabel('min')
> > axes3.plot(min_data)
> > axes3.set_ylim(numpy.min(min_data), numpy.max(min_data) * 1.1)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Desenhando Linhas Retas
>
> Nos subplots ao centro e à direita acima, esperamos que todas as linhas se pareçam passos de uma função porque
> valores não inteiros não são realistas para valores de mínimo e máximo. No entanto, você pode ver
> que as linhas nem sempre são verticais ou horizontais, e particularmente o passo da função
> no subplot da direita parece ser inclinado. Por quê?
>
> > ## Solução
> > Porque o matplotlib interpola (traça uma linha reta) entre dois pontos.
> > Uma maneira de evitar isso é usar a opção `drawstyle` do Matplotlib:
> >
> > ~~~
> > import numpy
> > import matplotlib.pyplot
> >
> > data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
> >
> > fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))
> >
> > axes1 = fig.add_subplot(1, 3, 1)
> > axes2 = fig.add_subplot(1, 3, 2)
> > axes3 = fig.add_subplot(1, 3, 3)
> >
> > axes1.set_ylabel('average')
> > axes1.plot(numpy.mean(data, axis=0), drawstyle='steps-mid')
> >
> > axes2.set_ylabel('max')
> > axes2.plot(numpy.max(data, axis=0), drawstyle='steps-mid')
> >
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0), drawstyle='steps-mid')
> >
> > fig.tight_layout()
> >
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> ![Plot with step lines](../fig/inflammation-01-line-styles.svg)
> {: .solution}
{: .challenge}

> ## Faça seu próprio plot
>
> Crie um plot mostrando o desvio padrão (`numpy.std`)
> dos dados de inflamação para cada dia de todos os pacientes.
>
> > ## Solução
> > ~~~
> > std_plot = matplotlib.pyplot.plot(numpy.std(data, axis=0))
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Movendo Áreas ao Redor
>
> Modifique o programa para mostrar os 3 plots, um em cima do outro
> em vez de um ao lado do outro.
>
> > ## Solução
> > ~~~
> > import numpy
> > import matplotlib.pyplot
> >
> > data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
> >
> > # change figsize (swap width and height)
> > fig = matplotlib.pyplot.figure(figsize=(3.0, 10.0))
> >
> > # change add_subplot (swap first two parameters)
> > axes1 = fig.add_subplot(3, 1, 1)
> > axes2 = fig.add_subplot(3, 1, 2)
> > axes3 = fig.add_subplot(3, 1, 3)
> >
> > axes1.set_ylabel('average')
> > axes1.plot(numpy.mean(data, axis=0))
> >
> > axes2.set_ylabel('max')
> > axes2.plot(numpy.max(data, axis=0))
> >
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0))
> >
> > fig.tight_layout()
> >
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

{% include links.md %}
