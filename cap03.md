# Repositório Local
Gabriel Sartori  
29/10/2015  


### Instruções do Git

Neste capítulo, as instruções serão todas feitas no terminal mesmo que
existam alternativas gráficas para as mesmas. Isso enfatiza no que está
sendo feito além do fato de que no terminal todos devem ter os mesmos
recursos e os comandos irão produzir os mesmos resultados, o que faz
esse tutorial algo reproduzível. Para usufruir das ferramentas gráfica va até o capitulo 6 **link*.


Já temos o Git devidamente e com credenciais (nome e email) e
configurações aplicadas. Vamos então ver como o sistema de controle de
versão acontece.

Todas as instruções do Git são sinalizadas por começar com `git` seguido
da instrução/comando e seus argumentos complementares, se
existirem/necessários.




```sh
cd meu1repo ## Diretório de teste de comandos 
```

Antes de iniciarmos o repositório, vamos só verificar o cadastro. Se
você já usa o Git ou fez os procedimento apresentados na primeira
sessão, o comando abaixo vai retornar o nome e email usados e alguns
definições adicionais, caso existam. Em caso de ainda não ter
configurado o seu Git, informe o nome e email conforme apresentado na
sessão anterior.



```sh
## Mostra as informações/definições do usuário.
git config --list
```

```sh
user.name=Knight Rider
user.email=batman@justiceleague.org
```

Temos um diretório destinado ao projeto que será mantido sobre
versionamento, então vamos iniciar um repositório Git nele.


```bash
## Inicia um repositório sob versionamento Git.
git init
```

```
## Initialized empty Git repository in /home/gabriel/apostila-git/cap03/meu1repo/.git/
```

O Git retorna a mensagem de inicilização do repositório. Nesse momento
ele cria um diretório oculto `.git/` com subdiretórios que são o coração
do sistema de versionamento. Você não deve modificar nada nesse
diretório. É por essa razão que ele é oculto. Alterar o conteúdo pode
prejudicar ou interromper o funcionamento do Git. Se você quiser
encerrar o processo de versionamento fazendo com que esse diretório seja
como qualquer outro diretório, é só excluir a diretório `.git/`. Cada
subdiretório do `.git/` tem um propósito mas deixaremos os
esclarecimentos para o futuro. Por agora vamos apenas conferir a sua
estrutura.


```bash
## Mostra todo conteúdo do diretório.
tree -a
```

```
## .
## └── .git
##     ├── branches
##     ├── config
##     ├── description
##     ├── HEAD
##     ├── hooks
##     │   ├── applypatch-msg.sample
##     │   ├── commit-msg.sample
##     │   ├── post-update.sample
##     │   ├── pre-applypatch.sample
##     │   ├── pre-commit.sample
##     │   ├── prepare-commit-msg.sample
##     │   ├── pre-push.sample
##     │   ├── pre-rebase.sample
##     │   └── update.sample
##     ├── info
##     │   └── exclude
##     ├── objects
##     │   ├── info
##     │   └── pack
##     └── refs
##         ├── heads
##         └── tags
## 
## 10 directories, 13 files
```

**NOTA**: o `tree` é um programa instalado a parte (*third party
software*) que retorna arte ASCII representado a estrutura de
diretórios. Se você usa distribuição Debian, instale com `sudo apt-get
install tree`. Windows: [tree][].

## Minha Primeira Sessão

Vamos começar da maneira mais simples, criando um arquivo com uma linha
de texto apenas. Bem, vale avisar que ao longo desse tutorial, os
arquivos serão sempre bem pequenos e dificilmente realistas, mas como o
enfoque está no funcionamento, não haverá prejuízo.

Vamos criar o arquivo com conteúdo também pelo terminal. Se você
preferir, abra um editor de texto favorito (Emacs, Gedit, Geany,
RStudio, Bloco de Notas, etc) e faça algo mais elaborado.



```bash
## Cria o arquivo README.txt com a linha - Meu primeiro repositório Git.
echo "Meu primeiro repositório Git" > README.txt

## Lista os arquivos do diretório.
tree
```

```
## .
## └── README.txt
## 
## 0 directories, 1 file
```

Ao criarmos o arquivo e pedirmos a situação (*status*), ele indica que 
existe um arquivo não restreado (*untracked*) no diretório. Inclusive 
sugere uma ação que seria adicionar o aquivo (*add*). Se o seu sistema 
operacional está em português, parte dos outputs do Git podem estar 
traduzidos.



```bash
## Reconhecimento do Git sobre aquivo criado.
git status
```

```
## On branch master
## 
## Initial commit
## 
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
## 
## 	README.txt
## 
## nothing added to commit but untracked files present (use "git add" to track)
```

A situação está o seguinte: figura-cap03-situation:

Temos 3 estágios para o controle versionamento, após ter criado o docum
-ento, está na condição diretório de trabalho. Aonde os arquivos não está
rastreado, apenas no seu computador como qualquer outro. Para tornar ver
sionado precisa passar para área temporária (add) e depois confirmar (commit). Após conf
irmado então o arquivo está tendo controle de versão. Faremos então este
processo.


Para que o arquivo seja incluído no monitoramento é necessário que ele
receba o primeiro comando *add*. Isso marca a entrada dele no projeto
como um arquivo que a partir de então será versionado. O *status* agora
não indica mais que ele está *untracked* mas sim que existem mudanças
para serem registradas (*changes to be commited*). A melhor tradução de
*commit*, pensando no seu uso em Git, é **fechar sob segurança**. Quando
um *commit* é feito, cria-se um instante na linha do tempo que salva o
estado do projeto. Para esse instante o projeto pode ser retrocedido,
voltando o condição/conteúdo de todos os arquivos para o momento no qual
o mencionado *commit* foi feito. Você pode voltar para um *commit* de
semanas e até anos atrás.

O controle de versão não é apenas voltar os arquivos para o conteúdo que
eles tinham no passado. Arquivos rastreados que foram deletados ou
renomeados são recuperados. Até mesmo as permissões de
leitura/escrita/execussão dos arquivos são comtempladas no
versionamento.


```bash
## O primeiro `add` submete o arquivo ao versionamento.
git add README.txt
git status
```

```
## On branch master
## 
## Initial commit
## 
## Changes to be committed:
##   (use "git rm --cached <file>..." to unstage)
## 
## 	new file:   README.txt
```

O arquivo `README.txt` já é visto pelo Git como um arquivo com o qual
ele deve se "preocupar", pois está sob versionamento. Vamos agora fazer
um registro definitivo sobre o estado desse arquivo (*commit*). É de
fundamental importância que a mensagem de notificação, ou mensagem de
*commit*, reflita as moficações feitas. São as mensagens que serão
consultadas quando você precisar desfazer/voltar. Ela deve ser curta (<=
72 caracteres) e ao mesmo tempo informativa. A minha primeira mensagem
não será, todavia.


Boas Práticas de commit: 

- Verbo no indicativo
- Frases curtas
- Dizer o que fez e não como fez

Péssimas Práticas de commit:

"BLABLABLABLA"
"Trabalhei muito hoje"
"Terminando este trabalho na madruga"


```bash
## Registro de versão.
git commit -m "Cria arquivo com título."
```

```
## [master (root-commit) 7d5ce41] Cria arquivo com título.
##  1 file changed, 1 insertion(+)
##  create mode 100644 README.txt
```


O retorno da instrução de *commit* indica o número de arquivos incluídos
no *commit* e o número de inserções e deleções de linhas. O mais
importante está na primeira linha que informa o ramo de trabalho atual
(*branch*) e o *sha1* do *commit*. O *sha1* é uma sequência hexadecimal
de 40 digitos que representa unicamente o *commit*, então são $16^40$
possibilidades!. É por meio do *sha1* que podemos retroceder o
projeto. São mostrados apenas os 7 primeiros digitos porque são
suficientes para diferenciar *commits* dentro até mesmo de projetos
moderados ou grandes



# Aperfeiçoando

Vamos criar mais arquivos e acrescentar conteúdo ao já rastreado pelo
Git para percebermos o funcionamento. Escrever uma lista de razões para
usar o Linux. Deixei a lista curta poder ampliar no futuro e com erros
de português para corrigir depois.



```bash
## Adiciona mais linhas ao README.txt
echo "
A filosofia do Linux é 'Ria na face do perigo'.
Ôpa. Errado. 'Faça você mesmo'. É, é essa.
                            -- Lunus Torvalds" >> README.txt

## Cria uma lista de pontos sobre o porquê de usar o Linux.
echo "Por que usar o Linux?

* É livre
* É seguro
* É customizavel" > porqueLinux.txt
```


```bash
## Mostra o conteúdo do arquivo.
less README.txt
```

```
## Meu primeiro repositório Git
## 
## A filosofia do Linux é 'Ria na face do perigo'.
## Ôpa. Errado. 'Faça você mesmo'. É, é essa.
##                             -- Lunus Torvalds
```

```bash
## Mostra o conteúdo do arquivo.
less porqueLinux.txt
```

```
## Por que usar o Linux?
## 
## * É livre
## * É seguro
## * É customizavel
```

E o que o Git "acha" de tudo isso? O comando *status* é o mais usado do
Git, principalmente nas etapas de aprendizado. Uma característica
diferente do Git, se comparado a outras aplicações de uso por terminal,
é que ele é realmente camarada. Nas mensagens de *output*, o Gitque
informa o que aconteceu e também dá sugestões do que fazer.


```bash
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
## 
## 	modified:   README.txt
## 
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
## 
## 	porqueLinux.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```

O Git retornou dois campos. No primeiro ele diz que existem mudanças no
`README.txt` não encaminhadas para receber registro (*not staged for
commit*) e no segundo ele aponta que o `porqueLinux.txt` é um arquivo
não rastreado (fora de monitoramento).

Vamos explorar um pouco mais os recursos do Git antes de adicionar as
recentes mudanças. Até o momento, temos apenas um *commit* feito. Para
acessar o histórico de registros usamos `git log`. O histórico mostra o
*sha1*, o autor, data e mensagem de *commit*. Uma saída mais enxuta é
obtida com `git log --oneline`, útil quando o histórico é longo. É
possível fazer restrição no `git log`, como mostrar os *commits* a
partir de certa data, certo intervalo de datas, para um único autor ou
único arquivo. Visite: [git-log][].


```bash
## Mostra o histórico de commits.
git log
```

```
## commit 7d5ce4170045be9bb241a1261b641a94012ef12d
## Author: gabriel sartori <gabrielsartori2008@hotmail.com>
## Date:   Sat Nov 14 19:51:43 2015 -0200
## 
##     Cria arquivo com título.
```

O comando *diff* mostra as diferenças no conteúdo dos
arquivos/diretório. No caso, apenas o `README.txt` está sendo rastreado,
por isso o *output* indica a adição (`+`) de novas linhas. Na saída
tem-se os *sha1* das versões comparadas e o intervalo de linhas
envolvido na porção modificada (`@@`). Visite: [git-diffs][].


```bash
## Diferença nos arquivos versionados.
git diff
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
```

Vamos aplicar o primeiro *add* ao `porqueLinux.txt` para que ele começe
a ser versionado. Perceba que ao adicioná-lo, as mudanças, no caso a
criação do arquivo com contúdo, já são separadas para receber registro
(*changes to be commited*).


```bash
## Adiciona o arquivo ao processo de reastreamento.
git add porqueLinux.txt
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
## 
## 	new file:   porqueLinux.txt
## 
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
## 
## 	modified:   README.txt
```


```bash
## Mensagem que registra as modificações adicionadas.
git commit -m "Lista de inicial de o porquê usar o Linux."
```

```
## [master 2785f3e] Lista de inicial de o porquê usar o Linux.
##  1 file changed, 5 insertions(+)
##  create mode 100644 porqueLinux.txt
```


```bash
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
## 
## 	modified:   README.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```

Ainda resta o `REAMDE.txt` para receber registro. Você não precisa fazer
agora. Pode continuar editanto caso não tenha atingido uma quantidade de
modificação merecedora de *commit*. Lembre-se que registros geram
conteúdo no diretório `.git`. Quanto mais *commits*, mais conteúdo
gerado. Mas também, toda vez que você faz um *commit*, você define um
ponto de retorno, um estado salvo, caso precise no futuro
recuperar/visitar. O que é uma unidade de modificação comitável você irá
definir aos poucos com a prática.


```bash
## Encaminha o arquivo para receber registro.
git add README.txt
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
## 
## 	modified:   README.txt
```


```bash
## Atribui mensagem de notificação.
git commit -m "Adiciona frase do Linux Torvalds."
```

```
## [master 53fa265] Adiciona frase do Linux Torvalds.
##  1 file changed, 4 insertions(+)
```

Agora temos 3 *commits* e o *log* apresenta os *sha1* e as mensagens
correspondentes aos mesmos. Com `--oneline` resumimos o *output* mostrando
apenas o *sha1* e a mensagem de *commit*.


```bash
git log --oneline
```

```
## 53fa265 Adiciona frase do Linux Torvalds.
## 2785f3e Lista de inicial de o porquê usar o Linux.
## 7d5ce41 Cria arquivo com título.
```

Por meio dos *sha1*, podemos aplicar o *diff* para visitarmos as
modificações entre dois *commits*, não necessariamente consecutivos, por
exemplo. Também podemos retroceder (*checkout*, *reset*, *revert*) o
projeto para alguns desses pontos.

Abaixo instruímos o Git mostrar as diferenças para um *commit* atrás. A
cabeça (*HEAD*) é o que se entende como estado mais recente. Usa-se o
termo *HEAD* (cabeça) pois considera-se um crescimento do histórico
debaixo para cima no qual um novo *commit* é colocado em cima dos demais
(empilhado). O `HEAD@{0}` ou apenas `HEAD` representa o último registro
feito. Não é necessário escrever o último `HEAD` na intrução abaixo.


```bash
git diff HEAD@{1}
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
```

Agora inspecionado uma distância de 2 *commits* a partir do último. Aqui
tem-se os dois arquivos envolvidos nesse intervalo de 2 *commits*. Com
`--name-only` retorna-se só o nome dos arquivos.


```bash
git diff HEAD@{2} HEAD@{0}
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
## diff --git a/porqueLinux.txt b/porqueLinux.txt
## new file mode 100644
## index 0000000..8ecdfda
## --- /dev/null
## +++ b/porqueLinux.txt
## @@ -0,0 +1,5 @@
## +Por que usar o Linux?
## +
## +* É livre
## +* É seguro
## +* É customizavel
```


```bash
git diff --name-only HEAD@{2} HEAD@{0}
```

```
## README.txt
## porqueLinux.txt
```

Vamos resolver logo o caso da palavra sem acento em
`porqueLinux.txt`. Você abre o arquivo no seu editor de texto e modifica
conforme necessário. A modificação compreende um linha apenas mas aí
lembrei de mais coisas e acrescentei. O `git diff` mostra as
diferenças. Epa! As diferenças não eram entre *commits*? O conteúdo
adicionado ainda não recebeu notificação!




```bash
## Depois de corrigir palavras e adicionar conteúdo.
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
## 
## 	modified:   porqueLinux.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```

O Git sugere você aplicar *add* para preparar para *commit*. Caso as
modificações sejam um engano e não mais desejadas, você pode
desfazazê-las, abadonar a correção/inclusão das palavras usando
`checkout`. Vamos aplicá-lo para ver como funciona.


```bash
## Palavras corrigidas e mais itens adicionados.
less porqueLinux.txt
```

```
## Por que usar o Linux?
## 
## * É livre
## * É seguro
## * É customizável
## * Tem repositórios de software
## * Atualização constante
## * Desempenho
```


```bash
## Abandona modificações feitas presentes no arquivo.
git checkout -- porqueLinux.txt
```


```bash
less porqueLinux.txt
```

```
## Por que usar o Linux?
## 
## * É livre
## * É seguro
## * É customizavel
```

Bateu o arrependimento? Tem formas de poder retroceder com mudanças
ainda não registradas mas mantendo a possibilidade de
recuperá-las. Mostraremos em breve.

**NOTA**: sempre que quiser testar um comando novo e não está seguro do
que ele faz ou da extensão dos seus efeitos, faça uma cópia do projeto
em outro diretório e experimente ele lá. Isso previne sabores amargos,
pois algumas ações podem ser irreversíveis.


```bash
## Depois de desfazer as modificações no porqueLinux.txt
git status
```

```
## On branch master
## nothing to commit, working directory clean
```

Vamos seguir com as modificações em `porqueLinux.txt` que corrigem o
texto e acrescentam itens novos.




```bash
git status
```

```
## On branch master
## Changes not staged for commit:
##   (use "git add <file>..." to update what will be committed)
##   (use "git checkout -- <file>..." to discard changes in working directory)
## 
## 	modified:   porqueLinux.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```

O `diff` vazio compara o diretório de trabalho com o último registro
(último *commit*). Quando você usa explicitamente na instrução `HEAD@{ }`
seguido de número, então estão sendo comparadas versões
"commitadas". Existem variantes de sufixo para usar no `HEAD` que são:

  * `HEAD@{n}`
  * `HEAD^n`
  * `HEAD~n`

em que `n` é um número inteiro não negativo. Cada sulfixo tem uma
finalidade que não detalharemos agora. Visite: [git-caret-and-tilde][].


```bash
## Modificações no diretório vs último commit.
git diff
```

```
## diff --git a/porqueLinux.txt b/porqueLinux.txt
## index 8ecdfda..8747d1e 100644
## --- a/porqueLinux.txt
## +++ b/porqueLinux.txt
## @@ -2,4 +2,7 @@ Por que usar o Linux?
##  
##  * É livre
##  * É seguro
## -* É customizavel
## +* É customizável
## +* Tem repositórios de software
## +* Atualização constante
## +* Desempenho
```


```bash
## Último commit vs dois ancestrais, usando ~.
git diff HEAD~1 HEAD~0
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
```


```bash
## Último commit vs seu ancestral, usando @{}.
git diff HEAD@{1} HEAD@{0}
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
```


```bash
## Último commit vs dois ancestrais.
## git diff HEAD~2 HEAD~0
git diff HEAD@{2} HEAD@{0}
```

```
## diff --git a/README.txt b/README.txt
## index 07d3585..d0af1d3 100644
## --- a/README.txt
## +++ b/README.txt
## @@ -1 +1,5 @@
##  Meu primeiro repositório Git
## +
## +A filosofia do Linux é 'Ria na face do perigo'.
## +Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## +                            -- Lunus Torvalds
## diff --git a/porqueLinux.txt b/porqueLinux.txt
## new file mode 100644
## index 0000000..8ecdfda
## --- /dev/null
## +++ b/porqueLinux.txt
## @@ -0,0 +1,5 @@
## +Por que usar o Linux?
## +
## +* É livre
## +* É seguro
## +* É customizavel
```

Para ficar claro daqui em diante, você pode ao invés de pedir `log`,
pedir o `reflog` que incluí as referências em termos da sequência do
mais rencente para os seus ancestrais.


```bash
## Mostra referências para commits os ancentrais.
git reflog
```

```
## 53fa265 HEAD@{0}: commit: Adiciona frase do Linux Torvalds.
## 2785f3e HEAD@{1}: commit: Lista de inicial de o porquê usar o Linux.
## 7d5ce41 HEAD@{2}: commit (initial): Cria arquivo com título.
```


```bash
## Adiciona e commita.
git add porqueLinux.txt
git commit -m "Novos argumentos."
```

```
## [master c48f96c] Novos argumentos.
##  1 file changed, 4 insertions(+), 1 deletion(-)
```

O Git permite um nível de rastreabilidade bem fino. Veja por exemplo que
é possível saber quem modificou e quando cada linha do arquivo e qual o
correspondente *sha1* do *commit*.


```bash
## Mostra quem, onde e o que fez em cada arquivo.
git blame README.txt
```

```
## ^7d5ce41 (gabriel sartori 2015-11-14 19:51:43 -0200 1) Meu primeiro repositório Git
## 53fa265e (gabriel sartori 2015-11-14 19:51:44 -0200 2) 
## 53fa265e (gabriel sartori 2015-11-14 19:51:44 -0200 3) A filosofia do Linux é 'Ria na face do perigo'.
## 53fa265e (gabriel sartori 2015-11-14 19:51:44 -0200 4) Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## 53fa265e (gabriel sartori 2015-11-14 19:51:44 -0200 5)                             -- Lunus Torvalds
```




## Back to Past (Imagem de Volta para o Futuro)

git checkout
git mv *Não é bem assim
git reset 

## Ramificações 

Master
Branch

## Complementos
git blame
git show
git rm
git ls-files


## Ajuda

Git help
