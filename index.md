---
layout: lesson
root: .
permalink: index.html
---

## Análise de Dados c/ Python (junho/2020)

Bem-vinda à Oficina de Análise de Dados com Luciano Ramalho.
Essa turma gratuita é oferecida para mulheres, como uma pequena contribuição para reduzir a presença desproporcional de homens entre as pessoas desenvolvedoras.

> ## Pré-requisitos
>
> Para participar, você precisa entender os conceitos de **arquivos** e **diretórios**, e como
> iniciar um interpretador **Python 3** e digitar comandos básicos. Não é preciso saber **Python**.
>
> Nas atividades, você poderá usar o Python na linha de comando, o Jupyter Notebook ou outro console interativo.
> Se precisar de ajuda para instalar Python ou Jupyter,
> apareça no encontro de preparação conforme instruções que enviaremos por e-mail.
> Teremos pessoas monitoras para ajudar na configuração do ambiente e nos exercícios.
>
> Para aproveitar a oficina, é necessário disposição para seguir instruções por escrito.
> Primeira instrução: a senha solicitada na inscrição é "Katherine Johnson"
{: .prereq}

### Datas e horários

Serão 4 encontros online por Zoom, 3ª/5ª-feiras, 18:30, com duração de 1h30 ou 3h00, dessa forma:

* 16/jun, de 18:30 a 19:30 (encontro opcional): estaremos online para ajudar as pessoas a instalar Python 3.8 e Jupyter Notebook
* 18, 23, 25/jun, de 18:30 a 21:30: aulas expositivas e exercícios (com intervalos para descansar) 

### Como se inscrever

Preencha este formulário: **LOTOU!** (40 inscritas).
Preencher o formulário não garante a inscrição. Você receberá um e-mail confirmando se conseguiu uma vaga ou se a turma lotou.

## O resto desta página...

É a apresentação do material que vamos estudar.
As aulas serão faladas em português, e os enunciados dos exercícios também serão traduzidos para o português.
Mas o material completo por enquanto está em inglês.

A página inicial do curso em inglês está [aqui](index-en.md)

### Arthritis Inflammation
We are studying **inflammation in patients** who have been given a new treatment for arthritis, and
need to analyze the first dozen data sets of their daily inflammation. The data sets are stored in
[comma-separated values]({{ page.root }}/reference/#comma-separated-values) (CSV) format:

- each row holds information for a single patient,
- columns represent successive days.

The first three rows of our first file look like this:
~~~
0,0,1,3,1,2,4,7,8,3,3,3,10,5,7,4,7,7,12,18,6,13,11,11,7,7,4,6,8,8,4,4,5,7,3,4,2,3,0,0
0,1,2,1,2,1,3,2,2,6,10,11,5,9,4,4,7,16,8,6,18,4,12,5,12,7,11,5,11,3,3,5,4,4,5,5,1,1,0,1
0,1,1,3,3,2,6,2,5,9,5,7,4,5,4,15,5,11,9,10,19,14,12,17,7,12,11,7,4,2,10,5,4,2,2,3,2,2,1,1
~~~
{: .source}
Each number represents the number of inflammation bouts that a particular patient experienced on a
given day. For example, value "6" at row 3 column 7 of the data set above means that the third
patient was experiencing inflammation six times on the seventh day of the clinical study.

So, we want to:

1. Calculate the average inflammation per day across all patients.
2. Plot the result to discuss and share with colleagues.

To do all that, we'll have to learn a little bit about programming.


### Getting Started
To get started, follow the directions on the "[Setup](setup/)" page to download data
and install a Python interpreter.
