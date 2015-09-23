# Tutorial de Git
PET Estatística UFPR  



<!--
## Processar com:
render git_tuto.Rmd
rm -rf meu1repo/ && rm -rf ~/maquina2/meu1repo/ && render git_tuto.Rmd

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

  * Loiane Groner - [Git e Github para iniciantes](https://www.youtube.com/watch?v=UMhskLXJuq4)
  * HxTutors - [Github - Pra que serve e como usar?](https://www.youtube.com/watch?v=neDiLHwXSVo)
  * Devmedia Editora - [Controle de versoes distribuido com Git](https://www.youtube.com/watch?v=1zj8ItHi_Kk)
  * RBtech - [Curso básico de Git (playlist)](https://www.youtube.com/playlist?list=PLInBAd9OZCzzHBJjLFZzRl6DgUmOeG3H0)
  * Luiz Venturote - [Controle de Versão com Git](https://www.youtube.com/playlist?list=PLBzQU3U8iMRndBoeUhURmQf1aLhQExbP8)
  * Leandro Cavalcante [Git (playlist)](https://www.youtube.com/watch?v=GBnt3ztA6nI&list=PLXtEEPEfASEIrUZj9X_kj-dlaul59bRox)
  * StudyClassOficial - [Controle de Versão com GIT](https://www.youtube.com/watch?v=Wj8EB4IAqWc)
  * Israel Santos - [Controle de versão com git](https://www.youtube.com/watch?v=morEwdyzmY4)
  * Giovanni Silva - [Tutorial Git (playlist)](https://www.youtube.com/playlist?list=PL3NGePwPGuvvnBO4tk---xNABmNVEpD2R)
  * makigas - [Tutorial de Git en media hora](https://www.youtube.com/watch?v=QGKTdL7GG24)
  * Desde Cero - [Cómo Instalar Git en Windows Desde Cero](https://www.youtube.com/watch?v=poVAyKNsk00)

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

```sh
user.name=Knight Rider
user.email=batman@justiceleague.org
merge.tool=meld
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
[master (root-commit) 6a515a2] Cria arquivo com título.
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
commit 6a515a2d2728373a9eb07bf4fe68d70dd4f04253
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:13 2015 -0300

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
[master 6752451] Lista de inicial de o porquê usar o Linux.
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
[master bd8a80b] Adiciona frase do Linux Torvalds.
 1 file changed, 4 insertions(+)
```

Agora temos 3 *commits* e o *log* apresenta os *sha1* e as mensagens
correspondentes aos mesmos. Com `--oneline` resumimos o *output* mostrando
apenas o *sha1* e a mensagem de *commit*.


```bash
git log --oneline
```

```
bd8a80b Adiciona frase do Linux Torvalds.
6752451 Lista de inicial de o porquê usar o Linux.
6a515a2 Cria arquivo com título.
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
bd8a80b HEAD@{0}: commit: Adiciona frase do Linux Torvalds.
6752451 HEAD@{1}: commit: Lista de inicial de o porquê usar o Linux.
6a515a2 HEAD@{2}: commit (initial): Cria arquivo com título.
```


```bash
## Adiciona e commita.
git add porqueLinux.txt
git commit -m "Novos argumentos."
```

```
[master a2ad1a5] Novos argumentos.
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
^6a515a2 (Walmes Zeviani 2015-09-23 19:06:13 -0300 1) Meu primeiro repositório Git
bd8a80b3 (Walmes Zeviani 2015-09-23 19:06:13 -0300 2) 
bd8a80b3 (Walmes Zeviani 2015-09-23 19:06:13 -0300 3) A filosofia do Linux é 'Ria na face do perigo'.
bd8a80b3 (Walmes Zeviani 2015-09-23 19:06:13 -0300 4) Ôpa. Errado. 'Faça você mesmo'. É, é essa.
bd8a80b3 (Walmes Zeviani 2015-09-23 19:06:13 -0300 5)                             -- Lunus Torvalds
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
a2ad1a5 Novos argumentos.
bd8a80b Adiciona frase do Linux Torvalds.
6752451 Lista de inicial de o porquê usar o Linux.
6a515a2 Cria arquivo com título.
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
--2015-09-23 19:06:14--  http://people.ufpr.br/~giolo/CE071/Exemplos/vif.R
Resolving people.ufpr.br (people.ufpr.br)... ???.??.???.??, 2801:82:8020:0:8377:0:100:20
Connecting to people.ufpr.br (people.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 560
Saving to: ‘vif.R’

     0K                                                       100% 44,0M=0s

2015-09-23 19:06:14 (44,0 MB/s) - ‘vif.R’ saved [560/560]
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
[feature01 85a471c] Adiciona função R para VIF.
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
85a471c HEAD@{0}: commit: Adiciona função R para VIF.
a2ad1a5 HEAD@{1}: checkout: moving from master to feature01
a2ad1a5 HEAD@{2}: commit: Novos argumentos.
bd8a80b HEAD@{3}: commit: Adiciona frase do Linux Torvalds.
6752451 HEAD@{4}: commit: Lista de inicial de o porquê usar o Linux.
6a515a2 HEAD@{5}: commit (initial): Cria arquivo com título.
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
Updating a2ad1a5..85a471c
Fast-forward
 vif.R | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)
 create mode 100644 vif.R
```


```bash
git log --oneline
```

```
85a471c Adiciona função R para VIF.
a2ad1a5 Novos argumentos.
bd8a80b Adiciona frase do Linux Torvalds.
6752451 Lista de inicial de o porquê usar o Linux.
6a515a2 Cria arquivo com título.
```

É possível criar um ramo a partir de um *commit* ancestral ao atual. Isso
é extremamente útil para resolver os bugs. Vamos fazer um segundo ramo a
partir do *commit* anterior a inclusão do arquivo R.


```bash
## Referencias aos commits.
git reflog
```

```
85a471c HEAD@{0}: merge feature01: Fast-forward
a2ad1a5 HEAD@{1}: checkout: moving from feature01 to master
85a471c HEAD@{2}: commit: Adiciona função R para VIF.
a2ad1a5 HEAD@{3}: checkout: moving from master to feature01
a2ad1a5 HEAD@{4}: commit: Novos argumentos.
bd8a80b HEAD@{5}: commit: Adiciona frase do Linux Torvalds.
6752451 HEAD@{6}: commit: Lista de inicial de o porquê usar o Linux.
6a515a2 HEAD@{7}: commit (initial): Cria arquivo com título.
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

HEAD is now at a2ad1a5... Novos argumentos.
```


```bash
## Qual a situação.
git status
```

```
HEAD detached at a2ad1a5
nothing to commit, working directory clean
```


```bash
## O histório existente nesse ponto.
git log --name-only --oneline
```

```
a2ad1a5 Novos argumentos.
porqueLinux.txt
bd8a80b Adiciona frase do Linux Torvalds.
README.txt
6752451 Lista de inicial de o porquê usar o Linux.
porqueLinux.txt
6a515a2 Cria arquivo com título.
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
* (HEAD detached at a2ad1a5)
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
Previous HEAD position was a2ad1a5... Novos argumentos.
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
85a471c Adiciona função R para VIF.
a2ad1a5 Novos argumentos.
bd8a80b Adiciona frase do Linux Torvalds.
6752451 Lista de inicial de o porquê usar o Linux.
6a515a2 Cria arquivo com título.
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
85a471c HEAD@{0}: checkout: moving from a2ad1a58f8f9d17dd76697b9dd959636e9be8827 to master
a2ad1a5 HEAD@{1}: checkout: moving from master to HEAD@{4}
85a471c HEAD@{2}: merge feature01: Fast-forward
a2ad1a5 HEAD@{3}: checkout: moving from feature01 to master
85a471c HEAD@{4}: commit: Adiciona função R para VIF.
a2ad1a5 HEAD@{5}: checkout: moving from master to feature01
a2ad1a5 HEAD@{6}: commit: Novos argumentos.
bd8a80b HEAD@{7}: commit: Adiciona frase do Linux Torvalds.
6752451 HEAD@{8}: commit: Lista de inicial de o porquê usar o Linux.
6a515a2 HEAD@{9}: commit (initial): Cria arquivo com título.
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

HEAD is now at a2ad1a5... Novos argumentos.
```




```bash
## Baixa arquivo de dados da internet.
wget 'http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt'
```


```
--(date +"%Y-%m-%d %H:%M:%S")--  http://www.leg.ufpr.br/~walmes/data/pimentel_racoes.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 217 [text/plain]
Saving to: ‘pimentel_racoes.txt’

     0K                                                       100% 68,9M=0s

(date +"%Y-%m-%d %H:%M:%S") (68,9 MB/s) - ‘pimentel_racoes.txt’ saved [217/217]

‘pimentel_racoes.txt’ -> ‘../meu1repo/pimentel_racoes.txt’
```


```bash
git status
```

```
HEAD detached at a2ad1a5
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
[detached HEAD 61e9bbf] Adiciona aquivo de dados de experimento com rações.
 1 file changed, 24 insertions(+)
 create mode 100644 pimentel_racoes.txt
```


```bash
git status
```

```
HEAD detached from a2ad1a5
nothing to commit, working directory clean
```


```bash
## Log num formato gráfico ASCII para mostrar o novo ramo.
git log --graph --oneline --decorate --date=relative --all
```

```
* 85a471c (master, feature01) Adiciona função R para VIF.
| * 61e9bbf (HEAD) Adiciona aquivo de dados de experimento com rações.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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
* (HEAD detached from a2ad1a5)
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
* 85a471c (master, feature01) Adiciona função R para VIF.
| * 61e9bbf (HEAD -> feature02) Adiciona aquivo de dados de experimento com rações.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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


```
Diretório existe.
Arquivo brasilCopa2014.txt já existe.
‘brasilCopa2014.txt’ -> ‘../meu1repo/brasilCopa2014.txt’
```


```bash
wget 'http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt'
```


```
--2015-09-23 19:06:15--  http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1254 (1,2K) [text/plain]
Saving to: ‘brasilCopa2014.txt’

     0K .                                                     100% 69,6M=0s

2015-09-23 19:06:15 (69,6 MB/s) - ‘brasilCopa2014.txt’ saved [1254/1254]
```


```bash
git add brasilCopa2014.txt
git commit -m "Arquivo sobre copa 2014 celeção brasileira."
```

```
[feature01 0e14c42] Arquivo sobre copa 2014 celeção brasileira.
 1 file changed, 22 insertions(+)
 create mode 100644 brasilCopa2014.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 0e14c42 (HEAD -> feature01) Arquivo sobre copa 2014 celeção brasileira.
* 85a471c (master) Adiciona função R para VIF.
| * 61e9bbf (feature02) Adiciona aquivo de dados de experimento com rações.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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
Updating 85a471c..0e14c42
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
*   046b056 (HEAD -> master) Merge branch 'feature02'
|\  
| * 61e9bbf (feature02) Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 (feature01) Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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
Deleted branch feature01 (was 0e14c42).
Deleted branch feature02 (was 61e9bbf).
* master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   046b056 (HEAD -> master) Merge branch 'feature02'
|\  
| * 61e9bbf Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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
--2015-09-23 19:06:15--  http://www.leg.ufpr.br/~walmes/data/bib1.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 535 [text/plain]
Saving to: ‘bib1.txt’

     0K                                                       100% 35,0M=0s

2015-09-23 19:06:15 (35,0 MB/s) - ‘bib1.txt’ saved [535/535]
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
[feature03 3bd80e1] Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
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
[master 90864ca] Arquivo de experimento em BIB. Cabeçalho em caixa alta.
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
* 3bd80e1 (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
| * 90864ca (HEAD -> master) Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   046b056 Merge branch 'feature02'
|\  
| * 61e9bbf Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
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
## `less` printa o conteúdo do arquivo mas `head` limita para 10 linhas.
less bib1.txt | head -10
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
[master 8df2b99] Resolve conflito, trunca com caixa alta.
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
*   8df2b99 (HEAD -> master) Resolve conflito, trunca com caixa alta.
|\  
| * 3bd80e1 (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 90864ca Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   046b056 Merge branch 'feature02'
|\  
| * 61e9bbf Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
```


```bash
git reflog
```

```
8df2b99 HEAD@{0}: commit (merge): Resolve conflito, trunca com caixa alta.
90864ca HEAD@{1}: commit: Arquivo de experimento em BIB. Cabeçalho em caixa alta.
046b056 HEAD@{2}: checkout: moving from feature03 to master
3bd80e1 HEAD@{3}: commit: Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
046b056 HEAD@{4}: checkout: moving from master to feature03
046b056 HEAD@{5}: merge feature02: Merge made by the 'recursive' strategy.
0e14c42 HEAD@{6}: merge feature01: Fast-forward
85a471c HEAD@{7}: checkout: moving from feature01 to master
0e14c42 HEAD@{8}: commit: Arquivo sobre copa 2014 celeção brasileira.
85a471c HEAD@{9}: checkout: moving from feature02 to feature01
61e9bbf HEAD@{10}: checkout: moving from 61e9bbf687a02cb3daa490126fb7f1d18779efed to feature02
61e9bbf HEAD@{11}: commit: Adiciona aquivo de dados de experimento com rações.
a2ad1a5 HEAD@{12}: checkout: moving from master to HEAD@{6}
85a471c HEAD@{13}: checkout: moving from a2ad1a58f8f9d17dd76697b9dd959636e9be8827 to master
a2ad1a5 HEAD@{14}: checkout: moving from master to HEAD@{4}
85a471c HEAD@{15}: merge feature01: Fast-forward
a2ad1a5 HEAD@{16}: checkout: moving from feature01 to master
85a471c HEAD@{17}: commit: Adiciona função R para VIF.
a2ad1a5 HEAD@{18}: checkout: moving from master to feature01
a2ad1a5 HEAD@{19}: commit: Novos argumentos.
bd8a80b HEAD@{20}: commit: Adiciona frase do Linux Torvalds.
6752451 HEAD@{21}: commit: Lista de inicial de o porquê usar o Linux.
6a515a2 HEAD@{22}: commit (initial): Cria arquivo com título.
```

## Trabalhando com cópias




```bash
git remote -v
```


```bash
## Diretório na segunda que terá uma cópia em desenvolvimento do
## projeto.
pwd
```

```
/home/walmes/maquina2
```


```bash
## Conteúdo.
tree -a
```

```
.

0 directories, 0 files
```


```bash
## Clonando o projeto de outro lugar.
## $DIRGIT representa o caminho para chegar até meu1repo.
git clone "$DIRGIT/meu1repo/.git" && cd meu1repo
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
## Conteúdo após clonar.
tree
```

```
.
└── meu1repo
    ├── bib1.txt
    ├── brasilCopa2014.txt
    ├── pimentel_racoes.txt
    ├── porqueLinux.txt
    ├── README.txt
    └── vif.R

1 directory, 6 files
```


```bash
git remote -v
```

```
origin	/home/walmes/GitLab/git-tutorial/meu1repo/.git (fetch)
origin	/home/walmes/GitLab/git-tutorial/meu1repo/.git (push)
```


```bash
git log --oneline
```

```
8df2b99 Resolve conflito, trunca com caixa alta.
90864ca Arquivo de experimento em BIB. Cabeçalho em caixa alta.
3bd80e1 Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
046b056 Merge branch 'feature02'
0e14c42 Arquivo sobre copa 2014 celeção brasileira.
61e9bbf Adiciona aquivo de dados de experimento com rações.
85a471c Adiciona função R para VIF.
a2ad1a5 Novos argumentos.
bd8a80b Adiciona frase do Linux Torvalds.
6752451 Lista de inicial de o porquê usar o Linux.
6a515a2 Cria arquivo com título.
```


```bash
git branch -a
```

```
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature03
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
## Tenta ir para o diretório downloads, se não conseguir é porque não
## existe então cria um diretório download para então entrar nele.
if [ -d downloads ]
then
    echo "Diretório existe."
    cd downloads
else
    echo "Diretório não existe."
    mkdir downloads
    cd downloads
fi

## Se não existir o aquivo diasbarros_feijao.txt, então baixar da
## internet.
if [ ! -f diasbarros_feijao.txt ]
then
    echo "Arquivo diasbarros_feijao.txt não existe. Baixando..."
    wget 'http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt'
else
    echo "Arquivo diasbarros_feijao.txt já existe."
fi

## Copiar o arquivo diasbarros_feijao.txt para o meu1repo (-v: verbose).
cp -v diasbarros_feijao.txt ~/maquina2/meu1repo/
```

```
Diretório existe.
Arquivo diasbarros_feijao.txt já existe.
‘diasbarros_feijao.txt’ -> ‘/home/walmes/maquina2/meu1repo/diasbarros_feijao.txt’
```


```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt'
```


```
--2015-09-23 19:06:16--  http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 487 [text/plain]
Saving to: ‘diasbarros_feijao.txt’

     0K                                                       100% 40,2M=0s

2015-09-23 19:06:16 (40,2 MB/s) - ‘diasbarros_feijao.txt’ saved [487/487]
```


```bash
git status
```

```
On branch feature04
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	diasbarros_feijao.txt

nothing added to commit but untracked files present (use "git add" to track)
```


```bash
git add diasbarros_feijao.txt
git commit -m "Dados de experimento com feijão."
```

```
[feature04 6c60887] Dados de experimento com feijão.
 1 file changed, 37 insertions(+)
 create mode 100644 diasbarros_feijao.txt
```


```bash
git push origin feature04
```

```
To /home/walmes/GitLab/git-tutorial/meu1repo/.git
 * [new branch]      feature04 -> feature04
```

Volta para origem e verifica o que recebeu de contribuição.


```bash
pwd
```

```
/home/walmes/GitLab/git-tutorial/meu1repo
```


```bash
git status
```

```
On branch master
nothing to commit, working directory clean
```


```bash
git branch -a
```

```
  feature03
  feature04
* master
```

Opa! Tem um novo ramo. Vamos ver o que ele tem de diferente.


```bash
git diff --name-only feature04 master
```

```
diasbarros_feijao.txt
```

Parece que chegou um arquivo novo. Vamos então mesclar ao master.


```bash
git merge feature04 master
```

```
Updating 8df2b99..6c60887
Fast-forward
 diasbarros_feijao.txt | 37 +++++++++++++++++++++++++++++++++++++
 1 file changed, 37 insertions(+)
 create mode 100644 diasbarros_feijao.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 6c60887 (HEAD -> master, feature04) Dados de experimento com feijão.
*   8df2b99 Resolve conflito, trunca com caixa alta.
|\  
| * 3bd80e1 (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 90864ca Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   046b056 Merge branch 'feature02'
|\  
| * 61e9bbf Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
```


```bash
pwd
```

```
/home/walmes/maquina2/meu1repo
```


```bash
git pull origin master
```

```
From /home/walmes/GitLab/git-tutorial/meu1repo/
 * branch            master     -> FETCH_HEAD
   8df2b99..6c60887  master     -> origin/master
Already up-to-date.
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 6c60887 (HEAD -> feature04, origin/master, origin/feature04, origin/HEAD) Dados de experimento com feijão.
*   8df2b99 (master) Resolve conflito, trunca com caixa alta.
|\  
| * 3bd80e1 (origin/feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 90864ca Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   046b056 Merge branch 'feature02'
|\  
| * 61e9bbf Adiciona aquivo de dados de experimento com rações.
* | 0e14c42 Arquivo sobre copa 2014 celeção brasileira.
* | 85a471c Adiciona função R para VIF.
|/  
* a2ad1a5 Novos argumentos.
* bd8a80b Adiciona frase do Linux Torvalds.
* 6752451 Lista de inicial de o porquê usar o Linux.
* 6a515a2 Cria arquivo com título.
```


```bash
git log --stat
```

```
commit 6c608873941e2cff8c7414392f308d64bc1153c0
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:16 2015 -0300

    Dados de experimento com feijão.

 diasbarros_feijao.txt | 37 +++++++++++++++++++++++++++++++++++++
 1 file changed, 37 insertions(+)

commit 8df2b999bc19b929ba5b17aa5fa70b7adb28de31
Merge: 90864ca 3bd80e1
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Resolve conflito, trunca com caixa alta.

commit 90864ca25c5374d49d49e8f991f6def020b43b34
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Arquivo de experimento em BIB. Cabeçalho em caixa alta.

 bib1.txt | 58 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 58 insertions(+)

commit 3bd80e113d4c8ba530c110dceed750ce7783a53f
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.

 bib1.txt | 58 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 58 insertions(+)

commit 046b056d6bbced5bc980a9a0df53ed7896428335
Merge: 0e14c42 61e9bbf
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Merge branch 'feature02'

commit 0e14c4258f2c94f8031fd5a801869ad790a856a5
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Arquivo sobre copa 2014 celeção brasileira.

 brasilCopa2014.txt | 22 ++++++++++++++++++++++
 1 file changed, 22 insertions(+)

commit 61e9bbf687a02cb3daa490126fb7f1d18779efed
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:14 2015 -0300

    Adiciona aquivo de dados de experimento com rações.

 pimentel_racoes.txt | 24 ++++++++++++++++++++++++
 1 file changed, 24 insertions(+)

commit 85a471c9ddca137539b47597441161501882f9cd
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:14 2015 -0300

    Adiciona função R para VIF.

 vif.R | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)

commit a2ad1a58f8f9d17dd76697b9dd959636e9be8827
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:14 2015 -0300

    Novos argumentos.

 porqueLinux.txt | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

commit bd8a80b33badcd9c68da6576e3d34180c8f813fa
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:13 2015 -0300

    Adiciona frase do Linux Torvalds.

 README.txt | 4 ++++
 1 file changed, 4 insertions(+)

commit 6752451f0914cb1329e7d93a175258649e724517
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:13 2015 -0300

    Lista de inicial de o porquê usar o Linux.

 porqueLinux.txt | 5 +++++
 1 file changed, 5 insertions(+)

commit 6a515a2d2728373a9eb07bf4fe68d70dd4f04253
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:13 2015 -0300

    Cria arquivo com título.

 README.txt | 1 +
 1 file changed, 1 insertion(+)
```


```bash
git log -p -2
```

```
commit 6c608873941e2cff8c7414392f308d64bc1153c0
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:16 2015 -0300

    Dados de experimento com feijão.

diff --git a/diasbarros_feijao.txt b/diasbarros_feijao.txt
new file mode 100644
index 0000000..2525ebf
--- /dev/null
+++ b/diasbarros_feijao.txt
@@ -0,0 +1,37 @@
+## Teor proteico avaliado em 10 cultivares de feijoeiro e 1 de soja em
+## um ensaio em DIC com 3 repetições. Dias & Barros, Biometria
+## Experimental, pg 222.
+cultivar	rept	teorProt
+1	1	27.2
+1	2	26.1
+1	3	26.2
+2	1	26.6
+2	2	26.7
+2	3	26.7
+3	1	29.5
+3	2	29.4
+3	3	29.5
+4	1	30.9
+4	2	31.3
+4	3	31.4
+5	1	27.7
+5	2	27.9
+5	3	27.3
+6	1	33.7
+6	2	33.5
+6	3	33.3
+7	1	28.4
+7	2	28.5
+7	3	28.3
+8	1	27.3
+8	2	27.3
+8	3	27.4
+9	1	30.1
+9	2	30.2
+9	3	29.9
+10	1	22.4
+10	2	21.7
+10	3	22.3
+11	1	45.7
+11	2	45.9
+11	3	46.3

commit 8df2b999bc19b929ba5b17aa5fa70b7adb28de31
Merge: 90864ca 3bd80e1
Author: Walmes Zeviani <walmeszeviani@gmail.com>
Date:   Wed Sep 23 19:06:15 2015 -0300

    Resolve conflito, trunca com caixa alta.
```



****
## Ignorando arquivos e diretórios

****
## Trabalhando com repositórios remotos

Na etapa que vem a seguir, será solicitado uma senha
(`passphrase`). Você pode forncer uma ou apenas pressinar Enter para
correr o procedimento padrão. O resultado é uma senha gráfica ASCII.


```sh
ssh-keygen -t rsa -C "batman@justiceleague.org"
```

```sh
Generating public/private rsa key pair.
Enter file in which to save the key (/home/batman/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/batman/.ssh/id_rsa.
Your public key has been saved in /home/batman/.ssh/id_rsa.pub.
The key fingerprint is:
66:c1:0b:3a:94:25:83:00:81:9f:40:26:f7:aa:af:3a batman@justiceleague.org
The key's randomart image is:
          +--[ RSA 2048]----+
          |                 |
 ~MMMMMMMMMMMM           MMMMMMMMMMMM~  
    .MMMMMMMMM.   MMM   .MMMMMMMMM.     
      MMMMMMMMMMMMMMMMMMMMMMMMMMM       
       MMMMMMMMMMMMMMMMMMMMMMMMM       
      .MMMMMMMMMMMMMMMMMMMMMMMMM.        
              .MMMMMMMMM.               
                 .MMM.                  
                   M                    
          |                 |
          +-----------------+
```

O importante é o conteúdo do arquivo `/home/batman/.ssh/id_rsa.pub`. Este
deve ser fornecido ao GitLab (ou GitHub) em uma janela com as chaves. Os
endereços abaixo levam para a mencionada janela. Requer que esteja
logado.

  * GitLab: <http://gitab.c3sl.ufpr.br/profile/keys>
  * GitHub: <https://github.com/settings/ssh>

Nessa janela deverá ser informado o código gerado pelo
`ssh-keygen`. Você deve copiar o texto do arquivo
`/home/batman/.ssh/id_rsa.pub`, sem moficá-lo, e fornecer ao GitLab.
Para ver/abrir o conteúdo do arquivo no próprio terminal use `less` ou
`cat`. Para copiar do terminal use `ctrl+shift+c`. Para abrir com um
editor de texto, o `gedit` por exemplo, é só passar o nome do arquivo.

```sh
## Mostra o conteúdo do arquivo no próprio terminal.
less /home/batman/.ssh/id_rsa.pub  

## Abre o arquivo com o editor de texto Gedit.
gedit /home/batman/.ssh/id_rsa.pub
```

```
ssh-rsa BBBBB3NzaC1yc2EAAAADAQABAAABAQDDuQmvkQ0WgwYQvR16z37tG37Q61ID+Qf4hi8+cARjjSWP7015CAtRnCvmGFSbdFMjz3ZEkp2XzHIyRCKw2hLP57rkFcfioWra6N5/9+z+tPiwr2OzwLfk7J/GAETGA4rtoToV96hf5RvKRhvuqyO5uf5ouBILm1PRpjA/5AkfToWp25/7WC136eGIOSJMFgQ3OuK5U+qSXAwuSdu9Uj1XkVYFDjasA45ZjsnkE6L9bKiYymadshEbWEBHJAWqDErd8srMtBYS/2hodNnjfH7rNHHCo8wZD5GJFz7YUodaBSaSYuHVfrEryaEm/r5787CAiecFAjWEeVq6StM7N/lz batman@justiceleague.org
```

Para conferir a comunicação da sua máquina com o servidor do GitLab do
c3sl ou do GitHub, aplique a instrução `ssh` abaixo.

```sh
## Com gitlab do c3sl.
ssh -T git@gitlab.c3sl.ufpr.br

## Com github.
ssh -T git@github.com
```

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
