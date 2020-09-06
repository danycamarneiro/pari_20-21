Aula 1 - PARI, Sumário e Exercícios, 18 Set 2019
================================================
Vitor Santos <vitor@ua.pt>
v6.0, Sep. 2019

// Instruções especiais para o asciidoc usar icons no output
:icons: html5
:iconsdir: /etc/asciidoc/images/icons 


.Sumário
-----------------------------------------------
Introdução
    Apresentação
    Objetivos
    Programa
    Avaliação
Introdução ao Linux - A shell
Alguns comandos básicos
Redirecionamento (saida e entrada de comandos)
Pipes e encadeamento de comandos
Editores (pycharm e sua configuração)
Programas elementares em python
-----------------------------------------------


[TIP]
===================================================
.Pressupostos para a realização dos exercícios
- Ter o Linux instalado (ubuntu 18.04 *altamente recomendado*).
- Ter o acesso de rede configurado (_wireless_).
*   Consultar as instruções do site dos 
http://www.ua.pt/stic/PageText.aspx?id=15224[sTIC].
===================================================


Instalação do Ubuntu
--------------------
Existem diveras formas de usar o Ubuntu para quem tem outros sistemas
operativos (Windows, MacOS). As mais interessantes são:

  . Uso do live ubuntu: https://tutorials.ubuntu.com/tutorial/try-ubuntu-before-you-install[Try before you install]
  . Instalar uma máquina virtual (`virtualbox` ou outra) e instalar o Linux na máquina virtual.
  . Instalar o Linux em dual-boot com o Windows (Esta é a forma recomendada. As outras formas serão pouco adequadas em breve).

As duas primeiras soluções não interferem no disco nem no sistema operativo
existente, mas são mais limitadas em termos de funcionalidades e desempenho.
No caso da primeira, todo o trabalho que for feito se perde no fim da sessão
se não for copiado para outro local.
No caso da máquina virtual, vai ser preciso espaço em disco no ambinente Windows
(ou MacOs) para criar a "imagem" do disco onde correrá o Linux em máquina
virtual. É uma solução intermédia que funciona relativamente bem, mas como opera
sobre o sistema operativo nativo, pode ter limitações de desempenho e ficará
dependente da atividade desse sistema operativo (como as atualizações no
Windows).

A terceira solução (dual-boot com o sistema operativo nativo) é a mais poderosa
porque cada sistema operativo fica no seu próprio espaço e correm separadamente.
Porém, é preciso repartir o disco que estaria todo atribuído ao sistema
operativo nativo. O Linux oferece esta possibilidade durante a instalação e em
geral o processo corre bem, mas há sempre o risco de perda de informação.
Por isso, recomenda-se guardar toda a informação importante desenvolvida no
sistema operativo original antes de fazer esta forma de instalação.

Mais informações podem ser obtidas por exemplo nos seguintes endereços:

  * https://tutorials.ubuntu.com/
  * https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop

Notas iniciais sobre os ficheiros de apoio às aulas
---------------------------------------------------

[NOTE]
.Transformar os ficheiros de Sumários e Exercícios de ASCIIDOC para HTML
Estes ficheiros de Sumários são legíveis no formato ASCII, mas podem
ser convertidos em HTML para uma melhor apresentação usando
o comando `asciidoc`. Este comando pode ser instalado no Ubuntu com
`sudo apt install asciidoc` bastando depois executar na linha de comando
`asciidoc SumarioA1.adoc`, ou seja, num terminal (que é uma janela onde se escrevem
comandos manualmente --- essa janela pode ser lançada a partir da interface gráfica
do linux a partir da zona das aplicações). NOTA: Antes de fazer instalações pode
ser necessário atualizar as fontes dos repositórios; isso faz-se com `sudo apt update`.
Para fazer o `syntax highlight` do código de programação incluído neste ficheiro o programa
recorre a comandos externos. O de defeito é o `source-highlight` e que se se
deve instalar previamente, por exemplo, com o comando `sudo apt install source-highlight`.

Como exercício, sugere-se tentar criar o ficheiro em formato HTML (++SumarioA1.html++)
a partir do ficheiro em formato asciidoc (++SumarioA1.adoc++).

[NOTE]
.Transformar os ficheiros de Sumários e Exercícios de ASCIIDOC para PDF
Os documentos em formato ASCIIDOC também podem ser convertidos em PDF recorrendo ao comando `a2x`,
que é uma forma elaborada de usar o `asciidoc` e outras
packages auxiliares como o `dblatex` (por defeito) ou o `FOP` para gerar outros
formatos (dos quais o PDF é o de defeito).
Para serem usados, estes comandos também devem ser instalados: `sudo apt install dblatex fop`.
Depois, nesse caso, bastará fazer `a2x SumarioA1.adoc` ou `a2x --fop SumarioA1.adoc` respetivamente.
Qualquer destes comandos tem opções na linha de comando que os tornam configuráveis.
O `dblatex` pode ter problemas com ficheiros com caracteres especiais (por
exemplo UTF-8) e isso tem de ser prevenido para executar sem erros. Por vezes
isso torna-se complexo e a opção `a2x --fop SumarioA1.adoc` acaba por ser a mais
cómoda.


[WARNING]
.Nomes das linguagens para o _syntax highlight_ e o formato PDF
Quando se gera o documento em PDF, pode haver conflitos de nomes nas linguagens
para o _syntax highlight_. Um desses casos é a linguagem de `makefile` que é
reconhecida pelo `source-highlight` mas não pelo `highlight` nem pelo `pygments` 
que ainda por cima disso espera `c` e não `C` para código fonte em linguagem C.
Esta questão alarga-se quando se usa o comando `a2x` para gerar PDF porque
ele recorre ao `dblatex` que tem o seu próprio `syntax highlight` para gerar PDF
e não reconhece a linguagem `makefile` mas sim `make` (embora pobre!). 
Nesse caso, e se se pretende criar o PDF, ou se usa a variante `a2x --fop`,
que não faz qualquer `syntax highlight`, ou então usa-se o `a2x` de defeito (`dblatex`),
e altera-se o tipo de linguagem _source_ de `makefile` para `make`; porém
aí é o `asciidoc` que não funcionará bem se não se usar o `source-highlighter`.
A questão pode-se tornar confusa e há, portanto, uma questão de compromissos. O `syntax highlight` gerado
pelo `source-highlight` é em geral mais rico que os outros, portanto recomenda-se.
Se for para gerar PDF, ou se abdica do `syntax highlight` (usando a2x --fop) 
ou se ajusta as linguagens (mormente de `makefile` para `make`) e usa-se
o `dblatex`, que é o processador de defeito do `a2x`.


Parte 1 - Apresentação e generalidades
--------------------------------------
Ver o documento `0-PARI2019-2020-Apresentação`


Parte 2 - Introdução ao Linux e a Shell
---------------------------------------
Ver o documento  `1-Linux-Breve Introdução`


Parte 3 - Criação do ambiente e instalação de ferramentas básicas
-----------------------------------------------------------------

Metodologia
~~~~~~~~~~~
Para melhor se desenvolver o trabalho nas aulas, deve-se
seguir uma metodologia de organização de ficheiros em diretórios
por aulas e por exercícios. Assim, recomenda-se consultar mais tarde um documento
a disponibilizar on-line para uma descrição mais detalhada dos procedimentos:
`Metodologias_Exercicios_PARI.pdf`; porém, fica desde já a indicação
que cada aula deve estar numa pasta separada `Aula1`, `Aula2`, etc.

Dentro de cada aula, em especial nas primeiras, é também recomendado criar uma
subpasta para cada exercício `Ex1`, `Ex2`, etc. Em certas aulas, ou aulas mais
avançadas, os diversos exercícios serão feitos por acréscimo sucessivo sobre o código
base dos exercícios anteriores; nessa altura serão dadas as instruções nesse
sentido.

Editor
~~~~~~
A ferramenta principal para criar e modificar ficheiros é o editor, muitas
vezes integrado num ambiente de desenvolvimento (IDE). Há inúmeras opções
desde simples editores (`gedit`, `kate`, etc.) até ambientes de
desenvolvimento muito sofisticados (`codeblocks`, `eclipse`, etc.).

Além das propriedades fundamentais dos editores, hoje em dia são excelentes
_add-ons_ a "automated completion" (preenchimento automático de palavras
e estruturas) , o "syntax highlight" (realce da sintaxe da linguagem),
o "intellissense" (apresentação de todas as opções de preenchimento
automático de campos e estruturas em variáveis, funções, etc.), ou a
inserção automática de fragmentos de código padrão ("code snippets").

O editor com mais tradição por excelência é o "vim" (ou "vi" improuved)
mas a sua utilização eficaz pode requerer anos de prática continuada e
permite todas as facilidades indicadas acima, mas a sua configuração,
por ser praticamente ilimitada, pode-se tornar complexa e, por isso,
contraproducente em utilizadores iniciados.

Assim, recomenda-se como alternativa uma solução aberta disponibilizada
pela Microsoft para muitas plataformas, incluindo linux. Trata-se do 'Visual Studio Code' ou 'vscode'.
Pode ser instalado diretamente do gestor de aplicações do Ubuntu ('Ubuntu
Software') ou por outras vias (https://askubuntu.com/questions/616075/how-do-i-install-visual-studio-code).

Configuração do 'vscode'
~~~~~~~~~~~~~~~~~~~~~~~~
O 'vscode' pode ser configurado de muitas formas e existem inúmeras extensões.

A primeira recomendação, embora seja uma quetão pessoal, é que se ajuste o
sistema de cores ('color theme') para facilitar a visualização e manipulação
do texto e realce da sintaxe. Há várias formas de o fazer (pelos menus, pela
página de 'welcome', icon de configurações no canto inferior esquerdo).
O tema "Solarized Light" pode ser uma boa opção por oposição a temas mais escuros
que vêm por defeito.

A seguir recomendam-se algumas extensões dedicadas à edição de código C/C{plus}{plus}.
As mais úteis podem ser:

* C/C{plus}{plus} for Visual Studio Code (C/C{plus}{plus} IntelliSense, debugging, and code browsing).
* C/C{plus}{plus} Clang Command aDapter (Completion and Diagnostic).

Para as instalar basta fazer uma busca nas "Extensions" no icon do painel do
lado esquerdo da janela principal, ou então usar menus (View->Extensions) ou
aceleradores de teclado (Ctrl+Shift+X). NO fim de se localizar a extensão
pretendida pode-se instala-la seguindo as instruções locais ("Install") ou se
já estiver instalada pode-se desinstallar ("Uninstall") ou ativar/desativar
("Enable/Disable")

Há outra extensões úteis em outras fases dos trabalhos, e as seguintes são
exemplos das inumeras possibilidades:

* Doxygen Documentation Generator (para gerar comentários automáticos em formato Doxygen)
* Better Comments  (para destacar visualmente comentários pela sua tipologia)

Este editor `vscode` é na verdade mais do que um simples editor, e além de permitir
muitas janelas e organizações do ecran (`layout`), permite ter janelas com
terminais de comando (menu Terminal) e até permite lançar comandos
personalizáveis. Porém, em prol de desenvolvimentos futuros, como na
programação profissional, devem-se ter soluções mais abertas e não
vinculadas a um ecossistema fechado, como são alguns IDEs proprietários.
Por isso, nesta UC de PARI, não se exploram IDEs específicos e limitados,
mas antes se promove o uso separado de algumas ferramentas, deixando a opção
por um determinado IDE a eventuais profissionalizações futuras!

Parte 4 - Primeiros exercícios de programação em C
--------------------------------------------------

Exercício 1
~~~~~~~~~~~

Desenvolver um programa que imprima no terminal a frase "Hello World".
Editar o ficheiro `hello.c` com o editor escolhido (`gedit`, `kate`, etc.)

.hello.c
[source,C]
----------------------------
#include <stdio.h>
int main()
{
    printf("Hello World\n");
    return 0;
}
----------------------------

Compilar o programa com o seguinte comando: 

    gcc hello.c -o hello

Exercício 2
~~~~~~~~~~~
Criar um programa designado `primos` que imprime no ecran 
números primos, um por linha, até um certo limite.
Usar um `#define` e usar uma função auxiliar `isprime()`
que aceita um inteiro `n` e retorna 1 ou 0 conforme `n`
for primo ou não.

.primo.c
[source,C]
----------------------------------
#include <stdio.h>
#define NN 10000

int isprime(int); //function prototype

int main()
{
    int n;
    for(n=2;n < NN; n++)
    {
        if( isprime(n) )
        {
            printf("%d\n", n);
        }
    }
    return 0;
}

int isprime(int n)
{
    int k;
    for(k=2; k<n; k++)
    {
        // fill the appropriate code ...
        return 0;  // not prime!
    }
    return 1;  //if reached here, n is not prime
}
----------------------------------

Com a ajuda do programa, calcular quantos números primos 
inferiores a 10000 têm o algarismo 3.

    primos | grep "3" | wc -l

A resposta deve ser 561

Exercício 3
~~~~~~~~~~~
Calcular números perfeitos (aqueles cuja soma dos divisores igualam o número)
como por exemplo 6 = 3 + 2 + 1.
Além do `main()` criar a função `long sumDiv(long)`
que retorna a soma dos divisores de um número.

Usar uma `Makefile` e ter o `main()` separado das restantes funções
em dois ficheiros distintos.
 
.Makefile
[source,makefile]
----------------------------------
#My source files
SRC=main.c myf.c
PROG=perf
################################
CC=gcc
CFLAGS=-Wall
OBJ=$(SRC:.c=.o)
################################
$(PROG): $(OBJ)
	gcc $(OBJ) -o $(PROG) -lm

.c.o:
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(PROG) $(OBJ)
----------------------------------

[WARNING]
.TABs nas Makefiles
=========================================================
As ações associadas aos targets na `Makefile` devem 
começar sempre com um `TAB`.
=========================================================

Para compilar e linkar o programa basta fazer:

    make


// vim: set syntax=asciidoc:
