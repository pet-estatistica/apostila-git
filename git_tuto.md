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

TODO Materiais a serem lidos
* http://www.atualsistemas.net/dev/Manual_Git.PDF
* http://www.dcc.fc.up.pt/~pbv/aulas/labprog/slides/gitprimer.pdf

## Wiki de um tutorial completo do Conselho Nacional de Justiça.
http://www.cnj.jus.br/wikipje/index.php/GIT

## Slides com muitas ilustrações.
http://wiki.softwarelivre.org/pub/Blogs/BlogPostAntonioTerceiro20081108115324/curso-vcs.pdf

## Compara serviços de versionamento
http://www.ufjf.br/getcomp/files/2013/03/An%C3%A1lise-Comparativa-entre-Sistemas-de-Controle-de-Vers%C3%B5es-Daniel-Tannure-Menandro-de-Freitas.pdf

## Aproveita-se no glossario e cheat sheet
http://www.ceuma.br/nucleodeti/wp-content/uploads/2013/12/Git_v0.1.2.pdf
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

O Git é uma ferramenta de controle de versão que facilita os projetos em equipe 
a verficação do mesmo. Basicamente, o Git detecta as mudanças que ocorrem no
arquivo, bem como onde ocorreu e qual mudança foi feita. Ainda existe a
possibilidade de voltar no histórico do projeto, sempre que necessário.
Outra facilidade está na equipe trabalhar em cima do projeto ao mesmo tempo,
e no final o Git faz o trabalho de juntar todos os arquivos mostrando se há
algum conflito. Integrantes podem mandar sugestões de alterações, e cabe ao
responsável pelo projeto incorporar ou não essas alterações.

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
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

disponível comandos git em '/usr/lib/git-core'

  add                       merge-octopus
  add--interactive          merge-one-file
  am                        merge-ours
  annotate                  merge-recursive
  apply                     merge-resolve
  archimport                merge-subtree
  archive                   merge-tree
  bisect                    mergetool
  bisect--helper            mktag
  blame                     mktree
  branch                    mv
  bundle                    name-rev
  cat-file                  notes
  check-attr                p4
  check-ignore              pack-objects
  check-mailmap             pack-redundant
  check-ref-format          pack-refs
  checkout                  patch-id
  checkout-index            peek-remote
  cherry                    prune
  cherry-pick               prune-packed
  citool                    pull
  clean                     push
  clone                     quiltimport
  column                    read-tree
  commit                    rebase
  commit-tree               receive-pack
  config                    reflog
  count-objects             relink
  credential                remote
  credential-cache          remote-ext
  credential-cache--daemon  remote-fd
  credential-store          remote-ftp
  cvsexportcommit           remote-ftps
  cvsimport                 remote-http
  cvsserver                 remote-https
  daemon                    remote-testpy
  describe                  remote-testsvn
  diff                      repack
  diff-files                replace
  diff-index                repo-config
  diff-tree                 request-pull
  difftool                  rerere
  difftool--helper          reset
  fast-export               rev-list
  fast-import               rev-parse
  fetch                     revert
  fetch-pack                rm
  filter-branch             send-email
  fmt-merge-msg             send-pack
  for-each-ref              sh-i18n--envsubst
  format-patch              shell
  fsck                      shortlog
  fsck-objects              show
  gc                        show-branch
  get-tar-commit-id         show-index
  grep                      show-ref
  gui                       stage
  gui--askpass              stash
  hash-object               status
  help                      stripspace
  http-backend              submodule
  http-fetch                subtree
  http-push                 svn
  imap-send                 symbolic-ref
  index-pack                tag
  init                      tar-tree
  init-db                   unpack-file
  instaweb                  unpack-objects
  log                       update-index
  lost-found                update-ref
  ls-files                  update-server-info
  ls-remote                 upload-archive
  ls-tree                   upload-pack
  mailinfo                  var
  mailsplit                 verify-pack
  merge                     verify-tag
  merge-base                web--browse
  merge-file                whatchanged
  merge-index               write-tree

'git help -a' and 'git help -g' lists available subcommands and some
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
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

disponível comandos git em '/usr/lib/git-core'

  add                       merge-octopus
  add--interactive          merge-one-file
  am                        merge-ours
  annotate                  merge-recursive
  apply                     merge-resolve
  archimport                merge-subtree
  archive                   merge-tree
  bisect                    mergetool
  bisect--helper            mktag
  blame                     mktree
  branch                    mv
  bundle                    name-rev
  cat-file                  notes
  check-attr                p4
  check-ignore              pack-objects
  check-mailmap             pack-redundant
  check-ref-format          pack-refs
  checkout                  patch-id
  checkout-index            peek-remote
  cherry                    prune
  cherry-pick               prune-packed
  citool                    pull
  clean                     push
  clone                     quiltimport
  column                    read-tree
  commit                    rebase
  commit-tree               receive-pack
  config                    reflog
  count-objects             relink
  credential                remote
  credential-cache          remote-ext
  credential-cache--daemon  remote-fd
  credential-store          remote-ftp
  cvsexportcommit           remote-ftps
  cvsimport                 remote-http
  cvsserver                 remote-https
  daemon                    remote-testpy
  describe                  remote-testsvn
  diff                      repack
  diff-files                replace
  diff-index                repo-config
  diff-tree                 request-pull
  difftool                  rerere
  difftool--helper          reset
  fast-export               rev-list
  fast-import               rev-parse
  fetch                     revert
  fetch-pack                rm
  filter-branch             send-email
  fmt-merge-msg             send-pack
  for-each-ref              sh-i18n--envsubst
  format-patch              shell
  fsck                      shortlog
  fsck-objects              show
  gc                        show-branch
  get-tar-commit-id         show-index
  grep                      show-ref
  gui                       stage
  gui--askpass              stash
  hash-object               status
  help                      stripspace
  http-backend              submodule
  http-fetch                subtree
  http-push                 svn
  imap-send                 symbolic-ref
  index-pack                tag
  init                      tar-tree
  init-db                   unpack-file
  instaweb                  unpack-objects
  log                       update-index
  lost-found                update-ref
  ls-files                  update-server-info
  ls-remote                 upload-archive
  ls-tree                   upload-pack
  mailinfo                  var
  mailsplit                 verify-pack
  merge                     verify-tag
  merge-base                web--browse
  merge-file                whatchanged
  merge-index               write-tree

'git help -a' and 'git help -g' lists available subcommands and some
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
Initialized empty Git repository in /media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo/.git/
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
No ramo master

Submissão inicial.

Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

	README.txt

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
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
No ramo master

Submissão inicial.

Mudanças a serem submetidas:
  (utilize "git rm --cached <arquivo>..." para não apresentar)

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
[master (root-commit) e248651] Cria arquivo com título.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

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
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

	modificado: README.txt

Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

	porqueLinux.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
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
commit e2486515a9e75bf8e9e2e38e63e557c32ad887bf
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:58 2015 -0300

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
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

	new file:   porqueLinux.txt

Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

	modificado: README.txt
```


```bash
## Mensagem que registra as modificações adicionadas.
git commit -m "Lista de inicial de o porquê usar o Linux."
```

```
[master 68a99fc] Lista de inicial de o porquê usar o Linux.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 5 insertions(+)
 create mode 100644 porqueLinux.txt
```


```bash
git status
```

```
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

	modificado: README.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
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
No ramo master
Mudanças a serem submetidas:
  (use "git reset HEAD <file>..." to unstage)

	modificado: README.txt
```


```bash
## Atribui mensagem de notificação.
git commit -m "Adiciona frase do Linux Torvalds."
```

```
[master 28205ac] Adiciona frase do Linux Torvalds.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 4 insertions(+)
```

Agora temos 3 *commits* e o *log* apresenta os *sha1* e as mensagens
correspondentes aos mesmos. Com `--oneline` resumimos o *output* mostrando
apenas o *sha1* e a mensagem de *commit*.


```bash
git log --oneline
```

```
28205ac Adiciona frase do Linux Torvalds.
68a99fc Lista de inicial de o porquê usar o Linux.
e248651 Cria arquivo com título.
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
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

	modificado: porqueLinux.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
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
No ramo master
nada a submeter, diretório de trabalho vazio
```

Vamos seguir com as modificações em `porqueLinux.txt` que corrigem o
texto e acrescentam itens novos.




```bash
git status
```

```
No ramo master
Changes not staged for commit:
  (utilize "git add <arquivo>..." para atualizar o que será submetido)
  (utilize "git checkout -- <arquivo>..." para descartar mudanças no diretório de trabalho)

	modificado: porqueLinux.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
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
28205ac HEAD@{0}: commit: Adiciona frase do Linux Torvalds.
68a99fc HEAD@{1}: commit: Lista de inicial de o porquê usar o Linux.
e248651 HEAD@{2}: commit (initial): Cria arquivo com título.
```


```bash
## Adiciona e commita.
git add porqueLinux.txt
git commit -m "Novos argumentos."
```

```
[master e57eeaf] Novos argumentos.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

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
^e248651 (Teste 2015-10-01 16:36:58 -0300 1) Meu primeiro repositório Git
28205ac7 (Teste 2015-10-01 16:36:59 -0300 2) 
28205ac7 (Teste 2015-10-01 16:36:59 -0300 3) A filosofia do Linux é 'Ria na face do perigo'.
28205ac7 (Teste 2015-10-01 16:36:59 -0300 4) Ôpa. Errado. 'Faça você mesmo'. É, é essa.
28205ac7 (Teste 2015-10-01 16:36:59 -0300 5)                             -- Lunus Torvalds
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
No ramo feature01
nada a submeter, diretório de trabalho vazio
```


```bash
## Histórico de commits.
git log --oneline
```

```
e57eeaf Novos argumentos.
28205ac Adiciona frase do Linux Torvalds.
68a99fc Lista de inicial de o porquê usar o Linux.
e248651 Cria arquivo com título.
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
--2015-10-01 16:36:59--  http://people.ufpr.br/~giolo/CE071/Exemplos/vif.R
Resolving people.ufpr.br (people.ufpr.br)... ???.??.???.??, 2801:82:8020:0:8377:0:100:20
Connecting to people.ufpr.br (people.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 560
Saving to: ‘vif.R’

     0K                                                       100% 44,0M=0s

2015-10-01 16:36:59 (44,0 MB/s) - ‘vif.R’ saved [560/560]
```


```bash
## Situação do repositório após o download.
git status
```

```
No ramo feature01
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

	vif.R

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```


```bash
git add vif.R
git commit -m "Adiciona função R para VIF."
```

```
[feature01 294a431] Adiciona função R para VIF.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

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
294a431 HEAD@{0}: commit: Adiciona função R para VIF.
e57eeaf HEAD@{1}: checkout: moving from master to feature01
e57eeaf HEAD@{2}: commit: Novos argumentos.
28205ac HEAD@{3}: commit: Adiciona frase do Linux Torvalds.
68a99fc HEAD@{4}: commit: Lista de inicial de o porquê usar o Linux.
e248651 HEAD@{5}: commit (initial): Cria arquivo com título.
```


```bash
git status
```

```
No ramo feature01
nada a submeter, diretório de trabalho vazio
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
Updating e57eeaf..294a431
Fast-forward
 vif.R | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)
 create mode 100644 vif.R
```


```bash
git log --oneline
```

```
294a431 Adiciona função R para VIF.
e57eeaf Novos argumentos.
28205ac Adiciona frase do Linux Torvalds.
68a99fc Lista de inicial de o porquê usar o Linux.
e248651 Cria arquivo com título.
```

É possível criar um ramo a partir de um *commit* ancestral ao atual. Isso
é extremamente útil para resolver os bugs. Vamos fazer um segundo ramo a
partir do *commit* anterior a inclusão do arquivo R.


```bash
## Referencias aos commits.
git reflog
```

```
294a431 HEAD@{0}: merge feature01: Fast-forward
e57eeaf HEAD@{1}: checkout: moving from feature01 to master
294a431 HEAD@{2}: commit: Adiciona função R para VIF.
e57eeaf HEAD@{3}: checkout: moving from master to feature01
e57eeaf HEAD@{4}: commit: Novos argumentos.
28205ac HEAD@{5}: commit: Adiciona frase do Linux Torvalds.
68a99fc HEAD@{6}: commit: Lista de inicial de o porquê usar o Linux.
e248651 HEAD@{7}: commit (initial): Cria arquivo com título.
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

  git checkout -b new_branch_name

HEAD is now at e57eeaf... Novos argumentos.
```


```bash
## Qual a situação.
git status
```

```
HEAD detached at e57eeaf
nada a submeter, diretório de trabalho vazio
```


```bash
## O histório existente nesse ponto.
git log --name-only --oneline
```

```
e57eeaf Novos argumentos.
porqueLinux.txt
28205ac Adiciona frase do Linux Torvalds.
README.txt
68a99fc Lista de inicial de o porquê usar o Linux.
porqueLinux.txt
e248651 Cria arquivo com título.
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
* (detached from e57eeaf)
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
Previous HEAD position was e57eeaf... Novos argumentos.
Switched to branch 'master'
```


```bash
git status
```

```
No ramo master
nada a submeter, diretório de trabalho vazio
```


```bash
git log --oneline
```

```
294a431 Adiciona função R para VIF.
e57eeaf Novos argumentos.
28205ac Adiciona frase do Linux Torvalds.
68a99fc Lista de inicial de o porquê usar o Linux.
e248651 Cria arquivo com título.
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
294a431 HEAD@{0}: checkout: moving from e57eeaff9e77da94b22e5da043676a3cf70ed0b1 to master
e57eeaf HEAD@{1}: checkout: moving from master to HEAD@{4}
294a431 HEAD@{2}: merge feature01: Fast-forward
e57eeaf HEAD@{3}: checkout: moving from feature01 to master
294a431 HEAD@{4}: commit: Adiciona função R para VIF.
e57eeaf HEAD@{5}: checkout: moving from master to feature01
e57eeaf HEAD@{6}: commit: Novos argumentos.
28205ac HEAD@{7}: commit: Adiciona frase do Linux Torvalds.
68a99fc HEAD@{8}: commit: Lista de inicial de o porquê usar o Linux.
e248651 HEAD@{9}: commit (initial): Cria arquivo com título.
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

  git checkout -b new_branch_name

HEAD is now at e57eeaf... Novos argumentos.
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
HEAD detached at e57eeaf
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

	pimentel_racoes.txt

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```


```bash
## Adiciona para registrar a inclusão do arquivo.
git add pimentel_racoes.txt
git commit -m "Adiciona aquivo de dados de experimento com rações."
```

```
[detached HEAD eb21436] Adiciona aquivo de dados de experimento com rações.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 24 insertions(+)
 create mode 100644 pimentel_racoes.txt
```


```bash
git status
```

```
HEAD detached from e57eeaf
nada a submeter, diretório de trabalho vazio
```


```bash
## Log num formato gráfico ASCII para mostrar o novo ramo.
git log --graph --oneline --decorate --date=relative --all
```

```
* eb21436 (HEAD) Adiciona aquivo de dados de experimento com rações.
| * 294a431 (master, feature01) Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
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
* (detached from e57eeaf)
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
* eb21436 (HEAD, feature02) Adiciona aquivo de dados de experimento com rações.
| * 294a431 (master, feature01) Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
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
“brasilCopa2014.txt” -> “../meu1repo/brasilCopa2014.txt”
```


```bash
wget 'http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt'
```


```
--2015-10-01 16:37:00--  http://www.leg.ufpr.br/~walmes/cursoR/geneticaEsalq/brasilCopa2014.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1254 (1,2K) [text/plain]
Saving to: ‘brasilCopa2014.txt’

     0K .                                                     100% 69,6M=0s

2015-10-01 16:37:00 (69,6 MB/s) - ‘brasilCopa2014.txt’ saved [1254/1254]
```


```bash
git add brasilCopa2014.txt
git commit -m "Arquivo sobre copa 2014 celeção brasileira."
```

```
[feature01 6737802] Arquivo sobre copa 2014 celeção brasileira.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 22 insertions(+)
 create mode 100644 brasilCopa2014.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 6737802 (HEAD, feature01) Arquivo sobre copa 2014 celeção brasileira.
* 294a431 (master) Adiciona função R para VIF.
| * eb21436 (feature02) Adiciona aquivo de dados de experimento com rações.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
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
Updating 294a431..6737802
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
*   9bf4962 (HEAD, master) Merge branch 'feature02'
|\  
| * eb21436 (feature02) Adiciona aquivo de dados de experimento com rações.
* | 6737802 (feature01) Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
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
Deleted branch feature01 (was 6737802).
Deleted branch feature02 (was eb21436).
* master
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   9bf4962 (HEAD, master) Merge branch 'feature02'
|\  
| * eb21436 Adiciona aquivo de dados de experimento com rações.
* | 6737802 Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
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
--2015-10-01 16:37:00--  http://www.leg.ufpr.br/~walmes/data/bib1.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 535 [text/plain]
Saving to: ‘bib1.txt’

     0K                                                       100% 35,0M=0s

2015-10-01 16:37:00 (35,0 MB/s) - ‘bib1.txt’ saved [535/535]
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
[feature03 981d1ee] Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

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
[master 7546ee7] Arquivo de experimento em BIB. Cabeçalho em caixa alta.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

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
* 981d1ee (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
| * 7546ee7 (HEAD, master) Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   9bf4962 Merge branch 'feature02'
|\  
| * eb21436 Adiciona aquivo de dados de experimento com rações.
* | 6737802 Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
```


```bash
## Dá mensagem de erro que informa o conflito.
git merge feature03 master
```


```
Mesclagem automática de bib1.txt
CONFLITO (adicionar/adicionar): conflito de mesclagem em bib1.txt
Automatic merge failed; fix conflicts and then commit the result.
```


```bash
git status
```

```
No ramo master
Você tem caminhos não mesclados.
  (fixar conflitos e executar "git commit")

Caminhos não mesclados:
  (usar "git add <arquivo>..." para marcar resolução)

	ambos adicionaram:  bib1.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
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
No ramo master
Você tem caminhos não mesclados.
  (fixar conflitos e executar "git commit")

Caminhos não mesclados:
  (usar "git add <arquivo>..." para marcar resolução)

	ambos adicionaram:  bib1.txt

nenhuma modificação adicionada à submissão (utilize "git add" e/ou "git commit -a")
```


```bash
git add bib1.txt
git commit -m "Resolve conflito, trunca com caixa alta."
```

```
[master f44bbdf] Resolve conflito, trunca com caixa alta.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author
```


```bash
git status
```

```
No ramo master
nada a submeter, diretório de trabalho vazio
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
*   f44bbdf (HEAD, master) Resolve conflito, trunca com caixa alta.
|\  
| * 981d1ee (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 7546ee7 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   9bf4962 Merge branch 'feature02'
|\  
| * eb21436 Adiciona aquivo de dados de experimento com rações.
* | 6737802 Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
```


```bash
git reflog
```

```
f44bbdf HEAD@{0}: commit (merge): Resolve conflito, trunca com caixa alta.
7546ee7 HEAD@{1}: commit: Arquivo de experimento em BIB. Cabeçalho em caixa alta.
9bf4962 HEAD@{2}: checkout: moving from feature03 to master
981d1ee HEAD@{3}: commit: Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
9bf4962 HEAD@{4}: checkout: moving from master to feature03
9bf4962 HEAD@{5}: merge feature02: Merge made by the 'recursive' strategy.
6737802 HEAD@{6}: merge feature01: Fast-forward
294a431 HEAD@{7}: checkout: moving from feature01 to master
6737802 HEAD@{8}: commit: Arquivo sobre copa 2014 celeção brasileira.
294a431 HEAD@{9}: checkout: moving from feature02 to feature01
eb21436 HEAD@{10}: checkout: moving from eb21436153d68107dacd3e47aca77773b91a1f42 to feature02
eb21436 HEAD@{11}: commit: Adiciona aquivo de dados de experimento com rações.
e57eeaf HEAD@{12}: checkout: moving from master to HEAD@{6}
294a431 HEAD@{13}: checkout: moving from e57eeaff9e77da94b22e5da043676a3cf70ed0b1 to master
e57eeaf HEAD@{14}: checkout: moving from master to HEAD@{4}
294a431 HEAD@{15}: merge feature01: Fast-forward
e57eeaf HEAD@{16}: checkout: moving from feature01 to master
294a431 HEAD@{17}: commit: Adiciona função R para VIF.
e57eeaf HEAD@{18}: checkout: moving from master to feature01
e57eeaf HEAD@{19}: commit: Novos argumentos.
28205ac HEAD@{20}: commit: Adiciona frase do Linux Torvalds.
68a99fc HEAD@{21}: commit: Lista de inicial de o porquê usar o Linux.
e248651 HEAD@{22}: commit (initial): Cria arquivo com título.
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
/home/est/acn13/maquina2
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
No ramo master
Your branch is up-to-date with 'origin/master'.

nada a submeter, diretório de trabalho vazio
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
origin	/media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo/.git (fetch)
origin	/media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo/.git (push)
```


```bash
git log --oneline
```

```
f44bbdf Resolve conflito, trunca com caixa alta.
7546ee7 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
981d1ee Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
9bf4962 Merge branch 'feature02'
6737802 Arquivo sobre copa 2014 celeção brasileira.
eb21436 Adiciona aquivo de dados de experimento com rações.
294a431 Adiciona função R para VIF.
e57eeaf Novos argumentos.
28205ac Adiciona frase do Linux Torvalds.
68a99fc Lista de inicial de o porquê usar o Linux.
e248651 Cria arquivo com título.
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
“diasbarros_feijao.txt” -> “/home/est/acn13/maquina2/meu1repo/diasbarros_feijao.txt”
```


```bash
## Baixa o arquivo.
wget 'http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt'
```


```
--2015-10-01 16:37:02--  http://www.leg.ufpr.br/~walmes/data/diasbarros_feijao.txt
Resolving www.leg.ufpr.br (www.leg.ufpr.br)... ???.??.???.??
Connecting to www.leg.ufpr.br (www.leg.ufpr.br)|???.??.???.??|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 487 [text/plain]
Saving to: ‘diasbarros_feijao.txt’

     0K                                                       100% 40,2M=0s

2015-10-01 16:37:02 (40,2 MB/s) - ‘diasbarros_feijao.txt’ saved [487/487]
```


```bash
git status
```

```
No ramo feature04
Arquivos não monitorados:
  (utilize "git add <arquivo>..." para incluir o que será submetido)

	diasbarros_feijao.txt

nada adicionado ao envio mas arquivos não registrados estão presentes (use "git add" to registrar)
```


```bash
git add diasbarros_feijao.txt
git commit -m "Dados de experimento com feijão."
```

```
[feature04 18912c0] Dados de experimento com feijão.
 Committer: Teste <acn13@inf.ufpr.br>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 37 insertions(+)
 create mode 100644 diasbarros_feijao.txt
```


```bash
git push origin feature04
```

```
To /media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo/.git
 * [new branch]      feature04 -> feature04
```

Volta para origem e verifica o que recebeu de contribuição.


```bash
pwd
```

```
/media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo
```


```bash
git status
```

```
No ramo master
nada a submeter, diretório de trabalho vazio
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
Updating f44bbdf..18912c0
Fast-forward
 diasbarros_feijao.txt | 37 +++++++++++++++++++++++++++++++++++++
 1 file changed, 37 insertions(+)
 create mode 100644 diasbarros_feijao.txt
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 18912c0 (HEAD, master, feature04) Dados de experimento com feijão.
*   f44bbdf Resolve conflito, trunca com caixa alta.
|\  
| * 981d1ee (feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 7546ee7 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   9bf4962 Merge branch 'feature02'
|\  
| * eb21436 Adiciona aquivo de dados de experimento com rações.
* | 6737802 Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
```


```bash
pwd
```

```
/home/est/acn13/maquina2/meu1repo
```


```bash
git pull origin master
```

```
From /media/acn13/- Arquivos -/Projetos_GIT/apostila-git/meu1repo/
 * branch            master     -> FETCH_HEAD
   f44bbdf..18912c0  master     -> origin/master
Already up-to-date.
```


```bash
git log --graph --oneline --decorate --date=relative --all
```

```
* 18912c0 (HEAD, origin/master, origin/feature04, origin/HEAD, feature04) Dados de experimento com feijão.
*   f44bbdf (master) Resolve conflito, trunca com caixa alta.
|\  
| * 981d1ee (origin/feature03) Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.
* | 7546ee7 Arquivo de experimento em BIB. Cabeçalho em caixa alta.
|/  
*   9bf4962 Merge branch 'feature02'
|\  
| * eb21436 Adiciona aquivo de dados de experimento com rações.
* | 6737802 Arquivo sobre copa 2014 celeção brasileira.
* | 294a431 Adiciona função R para VIF.
|/  
* e57eeaf Novos argumentos.
* 28205ac Adiciona frase do Linux Torvalds.
* 68a99fc Lista de inicial de o porquê usar o Linux.
* e248651 Cria arquivo com título.
```


```bash
git log --stat
```

```
commit 18912c0e8b397bbb1e0b22e9710bb6061c317725
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:02 2015 -0300

    Dados de experimento com feijão.

 diasbarros_feijao.txt | 37 +++++++++++++++++++++++++++++++++++++
 1 file changed, 37 insertions(+)

commit f44bbdf3d63290cdd205a1fe5908413e63a660cd
Merge: 7546ee7 981d1ee
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Resolve conflito, trunca com caixa alta.

commit 7546ee745916c955baec2e6116ffccc9f6cdf443
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Arquivo de experimento em BIB. Cabeçalho em caixa alta.

 bib1.txt | 58 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 58 insertions(+)

commit 981d1eed5a20f296261cab67aaea499ecbc6ac05
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Arquivo de experimento em BIB. Trunca cabeçalho 4 digitos.

 bib1.txt | 58 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 58 insertions(+)

commit 9bf49622914702c9b2de0006217792609bebca0b
Merge: 6737802 eb21436
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Merge branch 'feature02'

commit 67378029fe8eed356c99df88db746a73e9c9d8ad
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Arquivo sobre copa 2014 celeção brasileira.

 brasilCopa2014.txt | 22 ++++++++++++++++++++++
 1 file changed, 22 insertions(+)

commit eb21436153d68107dacd3e47aca77773b91a1f42
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Adiciona aquivo de dados de experimento com rações.

 pimentel_racoes.txt | 24 ++++++++++++++++++++++++
 1 file changed, 24 insertions(+)

commit 294a43144efcf8c7aab402eab86920ae55af1647
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:59 2015 -0300

    Adiciona função R para VIF.

 vif.R | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)

commit e57eeaff9e77da94b22e5da043676a3cf70ed0b1
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:59 2015 -0300

    Novos argumentos.

 porqueLinux.txt | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

commit 28205ac71a0e20ee32673e9883226eb25c3053d7
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:59 2015 -0300

    Adiciona frase do Linux Torvalds.

 README.txt | 4 ++++
 1 file changed, 4 insertions(+)

commit 68a99fcb5cd57195651f99f7a4e35bb8c0a0acfb
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:59 2015 -0300

    Lista de inicial de o porquê usar o Linux.

 porqueLinux.txt | 5 +++++
 1 file changed, 5 insertions(+)

commit e2486515a9e75bf8e9e2e38e63e557c32ad887bf
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:36:58 2015 -0300

    Cria arquivo com título.

 README.txt | 1 +
 1 file changed, 1 insertion(+)
```


```bash
git log -p -2
```

```
commit 18912c0e8b397bbb1e0b22e9710bb6061c317725
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:02 2015 -0300

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

commit f44bbdf3d63290cdd205a1fe5908413e63a660cd
Merge: 7546ee7 981d1ee
Author: Teste <acn13@inf.ufpr.br>
Date:   Thu Oct 1 16:37:00 2015 -0300

    Resolve conflito, trunca com caixa alta.
```



****
## Ignorando arquivos e diretórios

Há momentos em que é necessário a criação de arquivos e pastas, dentro do 
repositório git, que não devem ser versionados, como é o caso de uma 
compilação Latex, que gera arquivos auxiliares que não é preciso deixar 
disponível a terceiros. Para esse intuito, o git possui um recurso que permite
que arquivos e pastas fiquem "invisíveis" para o software.

Para que isso ocorra, é indispensável a criação de um arquivo com extensão 
`.gitignore`, que o git irá reconhecer e efetuar leitura a procura de 
pastas e arquivos a ignorar. Dentro deste arquivo, é imprescindível que seja
escrito, por linha, somente um nome de pasta ou arquivo a ser ignorado.

### Padrões de formatos para o `.gitignore`

* Linhas em branco não são lidas, servindo apenas como modo de separar e 
organizar o arquivo.

* Os caracteres ` # ` e ` ! ` são reservado do git. Para pastas ou arquivos
que os nomes comecem com ` # ` (Exemplo: #git.txt) ou ` ! ` (Exemplo: !git.txt), 
deve-se usar uma barra invertida na frente do padrão (Exemplo: \\#ddd.txt, \\!ddd.txt).

* O caracter ` # ` serve para efetuar comentários, ou seja, a linha que iniciar com `#`
não será interpretada pelo git.

* O caracter `!` serve para negar um padrão, por exemplo, pode-se mandar o git 
ignorar todos os arquivos de determinada pasta (Usando: Nome_Dir/*),
mas deixar de ignorar um arquivo específico dentro dela 
(Exemplo: !Nome_Dir/Arquivo.txt).

* O asterisco ` * ` pode ser usado para substituir parte do nome de 
arquivos e pastas, ou o nome inteiro. Isso é valido também para a 
extensão do arquivo.

* Um diretório pode ser ignorado adicionando seu nome e uma barra ao final deste.

* Dois asteriscos ` ** ` podem ser usados para substituir caminhos de subpastas, 
como por exemplo, para ignorar o diretório Subpasta, 
o caminho `/Exercicio/Teste/Pasta/Subpasta/` pode ser substituido por `/**/Subpasta/`.


### Exemplo

O código abaixo é um exemplo de um arquivo com extensão `.gitignore`:


```sh
# Esta linha é um comentário.

# Ignorando arquivos com extensão .aux menos o arquivo EXEMPLO.aux:

*.aux
!EXEMPLO.aux

# Ignorando todos os arquivos com nome EXEMPLO:

EXEMPLO.*
  
# Ignorando arquivos que possuam HTML no nome:
  
HTML*.*
  
# Ignorando as Subpastas e os arquivos da pasta DIR:
  
DIR/*

# Não ignorar apenas a Subpasta1 da pasta DIR:
  
!DIR/Subpasta1/
  
```

Vale ressaltar que, no exemplo acima, por mais que esteja sendo ignorado arquivos 
com o nome EXEMPLO, e arquivos com extensão .aux, 
o arquivo EXEMPLO.aux (que está pecedido do sinal `!`) não será ignorado.

### Tornando Global

Cada vez que cria-se um novo projeto, para que arquivos sejam ignorados, 
deve-se criar um novo arquivo `.gitignore`. Para que isso não ocorra, e 
possível configurar o arquivo globalmente, ou seja, ele estará incorporado
as configurações do git do seu computador.



```sh
git config --global core.excludesfile ~/.gitignore_global
```

 Depois de executar o código acima, o `.gitignore` da pasta atual 
 (pasta do seu projeto) será atribuido como global no arquivo de 
 configuração do git (`.gitconfig`).

 Uma observação importante a ser feita é que, se adicionado arquivos para
 serem ignorados globalmente, como arquivos PDF (Usando: *.pdf), por exemplo,
 todos os arquivos  com essa extensão serão ignorados pelo git,
 não somente os do projeto atual. 
 Portanto, é recomendado somente definir um `.gitignore` como global, 
 se ele apenas desconsiderar arquivos auxiliares, ou seja, que não serão necessários
 para compilações futuras.

****
## Autenticando em contas do GitLab (c3sl) e GitHub

Os procedimentos dessa sessão tem o objetivo de promover o conexão da
sua máquina de trabalho com sua conta no GitLab do c3sl (alunos UFPR) ou
conta do GitHub. Assume-se, logicamente, que você tenha conta em algum
desses serviços. Caso você não tenha uma conta em algum serviço de
hospedagem de repsitório Git, seguem algumas opções:

  * GitHub: <https://github.com/>
  * GitLab: <https://about.gitlab.com/>
  * Bitbucket: <https://bitbucket.org/>

Uma comparação entre os serviços disponíveis para Git está disponível em
[git-hosting-services-compared][].

Abra o terminal em qualquer diretório. Não precisa ser um diretório
Git. Aqui será criado um par de chaves, que nada mais são que longas
cadeias de caracteres, de forma que elas formam um par
chave/cadeado. A pública (a chave) é copiada para o servidor. A privada
fica na sua máquina. Dessa maneira, a comunicação para transferência de
dados entre as máquinas pode ser feita.

Será solicitado uma senha (`passphrase`). Você pode forncer uma ou
apenas pressionar `Enter` para correr o procedimento padrão. O resultado
é uma senha gráfica ASCII além de gerar os arquivos (chaves) cujo
caminho é informado no *output*.


```sh
## keygen (chave gerar). rsa é o tipo.
ssh-keygen -t rsa -C "batman@justiceleague.org"
```

```
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

O importante é o conteúdo do arquivo `/home/batman/.ssh/id_rsa.pub`, a
sua chave pública. Este deve ser fornecido ao GitLab (ou GitHub) em uma
janela com as chaves. Os endereços abaixo levam para a mencionada
janela. Requer que esteja logado.

  * GitLab: <http://gitab.c3sl.ufpr.br/profile/keys>
  * GitHub: <https://github.com/settings/ssh>

Nessa janela deverá ser informado o código gerado pelo
`ssh-keygen`. Você deve copiar o texto do arquivo
`/home/batman/.ssh/id_rsa.pub`, sem moficá-lo, e fornecer ao GitLab.
Para ver/abrir o conteúdo do arquivo no próprio terminal use `less` ou
`cat`. Para copiar do terminal use `ctrl+shift+c`. Para abrir com um
editor de texto, o `gedit` por exemplo, é só passar o nome do arquivo.

```sh
## Abre o arquivo com o editor de texto Gedit.
gedit /home/batman/.ssh/id_rsa.pub

## Mostra o conteúdo do arquivo no próprio terminal.
less /home/batman/.ssh/id_rsa.pub  
```

```
ssh-rsa BBBBB3NzaC1yc2EAAAADAQABAAABAQDDuQmvkQ0WgwYQvR16z37tG37Q61ID+Qf4hi8+cARjjSWP7015CAtRnCvmGFSbdFMjz3ZEkp2XzHIyRCKw2hLP57rkFcfioWra6N5/9+z+tPiwr2OzwLfk7J/GAETGA4rtoToV96hf5RvKRhvuqyO5uf5ouBILm1PRpjA/5AkfToWp25/7WC136eGIOSJMFgQ3OuK5U+qSXAwuSdu9Uj1XkVYFDjasA45ZjsnkE6L9bKiYymadshEbWEBHJAWqDErd8srMtBYS/2hodNnjfH7rNHHCo8wZD5GJFz7YUodaBSaSYuHVfrEryaEm/r5787CAiecFAjWEeVq6StM7N/lz batman@justiceleague.org
```

Para conferir a comunicação da sua máquina com o servidor do GitLab do
c3sl ou do GitHub, aplique a instrução `ssh` abaixo.

```sh
## Com gitlab do c3sl.
ssh -T git@gitlab.c3sl.ufpr.br
```

```
Welcome to GitLab, Knight Rider!
```

```sh
## Com github.
ssh -T git@github.com
```

```
Hi batman! You've successfully authenticated, but GitHub does not provide shell access.
```

Em caso de obter uma mensagem não positiva, repita o comando com a opção
`-v` para um log do procedimento.

```sh
## Com gitlab do c3sl.
ssh -vT git@github.com
```

```
OpenSSH_6.6.1, OpenSSL 1.0.1f 6 Jan 2014
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: Applying options for *
debug1: Connecting to github.com [192.30.252.130] port 22.
debug1: Connection established.
debug1: identity file /home/batman/.ssh/id_rsa type 1
debug1: identity file /home/batman/.ssh/id_rsa-cert type -1
debug1: identity file /home/batman/.ssh/id_dsa type -1
debug1: identity file /home/batman/.ssh/id_dsa-cert type -1
debug1: identity file /home/batman/.ssh/id_ecdsa type -1
debug1: identity file /home/batman/.ssh/id_ecdsa-cert type -1
debug1: identity file /home/batman/.ssh/id_ed25519 type -1
debug1: identity file /home/batman/.ssh/id_ed25519-cert type -1
debug1: Enabling compatibility mode for protocol 2.0
debug1: Local version string SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu2.3
debug1: Remote protocol version 2.0, remote software version libssh-0.7.0
debug1: no match: libssh-0.7.0
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: server->client aes128-ctr hmac-sha1 none
debug1: kex: client->server aes128-ctr hmac-sha1 none
debug1: sending SSH2_MSG_KEX_ECDH_INIT
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: RSA 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48
debug1: Host 'github.com' is known and matches the RSA host key.
debug1: Found key in /home/batman/.ssh/known_hosts:1
debug1: ssh_rsa_verify: signature correct
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: Roaming not allowed by server
debug1: SSH2_MSG_SERVICE_REQUEST sent
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey
debug1: Next authentication method: publickey
debug1: Offering RSA public key: /home/batman/.ssh/id_rsa
debug1: Server accepts key: pkalg ssh-rsa blen 279
debug1: Authentication succeeded (publickey).
Authenticated to github.com ([192.30.252.130]:22).
debug1: channel 0: new [client-session]
debug1: Entering interactive session.
debug1: Sending environment.
debug1: Sending env LC_PAPER = pt_BR.UTF-8
debug1: Sending env LC_ADDRESS = pt_BR.UTF-8
debug1: Sending env LC_MONETARY = pt_BR.UTF-8
debug1: Sending env LC_NUMERIC = pt_BR.UTF-8
debug1: Sending env LC_TELEPHONE = pt_BR.UTF-8
debug1: Sending env LC_IDENTIFICATION = pt_BR.UTF-8
debug1: Sending env LANG = en_US.UTF-8
debug1: Sending env LC_MEASUREMENT = pt_BR.UTF-8
debug1: Sending env LC_TIME = pt_BR.UTF-8
debug1: Sending env LC_NAME = pt_BR.UTF-8
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
Hi batman! You've successfully authenticated, but GitHub does not provide shell access.
debug1: channel 0: free: client-session, nchannels 1
Transferred: sent 3856, received 1784 bytes, in 0.4 seconds
Bytes per second: sent 10261.9, received 4747.7
debug1: Exit status 1
```

### Requisições de mescla

### Colaborando via fork

****
## Modelos de fluxos de trabalho

<!--
Inspiração:

https://git-scm.com/book/pt-br/v1/Git-Distribu%C3%ADdo-Fluxos-de-Trabalho-Distribu%C3%ADdos
http://imasters.com.br/gerencia-de-ti/fluxo-de-desenvolvimento-com-gitflow/
http://www.magentonapratica.com.br/2014/07/um-modelo-bem-sucedido-de-ramificacao.html
-->

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
[git-hosting-services-compared]: http://www.git-tower.com/blog/git-hosting-services-compared/
