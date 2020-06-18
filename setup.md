---
layout: page
title: Setup
permalink: /setup/index.html
root: ..
---

## Visão geral

Esta lição foi criada para ser feita em um computador pessoal.
Todo o software e dados usados ​​nesta lição estão disponíveis gratuitamente on-line,
e instruções sobre como obtê-los são fornecidas abaixo.

## Instalar Python

Nesta lição, usaremos o Python 3 com algumas de suas bibliotecas científicas mais populares.
Embora seja possível instalar manualmente um Python básico e todas as bibliotecas necessárias,
recomendamos instalar [Anaconda][anaconda-website],
uma distribuição Python que vem com tudo o que precisamos para a lição.
Instruções detalhadas de instalação para vários sistemas operacionais podem ser encontradas
em The Carpentries [modelo de website para oficinas][anaconda-instructions]
e na [documentação do pacote Anaconda][anaconda-install].

## Obter dados para a lição

1. Baixe [python-novice-inflammation-data.zip][zipfile1]
        e [python-novice-inflammation-code.zip][zipfile2].
2. Crie uma pasta chamada `swc-python` em seu Desktop (Área de Trabalho).
3. Mova os dois arquivos baixados para `swc-python`.
4. Des-zipe os arquivos.

Agora você deverá pastas `data` e `code` na pasta `swc-python` 
em seu Desktop (Área de Trabalho).

## Abra o console do Python

Para começar a trabalhar com Python, precisamos abrir um programa que interprete e execute
comandos Python. Tal programa é um _console_ do Python. Abaixo listamos várias opções. Se você não tem uma preferência, use a primeira
opção que estiver instalada em sua máquina. Ou então, use o console de sua preferência.

## Option A: Jupyter Notebook

A Jupyter Notebook provides a browser-based interface for working with Python.
If you installed Anaconda, you can launch a notebook in two ways:

> ## Anaconda Navigator
>
> 1. Launch Anaconda Navigator.
> It might ask you if you'd like to send anonymized usage information to Anaconda developers:
> ![Anaconda Navigator first launch](../fig/anaconda-navigator-first-launch.png)
> Make your choice and click "Ok, and don't show again" button.
> 2. Find the "Notebook" tab and click on the "Launch" button:
> ![Anaconda Navigator Notebook launch](../fig/anaconda-navigator-notebook-launch.png)
> Anaconda will open a new browser window or tab with a Notebook Dashboard showing you the
> contents of your Home (or User) folder.
> 3. Navigate to the `data` directory by clicking on the directory names leading to it:
> `Desktop`, `swc-python`, then `data`:
> ![Anaconda Navigator Notebook directory](../fig/jupyter-notebook-data-directory.png)
> 4. Launch the notebook by clicking on the "New" button and then selecting "Python 3":
> ![Anaconda Navigator Notebook directory](../fig/jupyter-notebook-launch-notebook.png)
{: .solution}

> ## Command line (Terminal)
>
> 1\. Navigate to the `data` directory:
>
> > ## Unix shell
> > If you're using a Unix shell application, such as Terminal app in macOS, Console or Terminal
> > in Linux, or [Git Bash][gitbash] on Windows, execute the following command:
> > ~~~
> > cd ~/Desktop/swc-python/data
> > ~~~
> > {: .language-bash}
> {: .solution}
>
> > ## Command Prompt (Windows)
> > On Windows, you can use its native Command Prompt program.  The easiest way to start it up is
> > pressing <kbd>Windows Logo Key</kbd>+<kbd>R</kbd>, entering `cmd`, and hitting
> > <kbd>Return</kbd>. In the Command Prompt, use the following command to navigate to
> > the `data` folder:
> > ~~~
> > cd /D %userprofile%\Desktop\swc-python\data
> > ~~~
> > {: .source}
> {: .solution}
>
> 2\. Start Jupyter server
>
> > ## Unix shell
> > ~~~
> > jupyter notebook
> > ~~~
> > {: .language-bash}
> {: .solution}
>
> > ## Command Prompt (Windows)
> > ~~~
> > python -m notebook
> > ~~~
> > {: .source}
> {: .solution}
>
> 3\. Launch the notebook by clicking on the "New" button on the right and selecting "Python 3"
> from the drop-down menu:
> ![Anaconda Navigator Notebook directory](../fig/jupyter-notebook-launch-notebook2.png)
{: .solution}

&nbsp; <!-- vertical spacer -->

## Option B: IPython interpreter

IPython is an alternative solution situated somewhere in between the plain-vanilla Python
interpreter and Jupyter Notebook. It provides an interactive command-line based interpreter with
various convenience features and commands.  You should have IPython on your system if you installed
[Anaconda][anaconda-instructions].

To start using IPython, execute:
~~~
ipython
~~~
{: .source}

&nbsp; <!-- vertical spacer -->

## Option C: plain-vanilla Python interpreter

To launch a plain-vanilla Python interpreter, execute:
~~~
python
~~~
{: .source}

If you are using [Git Bash on Windows][gitbash], you have to call Python _via_ `winpty`:
~~~
winpty python
~~~
{: .source}

[anaconda-install]: https://docs.anaconda.com/anaconda/install
[anaconda-instructions]: https://carpentries.github.io/workshop-template/#python
[anaconda-website]: https://www.anaconda.com/
[gitbash]: https://gitforwindows.org
[zipfile1]: {{ page.root }}/data/python-novice-inflammation-data.zip
[zipfile2]: {{ page.root }}/code/python-novice-inflammation-code.zip
