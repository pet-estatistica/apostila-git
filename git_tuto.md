# Tutorial de Git
PET Estatística UFPR  



<!--
## Processar com:
render git_tuto.Rmd
rm -rf meu1repo/ && rm -rf ~/marquina2/meu1repo/ && render git_tuto.Rmd

TODO
  * Remover o downloads. Fazer uma vez para uma pasta /Downloads e só
    copiar de lá. Manter o comandos com wget porque assim outras pessoas
    podem reproduzir.
  * Aprender o que fazer para não precisar dar cd meu1repo em todos os
    chunks.
-->

<img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png"
width=200px align="right" display="block">

<!--==================================================================== -->

****
*Cheat sheets* para Git

  * [Tobias Günther](http://www.git-tower.com/blog/git-cheat-sheet/);
  * [GitHub git cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)
  * [Chris Sevilleja](https://scotch.io/bar-talk/git-cheat-sheet)
  * [Jan Krüger](http://jan-krueger.net/wordpress/wp-content/uploads/2007/09/git-cheat-sheet.pdf)
  * [William Leeks](http://www.cheetyr.com/git)
  * [cheat.errtheblog.com](http://cheat.errtheblog.com/s/git)
  
O modelo de funcionamento do Git:

  * [patrickzahnd.ch](http://www.patrickzahnd.ch/wp-content/uploads/2014/02/git-transport-v1.pdf)
  * [Andrew Petenson](http://ndpsoftware.com/git-cheatsheet.html)

Playlists de tutoriais de Git

  * TODO
  * TODO

****
## O que é o Git?

TODO

****
## Download e instalação

A primeira coisa a fazer é ter instalado os arquivos necessários para o
Git funcionar. Em sistemas Debian e suas variações (Ubuntu, LinuxMint,
...), os pacotes necessários podem ser instalados com comandos que, a
partir dos repositórios de cada distribuição, instalam o Git na sua
máquina.

**Linux**

Em uma sessão de terminal Linux de distribuições Debian (Ubuntu, Mint),
execute o código abaixo.


```sh
## Adicione o ppa para ter a versão mais recente do Git. Descomente e
## rode essas duas linhas de comando para isso.
## sudo add-apt-repository ppa:git-core/ppa
## sudo apt-get update

sudo apt-get install git git-core git-man git-gui git-doc \
    ssh openssh-server openssh-client
git --version

## Ferramentas complementares.
sudo apt-get install gitk meld
```

Usuários de Linux baseados no Arch instalam de uam forma ligeiramente
diferente.


```sh
pacman -S git openssh meld
git --version
```

O `ssh` e `openssh-*` são necessários para a comunicação entre sua
máquina e o servidor do GitHub ou GitLab. Iremos configurar repositórios
remotos em uma outra sessão. O Git também pode ser instalado em ou
sistemas operacionais. Visite [Installing-Git][] e siga as
instruções. Os arquivos de instalação podem ser baixados do endereço
<http://git-scm.com>.

**Windows**

Usuários Windows devem visitar <https://git-for-windows.github.io/>,
baixar e instalar. Essa instalação do Git traz o [**Git BASH**][] que é como
um terminal do (Li|U)nix, a [**Git GUI**][] que é uma interface para
trabalhar com Git e [**Shell Integration**][] que são ações disponíveis no
menu aberto pelo botão direto mouse. Além disso, segundo o que consta é
que essa instalação tras também a [**Gitk**][], uma interface para navegação
no histórico.

[Meld](http://meldmerge.org/) é um assistente de comparação de arquivos
(*file diff*). Ele é muito útil como ferramenta para resolver conflitos
de merge (*mergetool*). No entanto, não é obrigatório ter.

****
## Configurando perfil

Estas configurações precisam ser feitas apenas uma vez, e servem para
determinar algumas opções globais do Git.

Os comandos abaixo vão configurar o nome de usuário e email. Fique
tranquilo que o Git não vai te enviar email, isso é apenas informação
que ficará associada ao trabalho que você desenvolver de modo a permitir
que os colaborados/gestores do projeto identifiquem suas contribuições e
possam entrar em contato, se necessário (principalmente se você fizer
aqui de errado). Mesmo que você nunca venha a trabalhar em equipe,
apenas localmente, é importante fornecer nome e email. Se trabalhar de
duas máquinas diferentes, você pode indentificar no nome de usuário.


```sh
## Configurações do Git do Batman.
git config --global user.name "Knight Rider"
git config --global user.email "batman@justiceleague.org"

## Configurações do Git do Superman.
git config --global user.name "Kal-El"
git config --global user.email "superman@justiceleague.org"
```

O `--global` dessa instrução significa que o que for definido vai valer
para todo projeto Git da máquina. É possível fazer definições para cada
projeto, ou seja, não globais. Portanto, você pode trabalhar com nomes
ou emails diferentes para cada projeto. É possível também criar `alias`
para algumas intruções Git. Embora elas não sejam tão longas, no uso
contínuo pode valer a pena. Visite:

  * [Setting up a repository][]
  * [Customizing Git - Git Configuration][]

Além disso podemos definir um editor de texto padrão para escrever as
mensagens de *commits*. Por padrão, esse editor é o `$EDITOR` do seu
shell. (Essa etapa pode ser pulada a princípio, como veremos mais pra
frente). Esse editor não precisa ser necessariamente o mesmo editor que
você usa para escrever [texto, código]. No meu caso uso o Emacs, mas
para essa tarefa prefiro o vim por ser um editor embutido, e que não vai
carregar uma interface gráfica desnecessariamente quando for preciso
escrever uma mensagem de *commit*. Portanto, aqui pode-se deixar espaço
para o `vim`.


```sh
git config --global core.editor vim
```

O Emacs também pode ser carregado embutido no terminal (sem usar o X),
usando a opção `emacs -nw` (de *no window*) na sua inicialização.

No Linux, as informações acima passadas ficam salvas em um arquivo na
home do usuário chamado `.gitconfig`. Quando não se usa o `--global`, as
definições ficam salvas dentro do próprio do projeto. Eis o conteúdo do
arquivo de configuração do Batman.


```bash
less ~/.gitconfig
```

```
[user]
    name = Knight Rider
    email = batman@justiceleague.org
[merge]
    tool = meld
```

No caso dele, além de nome e email, tem que o `meld` que é a ferramenta
de merge definida como padrão. Para conseguir isso você precisa definir
como fez com os demais ([how-to-set-meld-as-git-mergetool][]).


```bash
git config --global merge.tool meld
```

**Avançado**: Para usuários Linux que apreciam o nível de customização
que o Linux oferece (como o Batman e nós), é possível configurar o
prompt do terminal para mostrar a informação do ramo, usuário, etc. Essa
informação estampada facilita um bocado, principalmente em projetos
grandes. Visite:

  * [Eranga Bandara](https://coderwall.com/p/fasnya/add-git-branch-name-to-bash-prompt)
  * [Michael Hoffman](http://code-worrier.com/blog/git-branch-in-bash-prompt/)

****

## Criar um projeto versionado

### Instruções do Git

Já temos o Git devidamente e com credenciais (nome e email) e
configurações aplicadas. Vamos então ver como o sistema de controle de
versão acontece.

Todas as instruções do Git são sinalizadas por começar com `git` seguido
da instrução/comando e seus argumentos complementares, se
existirem/necessários.


```bash
## Padrão de instruções Git.
git <instrução> <complementos ...>
```

Os comandos abaixo revelam tudo o Git tem, embora dizer o que ele tem
não signifique nada diante do que ele pode fazer com o que tem.


```bash
## Ajuda resumida do Git, principais comandos com descrição.
git help -a
```

```
bash: line 0: cd: meu1repo: No such file or directory
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

available git commands in '/usr/lib/git-core'

  add                       merge-octopus
  add--interactive          merge-one-file
  am                        merge-ours
  annotate                  merge-recursive
  apply                     merge-resolve
  archive                   merge-subtree
  bisect                    merge-tree
  bisect--helper            mergetool
  blame                     mktag
  branch                    mktree
  bundle                    mv
  cat-file                  name-rev
  check-attr                notes
  check-ignore              pack-objects
  check-mailmap             pack-redundant
  check-ref-format          pack-refs
  checkout                  patch-id
  checkout-index            prune
  cherry                    prune-packed
  cherry-pick               pull
  citool                    push
  clean                     quiltimport
  clone                     read-tree
  column                    rebase
  commit                    receive-pack
  commit-tree               reflog
  config                    relink
  count-objects             remote
  credential                remote-ext
  credential-cache          remote-fd
  credential-cache--daemon  remote-ftp
  credential-store          remote-ftps
  daemon                    remote-http
  describe                  remote-https
  diff                      remote-testsvn
  diff-files                repack
  diff-index                replace
  diff-tree                 request-pull
  difftool                  rerere
  difftool--helper          reset
  fast-export               rev-list
  fast-import               rev-parse
  fetch                     revert
  fetch-pack                rm
  filter-branch             send-pack
  fmt-merge-msg             sh-i18n--envsubst
  for-each-ref              shell
  format-patch              shortlog
  fsck                      show
  fsck-objects              show-branch
  gc                        show-index
  get-tar-commit-id         show-ref
  grep                      stage
  gui                       stash
  gui--askpass              status
  hash-object               stripspace
  help                      submodule
  http-backend              subtree
  http-fetch                symbolic-ref
  http-push                 tag
  imap-send                 unpack-file
  index-pack                unpack-objects
  init                      update-index
  init-db                   update-ref
  instaweb                  update-server-info
  interpret-trailers        upload-archive
  log                       upload-pack
  ls-files                  var
  ls-remote                 verify-commit
  ls-tree                   verify-pack
  mailinfo                  verify-tag
  mailsplit                 web--browse
  merge                     whatchanged
  merge-base                worktree
  merge-file                write-tree
  merge-index

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```


```bash
## Lista de todos os comandos disponíveis.
git help -a
```

```
bash: line 0: cd: meu1repo: No such file or directory
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

available git commands in '/usr/lib/git-core'

  add                       merge-octopus
  add--interactive          merge-one-file
  am                        merge-ours
  annotate                  merge-recursive
  apply                     merge-resolve
  archive                   merge-subtree
  bisect                    merge-tree
  bisect--helper            mergetool
  blame                     mktag
  branch                    mktree
  bundle                    mv
  cat-file                  name-rev
  check-attr                notes
  check-ignore              pack-objects
  check-mailmap             pack-redundant
  check-ref-format          pack-refs
  checkout                  patch-id
  checkout-index            prune
  cherry                    prune-packed
  cherry-pick               pull
  citool                    push
  clean                     quiltimport
  clone                     read-tree
  column                    rebase
  commit                    receive-pack
  commit-tree               reflog
  config                    relink
  count-objects             remote
  credential                remote-ext
  credential-cache          remote-fd
  credential-cache--daemon  remote-ftp
  credential-store          remote-ftps
  daemon                    remote-http
  describe                  remote-https
  diff                      remote-testsvn
  diff-files                repack
  diff-index                replace
  diff-tree                 request-pull
  difftool                  rerere
  difftool--helper          reset
  fast-export               rev-list
  fast-import               rev-parse
  fetch                     revert
  fetch-pack                rm
  filter-branch             send-pack
  fmt-merge-msg             sh-i18n--envsubst
  for-each-ref              shell
  format-patch              shortlog
  fsck                      show
  fsck-objects              show-branch
  gc                        show-index
  get-tar-commit-id         show-ref
  grep                      stage
  gui                       stash
  gui--askpass              status
  hash-object               stripspace
  help                      submodule
  http-backend              subtree
  http-fetch                symbolic-ref
  http-push                 tag
  imap-send                 unpack-file
  index-pack                unpack-objects
  init                      update-index
  init-db                   update-ref
  instaweb                  update-server-info
  interpret-trailers        upload-archive
  log                       upload-pack
  ls-files                  var
  ls-remote                 verify-commit
  ls-tree                   verify-pack
  mailinfo                  verify-tag
  mailsplit                 web--browse
  merge                     whatchanged
  merge-base                worktree
  merge-file                write-tree
  merge-index

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```

### Criar um diretório para o projeto Git

Vamos criar um diretório vazio para começarmos um projeto. Também se
pode começar de um diretório que já tenha arquivos e subdiretórios. Você
pode fazer isso com seu *file manager* padrão que no Ubuntu é o
[`Nautilus`](https://wiki.gnome.org/action/show/Apps/Nautilus), no Mint
é o `Nemo`.

**NOTA**: o desenvolvimento do Nemo é feito com Git e está disponível no
GitHub: [linuxmint/nemo][].

Nesse tutorial, as instruções serão todas feitas no terminal mesmo que
existam alternativas gráficas para as mesmas. Isso enfatiza no que está
sendo feito além do fato de que no terminal todos devem ter os mesmos
recursos e os comandos irão produzir os mesmos resultados, o que faz
esse tutorial algo reproduzível. Se você considera que uma ferramenta
gráfica é mais confortável ou produtiva, sinta-se à vontade para
aprendê-la e usá-la.


```bash
## Cria diretório (make directory).
mkdir meu1repo

## Entra no diretório (change directory).
cd meu1repo
```

Antes de iniciarmos o repositório, vamos só verificar o cadastro. Se
você já usa o Git ou fez os procedimento apresentados na primeira
sessão, o comando abaixo vai retornar o nome e email usados e alguns
definições adicionais, caso existam. Em caso de ainda não ter
configurado o seu Git, informe o nome e email conforme apresentado na
sessão anterior.


```bash
## Mostra as informações/definições do usuário.
git config --list
```

```
user.name=Walmes Zeviani
user.email=walmeszeviani@gmail.com
merge.tool=meld
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=git@gitlab.c3sl.ufpr.br:pet-estatistica/git-tutorial.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master
```

Temos um diretório destinado ao projeto que será mantido sobre
versionamento, então vamos iniciar um repositório Git nele.


```bash
## Inicia um repositório sob versionamento Git.
git init
```

```
Initialized empty Git repository in /home/walmes/GitLab/git-tutorial/meu1repo/.git/
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
.
└── .git
    ├── branches
    ├── config
    ├── description
    ├── HEAD
    ├── hooks
    │   ├── applypatch-msg.sample
    │   ├── commit-msg.sample
    │   ├── post-update.sample
    │   ├── pre-applypatch.sample
    │   ├── pre-commit.sample
    │   ├── prepare-commit-msg.sample
    │   ├── pre-push.sample
    │   ├── pre-rebase.sample
    │   └── update.sample
    ├── info
    │   └── exclude
    ├── objects
    │   ├── info
    │   └── pack
    └── refs
        ├── heads
        └── tags

10 directories, 13 files
```

**NOTA**: o `tree` é um programa instalado a parte (*third party
software*) que retorna arte ASCII representado a estrutura de
diretórios. Se você usa distribuição Debian, instale com `sudo apt-get
install tree`. Windows: [tree][].

Vamos começar da maneira mais simples: criando um arquivo com uma linha
de texto apenas. Bem, vale avisar que ao longo desse tutorial, os
arquivos serão sempre bem pequenos e dificilmente realistas, mas como o
enfoque está no funcionamento, não haverá prejuízo.

Vamos criar o arquivo com conteúdo também pelo terminal. Se você
preferir, abra eu editor de texto favorito (Emacs, Gedit, Geany,
RStudio, etc) e faça algo mais criativo.


```bash
## Cria um arquivo com uma linha de conteúdo.
echo "Meu primeiro repositório Git" > README.txt

## Lista os arquivos do diretório.
tree
```

```
.
└── README.txt

0 directories, 1 file
```

O Git está "atento" a tudo que acontece nesse diretório. Ao criarmos o
arquivo e pedirmos a situação (*status*), ele indica que existe um
arquivo não restreado (*untracked*) no diretório. Inclusive sugere uma
ação que seria adicionar o aquivo (*add*). Se o seu sistema operacional
está em português, parte dos outputs do Git podem estar traduzidos.


```bash
## Reconhecimento do Git sobre aquivo criado.
git status
```

```
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.txt

nothing added to commit but untracked files present (use "git add" to track)
```

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
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.txt
```

O arquivo `README.txt` já é visto pelo Git como um arquivo com o qual
ele deve se "preocupar", pois está sob versionamento. Vamos agora fazer
um registro definitivo sobre o estado desse arquivo (*commit*). É de
fundamental importância que a mensagem de notificação, ou mensagem de
*commit*, reflita as moficações feitas. São as mensagens que serão
consultadas quando você precisar desfazer/voltar. Ela deve ser curta (<=
72 caracteres) e ao mesmo tempo informativa. A minha primeira mensagem
não será, todavia.


```bash
## Registro de versão.
git commit -m "Cria arquivo com título."
```

```
[master (root-commit) 3bed6b0] Cria arquivo com título.
 1 file changed, 1 insertion(+)
 create mode 100644 README.txt
```

**NOTA**: Sobre mensagens de *commit* e trabalho colaborativo em Git
existem algumas boas práticas que devem ser seguidas. Visite:
[Git contributing guide][].

O retorno da instrução de *commit* indica o número de arquivos incluídos
no *commit* e o número de inserções e deleções de linhas. O mais
importante está na primeira linha que informa o ramo de trabalho atual
(*branch*) e o *sha1* do *commit*. O *sha1* é uma sequência hexadecimal
de 40 digitos que representa unicamente o *commit*, então são $16^40$
possibilidades!. É por meio do *sha1* que podemos retroceder o
projeto. São mostrados apenas os 7 primeiros digitos porque são
suficientes para diferenciar *commits* dentro até mesmo de projetos
moderados ou grandes. Visite: [sha1-size][].

Vamos criar mais arquivos e acrescentar conteúdo ao já rastreado pelo
Git para percebermos o funcionamento. Escrever uma lista de razões para
usar o Linux. Deixei a lista curta poder ampliar no futuro e com erros
de português para corrigir depois.

<!--
Frases do Linus Torvalds.
http://www.diolinux.com.br/2015/04/13-frases-epicas-de-linus-torvalds.html
-->


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
Meu primeiro repositório Git

A filosofia do Linux é 'Ria na face do perigo'.
Ôpa. Errado. 'Faça você mesmo'. É, é essa.
                            -- Lunus Torvalds
```


```bash
## Mostra o conteúdo do arquivo.
less porqueLinux.txt
```

```
Por que usar o Linux?

* É livre
* É seguro
* É customizavel
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
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	porqueLinux.txt

no changes added to commit (use "git add" and/or "git commit -a")
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
commit 3bed6b0935b7bccbf5e213a80d5f2648457cb564
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Tue Sep 22 18:22:48 2015 -0300

    Cria arquivo com título.
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
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
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
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   porqueLinux.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.txt
```


```bash
## Mensagem que registra as modificações adicionadas.
git commit -m "Lista de inicial de o porquê usar o Linux."
```

```
[master eda2e0a] Lista de inicial de o porquê usar o Linux.
 1 file changed, 5 insertions(+)
 create mode 100644 porqueLinux.txt
```


```bash
git status
```

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.txt

no changes added to commit (use "git add" and/or "git commit -a")
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
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.txt
```


```bash
## Atribui mensagem de notificação.
git commit -m "Adiciona frase do Linux Torvalds."
```

```
[master 3e3b4d3] Adiciona frase do Linux Torvalds.
 1 file changed, 4 insertions(+)
```

Agora temos 3 *commits* e o *log* apresenta os *sha1* e as mensagens
correspondentes aos mesmos. Com `--oneline` resumimos o *output* mostrando
apenas o *sha1* e a mensagem de *commit*.


```bash
git log --oneline
```

```
3e3b4d3 Adiciona frase do Linux Torvalds.
eda2e0a Lista de inicial de o porquê usar o Linux.
3bed6b0 Cria arquivo com título.
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
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
```

Agora inspecionado uma distância de 2 *commits* a partir do último. Aqui
tem-se os dois arquivos envolvidos nesse intervalo de 2 *commits*. Com
`--name-only` retorna-se só o nome dos arquivos.


```bash
git diff HEAD@{2} HEAD@{0}
```

```
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
diff --git a/porqueLinux.txt b/porqueLinux.txt
new file mode 100644
index 0000000..8ecdfda
--- /dev/null
+++ b/porqueLinux.txt
@@ -0,0 +1,5 @@
+Por que usar o Linux?
+
+* É livre
+* É seguro
+* É customizavel
```


```bash
git diff --name-only HEAD@{2} HEAD@{0}
```

```
README.txt
porqueLinux.txt
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
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   porqueLinux.txt

no changes added to commit (use "git add" and/or "git commit -a")
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
Por que usar o Linux?

* É livre
* É seguro
* É customizável
* Tem repositórios de software
* Atualização constante
* Desempenho
```


```bash
## Abandona modificações feitas presentes no arquivo.
git checkout -- porqueLinux.txt
```


```bash
less porqueLinux.txt
```

```
Por que usar o Linux?

* É livre
* É seguro
* É customizavel
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
On branch master
nothing to commit, working directory clean
```

Vamos seguir com as modificações em `porqueLinux.txt` que corrigem o
texto e acrescentam itens novos.




```bash
git status
```

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   porqueLinux.txt

no changes added to commit (use "git add" and/or "git commit -a")
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
diff --git a/porqueLinux.txt b/porqueLinux.txt
index 8ecdfda..8747d1e 100644
--- a/porqueLinux.txt
+++ b/porqueLinux.txt
@@ -2,4 +2,7 @@ Por que usar o Linux?
 
 * É livre
 * É seguro
-* É customizavel
+* É customizável
+* Tem repositórios de software
+* Atualização constante
+* Desempenho
```


```bash
## Último commit vs dois ancestrais, usando ~.
git diff HEAD~1 HEAD~0
```

```
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
```


```bash
## Último commit vs seu ancestral, usando @{}.
git diff HEAD@{1} HEAD@{0}
```

```
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
```


```bash
## Último commit vs dois ancestrais.
## git diff HEAD~2 HEAD~0
git diff HEAD@{2} HEAD@{0}
```

```
diff --git a/README.txt b/README.txt
index 07d3585..d0af1d3 100644
--- a/README.txt
+++ b/README.txt
@@ -1 +1,5 @@
 Meu primeiro repositório Git
+
+A filosofia do Linux é 'Ria na face do perigo'.
+Ôpa. Errado. 'Faça você mesmo'. É, é essa.
+                            -- Lunus Torvalds
diff --git a/porqueLinux.txt b/porqueLinux.txt
new file mode 100644
index 0000000..8ecdfda
--- /dev/null
+++ b/porqueLinux.txt
@@ -0,0 +1,5 @@
+Por que usar o Linux?
+
+* É livre
+* É seguro
+* É customizavel
```

Para ficar claro daqui em diante, você pode ao invés de pedir `log`,
pedir o `reflog` que incluí as referências em termos da sequência do
mais rencente para os seus ancestrais.


```bash
## Mostra referências para commits os ancentrais.
git reflog
```

```
3e3b4d3 HEAD@{0}: commit: Adiciona frase do Linux Torvalds.
eda2e0a HEAD@{1}: commit: Lista de inicial de o porquê usar o Linux.
3bed6b0 HEAD@{2}: commit (initial): Cria arquivo com título.
```


```bash
## Adiciona e commita.
git add porqueLinux.txt
git commit -m "Novos argumentos."
```

```
[master d5f7cdd] Novos argumentos.
 1 file changed, 4 insertions(+), 1 deletion(-)
```

O Git permite um nível de rastreabilidade bem fino. Veja por exemplo que
é possível saber quem modificou e quando cada linha do arquivo e qual o
correspondente *sha1* do *commit*.


```bash
## Mostra quem, onde e o que fez em cada arquivo.
git blame README.txt
```

```
^3bed6b0 (Walmes Zeviani 2015-09-22 18:22:48 -0300 1) Meu primeiro repositório Git
3e3b4d33 (Walmes Zeviani 2015-09-22 18:22:48 -0300 2) 
3e3b4d33 (Walmes Zeviani 2015-09-22 18:22:48 -0300 3) A filosofia do Linux é 'Ria na face do perigo'.
3e3b4d33 (Walmes Zeviani 2015-09-22 18:22:48 -0300 4) Ôpa. Errado. 'Faça você mesmo'. É, é essa.
3e3b4d33 (Walmes Zeviani 2015-09-22 18:22:48 -0300 5)                             -- Lunus Torvalds
```

****
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
* master
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
  feature01
* master
```


```bash
## Muda o HEAD de ramo.
git checkout feature01
```

```
Switched to branch 'feature01'
```


```bash
## Situação no novo ramo.
git status
```

```
On branch feature01
nothing to commit, working directory clean
```


```bash
## Histórico de commits.
git log --oneline
```

```
d5f7cdd Novos argumentos.
3e3b4d3 Adiciona frase do Linux Torvalds.
eda2e0a Lista de inicial de o porquê usar o Linux.
3bed6b0 Cria arquivo com título.
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
--2015-09-22 18:22:48--  http://people.ufpr.br/~giolo/CE071/Exemplos/vif.R
Resolving people.ufpr.br (people.ufpr.br)... 200.17.203.30, 2801:82:8020:0:8377:0:100:20
Connecting to people.ufpr.br (people.ufpr.br)|200.17.203.30|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 560
Saving to: ‘vif.R’

     0K                                                       100% 64,0M=0s

2015-09-22 18:22:48 (64,0 MB/s) - ‘vif.R’ saved [560/560]
```


```bash
## Situação do repositório após o download.
git status
```

```
On branch feature01
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	vif.R

nothing added to commit but untracked files present (use "git add" to track)
```


```bash
git add vif.R
git commit -m "Adiciona função R para VIF."
```

```
[feature01 71c72b3] Adiciona função R para VIF.
 1 file changed, 20 insertions(+)
 create mode 100644 vif.R
```


```bash
## Estrutura do diretório.
tree
```

```
.
├── porqueLinux.txt
├── README.txt
└── vif.R

0 directories, 3 files
```


```bash
## Histórico de commits.
git reflog
```

```
71c72b3 HEAD@{0}: commit: Adiciona função R para VIF.
d5f7cdd HEAD@{1}: checkout: moving from master to feature01
d5f7cdd HEAD@{2}: commit: Novos argumentos.
3e3b4d3 HEAD@{3}: commit: Adiciona frase do Linux Torvalds.
eda2e0a HEAD@{4}: commit: Lista de inicial de o porquê usar o Linux.
3bed6b0 HEAD@{5}: commit (initial): Cria arquivo com título.
```


```bash
git status
```

```
On branch feature01
nothing to commit, working directory clean
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
Switched to branch 'master'
```


```bash
## Estrutura do diretório.
tree
```

```
.
├── porqueLinux.txt
└── README.txt

0 directories, 2 files
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
diff --git a/vif.R b/vif.R
new file mode 100644
index 0000000..a114969
--- /dev/null
+++ b/vif.R
@@ -0,0 +1,20 @@
+vif<-function (obj, digits = 5) {
+    Qr <- obj$qr
+    if (is.null(obj$terms) || is.null(Qr)) 
+        stop("invalid 'lm' object:  no terms or qr component")
+    tt <- terms(obj)
+    hasintercept <- attr(tt, "intercept") > 0
+    p <- Qr$rank
+    if (hasintercept) 
+        p1 <- 2:p
+    else p1 <- 1:p
+    R <- Qr$qr[p1, p1, drop = FALSE]
+    if (length(p1) > 1) 
+        R[row(R) > col(R)] <- 0
+    Rinv <- qr.solve(R)
+    vv <- apply(Rinv, 1, function(x) sum(x^2))
+    ss <- apply(R, 2, function(x) sum(x^2))
+    vif <- ss * vv
+    signif(vif, digits)
+   }
+
```


```bash
## Mostra só os arquivos modificados.
git diff --name-only master feature01
```

```
vif.R
```

Como você já havia antecipado, a única diferença entre os ramos `master`
e `feature01` é o arquivo `vif.R`. Agora é só pedir o `git merge`.


```bash
## Mesclando as modificações em feature01 no master.
git merge feature01 master
```

```
Updating d5f7cdd..71c72b3
Fast-forward
 vif.R | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)
 create mode 100644 vif.R
```


```bash
git log --oneline
```

```
71c72b3 Adiciona função R para VIF.
d5f7cdd Novos argumentos.
3e3b4d3 Adiciona frase do Linux Torvalds.
eda2e0a Lista de inicial de o porquê usar o Linux.
3bed6b0 Cria arquivo com título.
```

É possível criar um ramo a partir de um *commit* ancestral ao atual. Isso
é extremamente útil para resolver os bugs. Vamos fazer um segundo ramo a
partir do *commit* anterior a inclusão do arquivo R.


```bash
## Referencias aos commits.
git reflog
```

```
71c72b3 HEAD@{0}: merge feature01: Fast-forward
d5f7cdd HEAD@{1}: checkout: moving from feature01 to master
71c72b3 HEAD@{2}: commit: Adiciona função R para VIF.
d5f7cdd HEAD@{3}: checkout: moving from master to feature01
d5f7cdd HEAD@{4}: commit: Novos argumentos.
3e3b4d3 HEAD@{5}: commit: Adiciona frase do Linux Torvalds.
eda2e0a HEAD@{6}: commit: Lista de inicial de o porquê usar o Linux.
3bed6b0 HEAD@{7}: commit (initial): Cria arquivo com título.
```


```bash
## Volta para antes do arquivo de baixar o vif.R.
git checkout HEAD@{4}
```

```
Note: checking out 'HEAD@{4}'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at d5f7cdd... Novos argumentos.
```


```bash
## Qual a situação.
git status
```

```
HEAD detached at d5f7cdd
nothing to commit, working directory clean
```


```bash
## O histório existente nesse ponto.
git log --name-only --oneline
```

```
d5f7cdd Novos argumentos.
porqueLinux.txt
3e3b4d3 Adiciona frase do Linux Torvalds.
README.txt
eda2e0a Lista de inicial de o porquê usar o Linux.
porqueLinux.txt
3bed6b0 Cria arquivo com título.
README.txt
```

Já que o *commit* mais recente dessa história aponta para o arquivo
compras, vamos checar o seu conteúdo apenas por medida de segurança.


```bash
## Mostra o conteúdo do arquivo.
less porqueLinux.txt
```

```
Por que usar o Linux?

* É livre
* É seguro
* É customizável
* Tem repositórios de software
* Atualização constante
* Desempenho
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
* (HEAD detached at d5f7cdd)
  feature01
  master
```

Se não fizemos nenhuma modificação, voltar é bem simples. Se
modificações foram feitas é necessário saber se precisam ser mantidas e
onde ou se devem ser descartadas.


```bash
## Volta para o presente.
git checkout master
```

```
Previous HEAD position was d5f7cdd... Novos argumentos.
Switched to branch 'master'
```


```bash
git status
```

```
On branch master
nothing to commit, working directory clean
```


```bash
git log --oneline
```

```
71c72b3 Adiciona função R para VIF.
d5f7cdd Novos argumentos.
3e3b4d3 Adiciona frase do Linux Torvalds.
eda2e0a Lista de inicial de o porquê usar o Linux.
3bed6b0 Cria arquivo com título.
```


```bash
## Fenda no tempo fechada. Sem sinal do detached HEAD.
git branch
```

```
  feature01
* master
```


```bash
## Sinal do passeio no tempo.
git reflog
```

```
71c72b3 HEAD@{0}: checkout: moving from d5f7cdd48a41d788afb8114ae56d84ce81204261 to master
d5f7cdd HEAD@{1}: checkout: moving from master to HEAD@{4}
71c72b3 HEAD@{2}: merge feature01: Fast-forward
d5f7cdd HEAD@{3}: checkout: moving from feature01 to master
71c72b3 HEAD@{4}: commit: Adiciona função R para VIF.
d5f7cdd HEAD@{5}: checkout: moving from master to feature01
d5f7cdd HEAD@{6}: commit: Novos argumentos.
3e3b4d3 HEAD@{7}: commit: Adiciona frase do Linux Torvalds.
eda2e0a HEAD@{8}: commit: Lista de inicial de o porquê usar o Linux.
3bed6b0 HEAD@{9}: commit (initial): Cria arquivo com título.
```

Vamos começar a ser ousados. Vamos voltar no passado, adicionar um
arquivo, commitar e ver o que acontece, como o histórico é representado.


```bash
## Volta no tempo, após commit que aumenta porqueLinux.txt.
git checkout HEAD@{6}
```

```
Note: checking out 'HEAD@{6}'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at d5f7cdd... Novos argumentos.
```


```bash
## Baixa arquivo de dados da internet.
wget 'http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt'
```

```
--2015-09-22 18:22:49--  http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... 200.17.213.49
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|200.17.213.49|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 217 [text/plain]
Saving to: ‘pimentel_racoes.txt’

     0K                                                       100% 12,1M=0s

2015-09-22 18:22:50 (12,1 MB/s) - ‘pimentel_racoes.txt’ saved [217/217]
```


```bash
git status
```

```
HEAD detached at d5f7cdd
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	pimentel_racoes.txt

nothing added to commit but untracked files present (use "git add" to track)
```


```bash
## Adiciona para registrar a inclusão do arquivo.
git add pimentel_racoes.txt
git commit -m "Adiciona aquivo de dados de experimento com rações."
```

```
[detached HEAD 278d3f1] Adiciona aquivo de dados de experimento com rações.
 1 file changed, 24 insertions(+)
 create mode 100644 pimentel_racoes.txt
```


```bash
git status
```

```
HEAD detached from d5f7cdd
nothing to commit, working directory clean
```


```bash
## Log num formato gráfico ASCII para mostrar o novo ramo.
git log --graph --oneline --decorate --date=relative --all
```

```
* 278d3f1 (HEAD) Adiciona aquivo de dados de experimento com rações.
| * 71c72b3 (master, feature01) Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
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
* (HEAD detached from d5f7cdd)
  feature01
  master
```


```bash
## Um novo ramo a partir do atual HEAD.
git checkout -b feature02
```

```
Switched to a new branch 'feature02'
```


```bash
git branch
```

```
  feature01
* feature02
  master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 278d3f1 (HEAD -> feature02) Adiciona aquivo de dados de experimento com rações.
| * 71c72b3 (master, feature01) Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
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
Switched to branch 'feature01'
```


```bash
wget 'http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt'
```

```
--2015-09-22 18:22:50--  http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... 200.17.213.49
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|200.17.213.49|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1254 (1,2K) [text/plain]
Saving to: ‘brasilCopa2014.txt’

     0K .                                                     100% 92,0M=0s

2015-09-22 18:22:50 (92,0 MB/s) - ‘brasilCopa2014.txt’ saved [1254/1254]
```


```bash
git add brasilCopa2014.txt
git commit -m "Arquivo sobre copa 2014 celeção brasileira."
```

```
[feature01 19db415] Arquivo sobre copa 2014 celeção brasileira.
 1 file changed, 22 insertions(+)
 create mode 100644 brasilCopa2014.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 19db415 (HEAD -> feature01) Arquivo sobre copa 2014 celeção brasileira.
* 71c72b3 (master) Adiciona função R para VIF.
| * 278d3f1 (feature02) Adiciona aquivo de dados de experimento com rações.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
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
Switched to branch 'master'
```


```bash
## Mescla o feature01.
git merge feature01 master
```

```
Updating 71c72b3..19db415
Fast-forward
 brasilCopa2014.txt | 22 ++++++++++++++++++++++
 1 file changed, 22 insertions(+)
 create mode 100644 brasilCopa2014.txt
```


```bash
## Mescla o feature02.
git merge feature02 master
```

```
Merge made by the 'recursive' strategy.
 pimentel_racoes.txt | 24 ++++++++++++++++++++++++
 1 file changed, 24 insertions(+)
 create mode 100644 pimentel_racoes.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   4a44483 (HEAD -> master) Merge branch 'feature02'
|\  
| * 278d3f1 (feature02) Adiciona aquivo de dados de experimento com rações.
* | 19db415 (feature01) Arquivo sobre copa 2014 celeção brasileira.
* | 71c72b3 Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
```


```bash
tree
```

```
.
├── brasilCopa2014.txt
├── pimentel_racoes.txt
├── porqueLinux.txt
├── README.txt
└── vif.R

0 directories, 5 files
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
Deleted branch feature01 (was 19db415).
Deleted branch feature02 (was 278d3f1).
* master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   4a44483 (HEAD -> master) Merge branch 'feature02'
|\  
| * 278d3f1 Adiciona aquivo de dados de experimento com rações.
* | 19db415 Arquivo sobre copa 2014 celeção brasileira.
* | 71c72b3 Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
```

Agora vou criar um novo ramo, adicionar um arquivo e encurtar o nome das
colunas no cabeçalho.


```bash
## Muda para um ramo criado na hora.
git checkout -b feature03
```

```
Switched to a new branch 'feature03'
```


```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/bib1.txt'
```

```
--2015-09-22 18:22:51--  http://www.leg.ufpr.br/~walmes/data/bib1.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... 200.17.213.49
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|200.17.213.49|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 535 [text/plain]
Saving to: ‘bib1.txt’

     0K                                                       100% 54,3M=0s

2015-09-22 18:22:51 (54,3 MB/s) - ‘bib1.txt’ saved [535/535]
```


```bash
## Mostra as 4 primeiras linhas.
head -4 bib1.txt
```

```
repetição	variedade	bloco	y
1	1	1	20
1	2	1	18
1	3	2	15
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
rept	vari	bloc	y
1	1	1	20
1	2	1	18
1	3	2	15
```


```bash
git add bib1.txt
git commit -m "Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos."
```

```
[feature03 09dbf4e] Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
 1 file changed, 58 insertions(+)
 create mode 100644 bib1.txt
```

Baixamos e modificamos o arquivo. Adicionamos e fizemos o registro das
modificações. Agora vamos voltar ao *master* e baixar o arquivo também,
fazendo de conta que é outra pessoa trabalhando no mesmo projeto, mas
essa pessoa vai passar a cabeçalho para caixa alta.


```bash
git checkout master
```

```
Switched to branch 'master'
```


```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/bib1.txt'
```

```
--2015-09-22 18:22:51--  http://www.leg.ufpr.br/~walmes/data/bib1.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... 200.17.213.49
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|200.17.213.49|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 535 [text/plain]
Saving to: ‘bib1.txt’

     0K                                                       100% 45,3M=0s

2015-09-22 18:22:51 (45,3 MB/s) - ‘bib1.txt’ saved [535/535]
```

Ao encurtar o nome para quatro dígitos, fica assim.


```bash
## Substitui o conteúdo da primeira linha pelo mesmo em caixa alta. Faça
## isso no seu editor de texto de preferido.
sed -i '1s/.*/\U&/' bib1.txt
head -4 bib1.txt
```

```
REPETIÇÃO	VARIEDADE	BLOCO	Y
1	1	1	20
1	2	1	18
1	3	2	15
```


```bash
git add bib1.txt
git commit -m "Arquivo de experimento em BIB. Cabeçalho em caixa alta."
```

```
[master fc86f72] Arquivo de experimento em BIB. Cabeçalho em caixa alta.
 1 file changed, 58 insertions(+)
 create mode 100644 bib1.txt
```


```bash
git diff master feature03
```

```
diff --git a/bib1.txt b/bib1.txt
index a8dfaa6..b5f5963 100644
--- a/bib1.txt
+++ b/bib1.txt
@@ -1,4 +1,4 @@
-REPETIÇÃO	VARIEDADE	BLOCO	Y
+rept	vari	bloc	y
 1	1	1	20
 1	2	1	18
 1	3	2	15
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 09dbf4e (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
| * fc86f72 (HEAD -> master) Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   4a44483 Merge branch 'feature02'
|\  
| * 278d3f1 Adiciona aquivo de dados de experimento com rações.
* | 19db415 Arquivo sobre copa 2014 celeção brasileira.
* | 71c72b3 Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
```


```bash
## Dá mensagem de erro que informa o conflito.
git merge feature03 master
```


```
Auto-merging bib1.txt
CONFLICT (add/add): Merge conflict in bib1.txt
Automatic merge failed; fix conflicts and then commit the result.
```


```bash
git status
```

```
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both added:      bib1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```


```bash
less bib1.txt
```

```
<<<<<<< HEAD
REPETIÇÃO	VARIEDADE	BLOCO	Y
=======
rept	vari	bloc	y
>>>>>>> feature03
1	1	1	20
1	2	1	18
1	3	2	15
1	4	2	16
1	5	3	14
1	6	3	15
1	7	4	16
1	8	4	18
2	1	1	24
2	3	1	18
2	2	2	25
2	8	2	19
2	4	3	13
2	5	3	16
2	6	4	12
2	7	4	16
3	1	1	23
3	4	1	17
3	2	2	26
3	7	2	18
3	3	3	15
3	6	3	17
3	5	4	13
3	8	4	16
4	1	1	21
4	5	1	13
4	2	2	23
4	3	2	16
4	4	3	10
4	7	3	12
4	6	4	13
4	8	4	11
5	1	1	28
5	6	1	14
5	2	2	27
5	4	2	18
5	3	3	18
5	8	3	15
5	5	4	16
5	7	4	17
6	1	1	22
6	7	1	17
6	2	2	24
6	6	2	16
6	3	3	18
6	5	3	14
6	4	4	15
6	8	4	17
7	1	1	23
7	8	1	15
7	2	2	21
7	5	2	13
7	3	3	15
7	7	3	12
7	4	4	13
7	6	4	16
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
REPT	VARI	BLOC	Y
1	1	1	20
1	2	1	18
1	3	2	15
1	4	2	16
1	5	3	14
```


```bash
git status
```

```
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both added:      bib1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```


```bash
git add bib1.txt
git commit -m "Resolve conflito, trunca com caixa alta."
```

```
[master 28962a2] Resolve conflito, trunca com caixa alta.
```


```bash
git status
```

```
On branch master
nothing to commit, working directory clean
```

```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   28962a2 (HEAD -> master) Resolve conflito, trunca com caixa alta.
|\  
| * 09dbf4e (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | fc86f72 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   4a44483 Merge branch 'feature02'
|\  
| * 278d3f1 Adiciona aquivo de dados de experimento com rações.
* | 19db415 Arquivo sobre copa 2014 celeção brasileira.
* | 71c72b3 Adiciona função R para VIF.
|/  
* d5f7cdd Novos argumentos.
* 3e3b4d3 Adiciona frase do Linux Torvalds.
* eda2e0a Lista de inicial de o porquê usar o Linux.
* 3bed6b0 Cria arquivo com título.
```


```bash
git reflog
```

```
28962a2 HEAD@{0}: commit (merge): Resolve conflito, trunca com caixa alta.
fc86f72 HEAD@{1}: commit: Arquivo de experimento em BIB. Cabeçalho em caixa alta.
4a44483 HEAD@{2}: checkout: moving from feature03 to master
09dbf4e HEAD@{3}: commit: Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
4a44483 HEAD@{4}: checkout: moving from master to feature03
4a44483 HEAD@{5}: merge feature02: Merge made by the 'recursive' strategy.
19db415 HEAD@{6}: merge feature01: Fast-forward
71c72b3 HEAD@{7}: checkout: moving from feature01 to master
19db415 HEAD@{8}: commit: Arquivo sobre copa 2014 celeção brasileira.
71c72b3 HEAD@{9}: checkout: moving from feature02 to feature01
278d3f1 HEAD@{10}: checkout: moving from 278d3f1035708484740f3b7b383cbb5bfd2f5145 to feature02
278d3f1 HEAD@{11}: commit: Adiciona aquivo de dados de experimento com rações.
d5f7cdd HEAD@{12}: checkout: moving from master to HEAD@{6}
71c72b3 HEAD@{13}: checkout: moving from d5f7cdd48a41d788afb8114ae56d84ce81204261 to master
d5f7cdd HEAD@{14}: checkout: moving from master to HEAD@{4}
71c72b3 HEAD@{15}: merge feature01: Fast-forward
d5f7cdd HEAD@{16}: checkout: moving from feature01 to master
71c72b3 HEAD@{17}: commit: Adiciona função R para VIF.
d5f7cdd HEAD@{18}: checkout: moving from master to feature01
d5f7cdd HEAD@{19}: commit: Novos argumentos.
3e3b4d3 HEAD@{20}: commit: Adiciona frase do Linux Torvalds.
eda2e0a HEAD@{21}: commit: Lista de inicial de o porquê usar o Linux.
3bed6b0 HEAD@{22}: commit (initial): Cria arquivo com título.
```

## Trabalhando com cópias


```bash
git remote -v
```


```bash
## Detório na segunda que terá uma cópia em desenvolvimento do projeto.
pwd
```

```
/home/walmes/marquina2
```


```bash
## Clonando o projeto de outro lugar.
git clone ~/GitLab/testeGit/meu1repo/.git && cd meu1repo
```

```
Cloning into 'meu1repo'...
done.
```


```bash
git status
```

```
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```


```bash
git remote -v
```

```
origin	/home/walmes/GitLab/testeGit/meu1repo/.git (fetch)
origin	/home/walmes/GitLab/testeGit/meu1repo/.git (push)
```


```bash
git log --oneline
```

```
7d5f9f3 Dados de experimento com feijão.
3d73327 Resolve conflito, trunca com caixa alta.
5a0061f Arquivo de experimento em BIB. Cabeçalho em caixa alta.
296bf48 Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
1793721 Merge branch 'feature02'
822fb96 Arquivo sobre copa 2014 celeção brasileira.
d6bcab6 Adiciona aquivo de dados de experimento com rações.
8e5da28 Adiciona função R para VIF.
bf3e89b Novos argumentos.
9550970 Adiciona frase do Linux Torvalds.
6d68b1f Lista de inicial de o porquê usar o Linux.
b3e771f Cria arquivo com título.
```


```bash
git branch -a
```

```
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature03
  remotes/origin/feature04
  remotes/origin/master
```


```bash
git branch feature04
git checkout feature04
```

```
Switched to branch 'feature04'
```




```bash
wget -N 'http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt'
```


```bash
git status
```


```bash
git add diasbarros_feijao.txt
git commit -m "Dados de experimento com feijão."
```


```bash
git push origin feature04
```

Volta para origem e verifica o que recebeu de contribuição.


```bash
pwd
```


```bash
git status
```


```bash
git branch -a
```

Opa! Tem um novo ramo. Vamos ver o que ele tem de diferente.


```bash
git diff --name-only feature04 master
```

Parece que chegou um arquivo novo. Vamos então mesclar ao master.


```bash
git merge feature04 master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```


```bash
pwd
```


```bash
git pull origin master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```


```bash
git log --stat
```


```bash
git log -p -2
```

****
## Ignorando arquivos e diretórios

****
## Trabalhando com repositórios remotos

### Configurando uma conta no GitHub

### Configurando uma conta no GitLab do c3sl

### Requisições de mescla

### Colaborando via fork

****
## Modelos de fluxos de trabalho

****
## Usando ferramentas gráficas para o Git

### Git GUI

### Gitk

### Meld

****
## Dicionário de termos

<!---------------------------------------------------------------------- -->
<!-- Referências ------------------------------------------------------- -->

[Customizing Git - Git Configuration]: http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration
[Setting up a repository]: https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config
[sha1-size]: http://stackoverflow.com/questions/18134627/how-much-of-a-git-sha-is-generally-considered-necessary-to-uniquely-identify-a
[git-log]: http://git-scm.com/docs/git-log
[Installing-Git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[**Git BASH**]: https://lostechies.com/derickbailey/files/2011/03/Screen-shot-2010-11-25-at-10.56.27-AM.png
[**Git GUI**]: http://www.davidegrayson.com/for_blog/entry/20130420_git_win8/git-gui.png
[**Shell Integration**]: http://planetozh.com/blog/wp-content/uploads/2012/11/pewpew.png
[**Gitk**]: http://www.davidegrayson.com/for_blog/entry/20130420_git_win8/git-history.png
[how-to-set-meld-as-git-mergetool]: http://stackoverflow.com/questions/12956509/how-to-set-meld-as-git-mergetool
[linuxmint/nemo]: https://github.com/linuxmint/nemo
[tree]: http://gnuwin32.sourceforge.net/packages/tree.htm
[Git contributing guide]: http://git.leg.ufpr.br/leg/gitlab-rautu/blob/master/CONTRIBUTING.md
[git-diffs]: http://www.git-tower.com/learn/git/ebook/command-line/advanced-topics/diffs
[git-caret-and-tilde]: http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde
[Professora Suely Giolo]: http://www.est.ufpr.br/prof/22-suely.html