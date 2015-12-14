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


## Comandos De Verificação
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
ref log

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
## [master 448b201] Lista de inicial de o porquê usar o Linux.
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
## [master 41a3225] Adiciona frase do Linux Torvalds.
##  1 file changed, 4 insertions(+)
```

Agora temos 3 *commits* e o *log* apresenta os *sha1* e as mensagens
correspondentes aos mesmos. Com `--oneline` resumimos o *output* mostrando
apenas o *sha1* e a mensagem de *commit*.


```bash
git log --oneline
```

```
## 41a3225 Adiciona frase do Linux Torvalds.
## 448b201 Lista de inicial de o porquê usar o Linux.
## ffc1d12 Cria arquivo com título.
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
## 41a3225 HEAD@{0}: commit: Adiciona frase do Linux Torvalds.
## 448b201 HEAD@{1}: commit: Lista de inicial de o porquê usar o Linux.
## ffc1d12 HEAD@{2}: commit (initial): Cria arquivo com título.
```


```bash
## Adiciona e commita.
git add porqueLinux.txt
git commit -m "Novos argumentos."
```

```
## [master a2c3f0d] Novos argumentos.
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
## ^ffc1d12 (gabriel sartori 2015-11-24 14:31:29 -0200 1) Meu primeiro repositório Git
## 41a32255 (gabriel sartori 2015-11-24 14:31:30 -0200 2) 
## 41a32255 (gabriel sartori 2015-11-24 14:31:30 -0200 3) A filosofia do Linux é 'Ria na face do perigo'.
## 41a32255 (gabriel sartori 2015-11-24 14:31:30 -0200 4) Ôpa. Errado. 'Faça você mesmo'. É, é essa.
## 41a32255 (gabriel sartori 2015-11-24 14:31:30 -0200 5)                             -- Lunus Torvalds
```


## Fazendo cópias e trabalhando com ramos

Existem várias formas de se trabalham com ramos. Geralmente os ramos são
feitos sob demandas para adicionar uma característica ao projeto
(*feature*) ou corrigir um *bug*. Alguns ramos, por outro lado, são
ramos fixos destinados a receber o desenvolvimento dos ramos de
demanda. Esses ramos são geralmente chamados de *devel* (*development*)
e *release*. O ramo *master* é o default e em geral, para projetos
grandes, o *master* só recebe versões funcionais do projeito, livre de
bugs.

Para criar um ramo, usandos `git branch` seguido do nome que se
deseja. Vamos criar um ramo para adicionar mais arquivos ou modificações
ao projeto.


```bash
## Lista ramos (all), locais e remotos.
## git branch    ## Só ramos locais
## git branch -r ## Só ramos remotos
git branch -a ## Todos os ramos.
```

```
## * master
```


```bash
## Cria um ramo para adição de conteúdo, novo segmento.
git branch feature01
```


```bash
## Novo ramo criado aparece.
git branch
```

```
##   feature01
## * master
```


```bash
## Muda o HEAD de ramo.
git checkout feature01
```

```
## Switched to branch 'feature01'
```


```bash
## Situação no novo ramo.
git status
```

```
## On branch feature01
## nothing to commit, working directory clean
```


```bash
## Histórico de commits.
git log --oneline
```

```
## a2c3f0d Novos argumentos.
## 41a3225 Adiciona frase do Linux Torvalds.
## 448b201 Lista de inicial de o porquê usar o Linux.
## ffc1d12 Cria arquivo com título.
```

Veja que o novo ramo não começa no zero ou vazio (sem arquivos) e sim a
partir do ramo que é seu ancestral, ou seja, ele começa a partir do
último *commit* existente, por padrão. Vamos adicionar um arquivo e
commitar. O comando `wget` permite baixar arquivos pelo terminal. Será
baixado um arquivo com um função para calcular o fator de inflação de
variância (*vif*, variance inflation factor) usado em modelos de
regressão, disponível na página da [Professora Suely Giolo][].




```bash
## Baixando arquivo da internet. Uma função do R.
wget 'http://people.ufpr.br/~giolo/CE071/Exemplos/vif.R'
```


```
## --2015-11-24 14:31:30--  http://people.ufpr.br/~giolo/CE071/Exemplos/vif.R
## Resolving people.ufpr.br (people.ufpr.br)... ???.??.???.??, 2801:82:8020:0:8377:0:100:20
## Connecting to people.ufpr.br (people.ufpr.br)|???.??.???.??|:80... connected.
## HTTP request sent, awaiting response... 200 OK
## Length: 560
## Saving to: ‘vif.R’
## 
##      0K                                                       100% 44,0M=0s
## 
## 2015-11-24 14:31:30 (44,0 MB/s) - ‘vif.R’ saved [560/560]
```


```bash
## Situação do repositório após o download.
git status
```

```
## On branch feature01
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
## 
## 	vif.R
## 
## nothing added to commit but untracked files present (use "git add" to track)
```


```bash
git add vif.R
git commit -m "Adiciona função R para VIF."
```

```
## [feature01 ed304f7] Adiciona função R para VIF.
##  1 file changed, 20 insertions(+)
##  create mode 100644 vif.R
```


```bash
## Estrutura do diretório.
tree
```

```
## .
## ├── porqueLinux.txt
## ├── README.txt
## └── vif.R
## 
## 0 directories, 3 files
```


```bash
## Histórico de commits.
git reflog
```

```
## ed304f7 HEAD@{0}: commit: Adiciona função R para VIF.
## a2c3f0d HEAD@{1}: checkout: moving from master to feature01
## a2c3f0d HEAD@{2}: commit: Novos argumentos.
## 41a3225 HEAD@{3}: commit: Adiciona frase do Linux Torvalds.
## 448b201 HEAD@{4}: commit: Lista de inicial de o porquê usar o Linux.
## ffc1d12 HEAD@{5}: commit (initial): Cria arquivo com título.
```


```bash
git status
```

```
## On branch feature01
## nothing to commit, working directory clean
```

Então acabamos de acrescentar um novo aquivo ao projeto. Agora que as
modificações foram salvas (*commit* feito) podemos trocar de ramo. Você
vai ver que ao voltarmos para o ramo *master* o arquivo baixado da
internet vai "desaparecer".


```bash
## Volta para o ramo master.
git checkout master
```

```
## Switched to branch 'master'
```


```bash
## Estrutura do diretório.
tree
```

```
## .
## ├── porqueLinux.txt
## └── README.txt
## 
## 0 directories, 2 files
```

O arquivo `vif.R` não sumiu. Ele está no ramo `feature01` e só passará
para o ramo master quando mesclarmos o que existe no `feature01` ao
`master`. Então é assim: mudou de ramo, muda o conteúdo do
diretório. Fazer isso é bem simples, basta dar um `git merge`. Antes
vamos aprender como saber as diferenças que existem entre ramos.


```bash
## Mostra todas as modificações, cada linha modificada de cada arquivo.
git diff master feature01
```

```
## diff --git a/vif.R b/vif.R
## new file mode 100644
## index 0000000..a114969
## --- /dev/null
## +++ b/vif.R
## @@ -0,0 +1,20 @@
## +vif<-function (obj, digits = 5) {
## +    Qr <- obj$qr
## +    if (is.null(obj$terms) || is.null(Qr)) 
## +        stop("invalid 'lm' object:  no terms or qr component")
## +    tt <- terms(obj)
## +    hasintercept <- attr(tt, "intercept") > 0
## +    p <- Qr$rank
## +    if (hasintercept) 
## +        p1 <- 2:p
## +    else p1 <- 1:p
## +    R <- Qr$qr[p1, p1, drop = FALSE]
## +    if (length(p1) > 1) 
## +        R[row(R) > col(R)] <- 0
## +    Rinv <- qr.solve(R)
## +    vv <- apply(Rinv, 1, function(x) sum(x^2))
## +    ss <- apply(R, 2, function(x) sum(x^2))
## +    vif <- ss * vv
## +    signif(vif, digits)
## +   }
## +
```


```bash
## Mostra só os arquivos modificados.
git diff --name-only master feature01
```

```
## vif.R
```

Como você já havia antecipado, a única diferença entre os ramos `master`
e `feature01` é o arquivo `vif.R`. Agora é só pedir o `git merge`.


```bash
## Mesclando as modificações em feature01 no master.
git merge feature01 master
```

```
## Updating a2c3f0d..ed304f7
## Fast-forward
##  vif.R | 20 ++++++++++++++++++++
##  1 file changed, 20 insertions(+)
##  create mode 100644 vif.R
```


```bash
git log --oneline
```

```
## ed304f7 Adiciona função R para VIF.
## a2c3f0d Novos argumentos.
## 41a3225 Adiciona frase do Linux Torvalds.
## 448b201 Lista de inicial de o porquê usar o Linux.
## ffc1d12 Cria arquivo com título.
```

É possível criar um ramo a partir de um *commit* ancestral ao atual. Isso
é extremamente útil para resolver os bugs. Vamos fazer um segundo ramo a
partir do *commit* anterior a inclusão do arquivo R.


```bash
## Referencias aos commits.
git reflog
```

```
## ed304f7 HEAD@{0}: merge feature01: Fast-forward
## a2c3f0d HEAD@{1}: checkout: moving from feature01 to master
## ed304f7 HEAD@{2}: commit: Adiciona função R para VIF.
## a2c3f0d HEAD@{3}: checkout: moving from master to feature01
## a2c3f0d HEAD@{4}: commit: Novos argumentos.
## 41a3225 HEAD@{5}: commit: Adiciona frase do Linux Torvalds.
## 448b201 HEAD@{6}: commit: Lista de inicial de o porquê usar o Linux.
## ffc1d12 HEAD@{7}: commit (initial): Cria arquivo com título.
```


```bash
## Volta para antes do arquivo de baixar o vif.R.
git checkout HEAD@{4}
```

```
## Note: checking out 'HEAD@{4}'.
## 
## You are in 'detached HEAD' state. You can look around, make experimental
## changes and commit them, and you can discard any commits you make in this
## state without impacting any branches by performing another checkout.
## 
## If you want to create a new branch to retain commits you create, you may
## do so (now or later) by using -b with the checkout command again. Example:
## 
##   git checkout -b new_branch_name
## 
## HEAD is now at a2c3f0d... Novos argumentos.
```


```bash
## Qual a situação.
git status
```

```
## HEAD detached at a2c3f0d
## nothing to commit, working directory clean
```


```bash
## O histório existente nesse ponto.
git log --name-only --oneline
```

```
## a2c3f0d Novos argumentos.
## porqueLinux.txt
## 41a3225 Adiciona frase do Linux Torvalds.
## README.txt
## 448b201 Lista de inicial de o porquê usar o Linux.
## porqueLinux.txt
## ffc1d12 Cria arquivo com título.
## README.txt
```

Já que o *commit* mais recente dessa história aponta para o arquivo
compras, vamos checar o seu conteúdo apenas por medida de segurança.


```bash
## Mostra o conteúdo do arquivo.
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

Dito e feito! Voltamos no tempo para o instante logo após o *commit* que
incluí novos itens na lista. Podemos voltar para o presente se
estivermos satisfeitos com o passeio mas também podemos criar um ramo
aqui, caso isso seja necessário. Primeiro vamos voltar para o presente
depois mostramos como criar o ramo.


```bash
## Mostra onde estamos.
git branch
```

```
## * (detached from a2c3f0d)
##   feature01
##   master
```

Se não fizemos nenhuma modificação, voltar é bem simples. Se
modificações foram feitas é necessário saber se precisam ser mantidas e
onde ou se devem ser descartadas.


```bash
## Volta para o presente.
git checkout master
```

```
## Previous HEAD position was a2c3f0d... Novos argumentos.
## Switched to branch 'master'
```


```bash
git status
```

```
## On branch master
## nothing to commit, working directory clean
```


```bash
git log --oneline
```

```
## ed304f7 Adiciona função R para VIF.
## a2c3f0d Novos argumentos.
## 41a3225 Adiciona frase do Linux Torvalds.
## 448b201 Lista de inicial de o porquê usar o Linux.
## ffc1d12 Cria arquivo com título.
```


```bash
## Fenda no tempo fechada. Sem sinal do detached HEAD.
git branch
```

```
##   feature01
## * master
```


```bash
## Sinal do passeio no tempo.
git reflog
```

```
## ed304f7 HEAD@{0}: checkout: moving from a2c3f0d2a344bf7c680ec67982efca4f5cdf164c to master
## a2c3f0d HEAD@{1}: checkout: moving from master to HEAD@{4}
## ed304f7 HEAD@{2}: merge feature01: Fast-forward
## a2c3f0d HEAD@{3}: checkout: moving from feature01 to master
## ed304f7 HEAD@{4}: commit: Adiciona função R para VIF.
## a2c3f0d HEAD@{5}: checkout: moving from master to feature01
## a2c3f0d HEAD@{6}: commit: Novos argumentos.
## 41a3225 HEAD@{7}: commit: Adiciona frase do Linux Torvalds.
## 448b201 HEAD@{8}: commit: Lista de inicial de o porquê usar o Linux.
## ffc1d12 HEAD@{9}: commit (initial): Cria arquivo com título.
```

Vamos começar a ser ousados. Vamos voltar no passado, adicionar um
arquivo, commitar e ver o que acontece, como o histórico é representado.


```bash
## Volta no tempo, após commit que aumenta porqueLinux.txt.
git checkout HEAD@{6}
```

```
## Note: checking out 'HEAD@{6}'.
## 
## You are in 'detached HEAD' state. You can look around, make experimental
## changes and commit them, and you can discard any commits you make in this
## state without impacting any branches by performing another checkout.
## 
## If you want to create a new branch to retain commits you create, you may
## do so (now or later) by using -b with the checkout command again. Example:
## 
##   git checkout -b new_branch_name
## 
## HEAD is now at a2c3f0d... Novos argumentos.
```




```bash
## Baixa arquivo de dados da internet.
wget 'http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt'
```


```
## --(date +"%Y-%m-%d %H:%M:%S")--  http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt
## Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
## Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
## HTTP request sent, awaiting response... 200 OK
## Length: 217 [text/plain]
## Saving to: ‘pimentel_racoes.txt’
## 
##      0K                                                       100% 68,9M=0s
## 
## (date +"%Y-%m-%d %H:%M:%S") (68,9 MB/s) - ‘pimentel_racoes.txt’ saved [217/217]
## 
## ‘pimentel_racoes.txt’ -> ‘../meu1repo/pimentel_racoes.txt’
```


```bash
git status
```

```
## HEAD detached at a2c3f0d
## Untracked files:
##   (use "git add <file>..." to include in what will be committed)
## 
## 	pimentel_racoes.txt
## 
## nothing added to commit but untracked files present (use "git add" to track)
```


```bash
## Adiciona para registrar a inclusão do arquivo.
git add pimentel_racoes.txt
git commit -m "Adiciona aquivo de dados de experimento com rações."
```

```
## [detached HEAD 344674a] Adiciona aquivo de dados de experimento com rações.
##  1 file changed, 24 insertions(+)
##  create mode 100644 pimentel_racoes.txt
```


```bash
git status
```

```
## HEAD detached from a2c3f0d
## nothing to commit, working directory clean
```


```bash
## Log num formato gráfico ASCII para mostrar o novo ramo.
git log --graph --oneline --decorate --date=relative --all
```

```
## * 344674a (HEAD) Adiciona aquivo de dados de experimento com rações.
## | * ed304f7 (master, feature01) Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```

No nosso projeto temos o *master* e o *feature01* em igual condição, sem
nenhuma diferença. O *commit* recém feito indica um novo seguimento a
partir daquele onde adicionamos novos itens na lista. Vamos criar um
novo ramo porque atualmente estamos em um ramos suspenso (*detached
HEAD*) que não é persistênte.


```bash
git branch
```

```
## * (detached from a2c3f0d)
##   feature01
##   master
```


```bash
## Um novo ramo a partir do atual HEAD.
git checkout -b feature02
```

```
## Switched to a new branch 'feature02'
```


```bash
git branch
```

```
##   feature01
## * feature02
##   master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## * 344674a (HEAD, feature02) Adiciona aquivo de dados de experimento com rações.
## | * ed304f7 (master, feature01) Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```

Vamos explorar bem a funcionalidade. Vamos voltar para o `feature01` e
criar mais coisas lá. Você já deve estar pensando que tudo isso é
absurdo e jamais alguém firaria indo e voltando assim. Você está certo,
porém, quando o projeto envolve mais pessoas, cerrtamente as coisas irão
bifurcar em algum ponto.


```bash
git checkout feature01
```

```
## Switched to branch 'feature01'
```


```
## Diretório existe.
## Arquivo brasilCopa2014.txt já existe.
## ‘brasilCopa2014.txt’ -> ‘../meu1repo/brasilCopa2014.txt’
```


```bash
wget 'http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt'
```


```
## --2015-11-24 14:31:31--  http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt
## Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
## Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
## HTTP request sent, awaiting response... 200 OK
## Length: 1254 (1,2K) [text/plain]
## Saving to: ‘brasilCopa2014.txt’
## 
##      0K .                                                     100% 69,6M=0s
## 
## 2015-11-24 14:31:31 (69,6 MB/s) - ‘brasilCopa2014.txt’ saved [1254/1254]
```


```bash
git add brasilCopa2014.txt
git commit -m "Arquivo sobre copa 2014 celeção brasileira."
```

```
## [feature01 78a7842] Arquivo sobre copa 2014 celeção brasileira.
##  1 file changed, 22 insertions(+)
##  create mode 100644 brasilCopa2014.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## * 78a7842 (HEAD, feature01) Arquivo sobre copa 2014 celeção brasileira.
## * ed304f7 (master) Adiciona função R para VIF.
## | * 344674a (feature02) Adiciona aquivo de dados de experimento com rações.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```

Agora nos temos o *feature01* na frente do master e o *feature02* ao
lado. O conteúdo dos dois ramos terá que ser incorporado ao *master* em
algum momento porque é assim que funciona. Mas não há razões para
preocupação pois o propósito do Git é justamente facilitar esse
processo. Nesse caso, por exemplo, como as diferenças nos ramos consiste
na adição de arquivos diferentes, incorporar as modificações no *master*
será uma tarefa simples para o Git. O agravante é quando em dois ramos
(ou duas pessoas) o mesmo arquivo é modificado no mesmo intervalo de
linhas. Nessa situação o *merge* nos arquivos deve ser supervisionado e
não automático. Vamos incorporar as modificações dos ramos ao master
então.


```bash
## Volta para o master.
git checkout master
```

```
## Switched to branch 'master'
```


```bash
## Mescla o feature01.
git merge feature01 master
```

```
## Updating ed304f7..78a7842
## Fast-forward
##  brasilCopa2014.txt | 22 ++++++++++++++++++++++
##  1 file changed, 22 insertions(+)
##  create mode 100644 brasilCopa2014.txt
```


```bash
## Mescla o feature02.
git merge feature02 master
```

```
## Merge made by the 'recursive' strategy.
##  pimentel_racoes.txt | 24 ++++++++++++++++++++++++
##  1 file changed, 24 insertions(+)
##  create mode 100644 pimentel_racoes.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## *   0bac2be (HEAD, master) Merge branch 'feature02'
## |\  
## | * 344674a (feature02) Adiciona aquivo de dados de experimento com rações.
## * | 78a7842 (feature01) Arquivo sobre copa 2014 celeção brasileira.
## * | ed304f7 Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```


```bash
tree
```

```
## .
## ├── brasilCopa2014.txt
## ├── pimentel_racoes.txt
## ├── porqueLinux.txt
## ├── README.txt
## └── vif.R
## 
## 0 directories, 5 files
```

****
## Resolvendo conflitos

Agora vamos de propósito mostrar uma situação em que não é possível
fazer o merge automaticamente. Vamos criar um conflito. Para isso vou
criar um ramo novo, modificar o arquivo na última linha e commitar. Vou
voltar par ao *master* e fazer o mesmo mas vou usar um texto diferente
para incluir no arquivo. Já que os ramos *feature01* e *feature02* não
são mais necessários, podemos removê-los. No entanto, eles permanecem na
história do projeto e poder resurgir se você voltar no tempo.


```bash
## Remove ramos.
git branch -d feature01
git branch -d feature02
git branch
```

```
## Deleted branch feature01 (was 78a7842).
## Deleted branch feature02 (was 344674a).
## * master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## *   0bac2be (HEAD, master) Merge branch 'feature02'
## |\  
## | * 344674a Adiciona aquivo de dados de experimento com rações.
## * | 78a7842 Arquivo sobre copa 2014 celeção brasileira.
## * | ed304f7 Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```

Agora vou criar um novo ramo, adicionar um arquivo e encurtar o nome das
colunas no cabeçalho.


```bash
## Muda para um ramo criado na hora.
git checkout -b feature03
```

```
## Switched to a new branch 'feature03'
```




```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/bib1.txt'
```


```
## --2015-11-24 14:31:31--  http://www.leg.ufpr.br/~walmes/data/bib1.txt
## Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
## Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
## HTTP request sent, awaiting response... 200 OK
## Length: 535 [text/plain]
## Saving to: ‘bib1.txt’
## 
##      0K                                                       100% 35,0M=0s
## 
## 2015-11-24 14:31:31 (35,0 MB/s) - ‘bib1.txt’ saved [535/535]
```


```bash
## Mostra as 4 primeiras linhas.
head -4 bib1.txt
```

```
## repetição	variedade	bloco	y
## 1	1	1	20
## 1	2	1	18
## 1	3	2	15
```

Ao encurtar o nome para quatro dígitos, fica assim.


```bash
## Substitui o conteúdo da primeira linha pelos nomes truncados em 4
## dígidos e separados por tabulação. Etapa que você pode fazer no seu
## editor de texto.
sed -i "1s/.*/rept\tvari\tbloc\ty/" bib1.txt
head -4 bib1.txt
```

```
## rept	vari	bloc	y
## 1	1	1	20
## 1	2	1	18
## 1	3	2	15
```


```bash
git add bib1.txt
git commit -m "Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos."
```

```
## [feature03 ef648bb] Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
##  1 file changed, 58 insertions(+)
##  create mode 100644 bib1.txt
```

Baixamos e modificamos o arquivo. Adicionamos e fizemos o registro das
modificações. Agora vamos voltar ao *master* e baixar o arquivo também,
fazendo de conta que é outra pessoa trabalhando no mesmo projeto, mas
essa pessoa vai passar a cabeçalho para caixa alta.


```bash
git checkout master
```

```
## Switched to branch 'master'
```




```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/bib1.txt'
```

Ao encurtar o nome para quatro dígitos, fica assim.


```bash
## Substitui o conteúdo da primeira linha pelo mesmo em caixa alta. Faça
## isso no seu editor de texto de preferido.
sed -i '1s/.*/\U&/' bib1.txt
head -4 bib1.txt
```

```
## REPETIÇÃO	VARIEDADE	BLOCO	Y
## 1	1	1	20
## 1	2	1	18
## 1	3	2	15
```


```bash
git add bib1.txt
git commit -m "Arquivo de experimento em BIB. Cabeçalho em caixa alta."
```

```
## [master 87e8601] Arquivo de experimento em BIB. Cabeçalho em caixa alta.
##  1 file changed, 58 insertions(+)
##  create mode 100644 bib1.txt
```


```bash
git diff master feature03
```

```
## diff --git a/bib1.txt b/bib1.txt
## index a8dfaa6..b5f5963 100644
## --- a/bib1.txt
## +++ b/bib1.txt
## @@ -1,4 +1,4 @@
## -REPETIÇÃO	VARIEDADE	BLOCO	Y
## +rept	vari	bloc	y
##  1	1	1	20
##  1	2	1	18
##  1	3	2	15
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## * ef648bb (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
## | * 87e8601 (HEAD, master) Arquivo de experimento em BIB. Cabeçalho em caixa alta.
## |/  
## *   0bac2be Merge branch 'feature02'
## |\  
## | * 344674a Adiciona aquivo de dados de experimento com rações.
## * | 78a7842 Arquivo sobre copa 2014 celeção brasileira.
## * | ed304f7 Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```


```bash
## Dá mensagem de erro que informa o conflito.
git merge feature03 master
```


```
## Auto-merging bib1.txt
## CONFLICT (add/add): Merge conflict in bib1.txt
## Automatic merge failed; fix conflicts and then commit the result.
```


```bash
git status
```

```
## On branch master
## You have unmerged paths.
##   (fix conflicts and run "git commit")
## 
## Unmerged paths:
##   (use "git add <file>..." to mark resolution)
## 
## 	both added:         bib1.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```


```bash
## `less` printa o conteúdo do arquivo mas `head` limita para 10 linhas.
less bib1.txt | head -10
```

```
## <<<<<<< HEAD
## REPETIÇÃO	VARIEDADE	BLOCO	Y
## =======
## rept	vari	bloc	y
## >>>>>>> feature03
## 1	1	1	20
## 1	2	1	18
## 1	3	2	15
## 1	4	2	16
## 1	5	3	14
```

Então deu conflito e o Git informa que ele deve ser resolvido. Resolver
o conflito aqui significa abrir os arquivos com problema listados no git
status e editar de tal forma a desconflitar. Nas regiões de conflito o
Git sinaliza de forma especial, indicando por divisórias (`<<<<<<<`,
`=======` e `>>>>>>>`) as versões no HEAD (ramo *master*) e no ramos a
ser incorporado (*feature03*). Então vamos resolver o conflito sem
favorecer ninguém, ou seja, vamos encurtar para 4 digitos e manter caixa
alta. Dessa forma o aquivo fica assim.




```bash
## Arquivo depois da edição que resolve o conflito.
head -6 bib1.txt
```

```
## REPT	VARI	BLOC	Y
## 1	1	1	20
## 1	2	1	18
## 1	3	2	15
## 1	4	2	16
## 1	5	3	14
```


```bash
git status
```

```
## On branch master
## You have unmerged paths.
##   (fix conflicts and run "git commit")
## 
## Unmerged paths:
##   (use "git add <file>..." to mark resolution)
## 
## 	both added:         bib1.txt
## 
## no changes added to commit (use "git add" and/or "git commit -a")
```


```bash
git add bib1.txt
git commit -m "Resolve conflito, trunca com caixa alta."
```

```
## [master 52b1f76] Resolve conflito, trunca com caixa alta.
```


```bash
git status
```

```
## On branch master
## nothing to commit, working directory clean
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
## *   52b1f76 (HEAD, master) Resolve conflito, trunca com caixa alta.
## |\  
## | * ef648bb (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
## * | 87e8601 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
## |/  
## *   0bac2be Merge branch 'feature02'
## |\  
## | * 344674a Adiciona aquivo de dados de experimento com rações.
## * | 78a7842 Arquivo sobre copa 2014 celeção brasileira.
## * | ed304f7 Adiciona função R para VIF.
## |/  
## * a2c3f0d Novos argumentos.
## * 41a3225 Adiciona frase do Linux Torvalds.
## * 448b201 Lista de inicial de o porquê usar o Linux.
## * ffc1d12 Cria arquivo com título.
```


```bash
git reflog
```

```
## 52b1f76 HEAD@{0}: commit (merge): Resolve conflito, trunca com caixa alta.
## 87e8601 HEAD@{1}: commit: Arquivo de experimento em BIB. Cabeçalho em caixa alta.
## 0bac2be HEAD@{2}: checkout: moving from feature03 to master
## ef648bb HEAD@{3}: commit: Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
## 0bac2be HEAD@{4}: checkout: moving from master to feature03
## 0bac2be HEAD@{5}: merge feature02: Merge made by the 'recursive' strategy.
## 78a7842 HEAD@{6}: merge feature01: Fast-forward
## ed304f7 HEAD@{7}: checkout: moving from feature01 to master
## 78a7842 HEAD@{8}: commit: Arquivo sobre copa 2014 celeção brasileira.
## ed304f7 HEAD@{9}: checkout: moving from feature02 to feature01
## 344674a HEAD@{10}: checkout: moving from 344674a37125d278b22320956316e7df2e939fdc to feature02
## 344674a HEAD@{11}: commit: Adiciona aquivo de dados de experimento com rações.
## a2c3f0d HEAD@{12}: checkout: moving from master to HEAD@{6}
## ed304f7 HEAD@{13}: checkout: moving from a2c3f0d2a344bf7c680ec67982efca4f5cdf164c to master
## a2c3f0d HEAD@{14}: checkout: moving from master to HEAD@{4}
## ed304f7 HEAD@{15}: merge feature01: Fast-forward
## a2c3f0d HEAD@{16}: checkout: moving from feature01 to master
## ed304f7 HEAD@{17}: commit: Adiciona função R para VIF.
## a2c3f0d HEAD@{18}: checkout: moving from master to feature01
## a2c3f0d HEAD@{19}: commit: Novos argumentos.
## 41a3225 HEAD@{20}: commit: Adiciona frase do Linux Torvalds.
## 448b201 HEAD@{21}: commit: Lista de inicial de o porquê usar o Linux.
## ffc1d12 HEAD@{22}: commit (initial): Cria arquivo com título.
```



