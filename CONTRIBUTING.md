Guia de contribuição
====================

Esse é um projeto público do PET Estatística e aberto a
colaboradores. Para que a colaboração seja bem sucedida, seguem algumas
intruções e recomendações.

## O funcionamento

O núcleo do tutorial é o arquivo `git_tuto.Rmd`. O arquivo `Rmd` é
marcado por ser escrito com sintaxe [markdown][] com fragmentos de
código R. Os fragmentos de código R são interpretados durante a
compilação feita com a função `render` do pacote [rmarkdown][]. Por ser
escrito em markdown, o tutorial pode ser transformado em formatos de
saída como markdown (`.md`), html e até PDF.

Apesar de `Rmd` normalmente ter fragmentos de código R, nesse tutorial
predominam fragmentos de código shell, em outras palavras, são
fragmentos de código executados do terminal do Linux. Para ter um
fragmento de código shell que seja interpretado na compilação, tem-se
que fazê-lo conforme abaixo.

    ```{r, engine="sh"}
    comando shell
    ```

A compilação desse documento cria sempre um projeto Git do zero. Com
intruções do shell ao longo do documento, no instante da compilação,
arquivos são criados, adicionados (`git add`), commitados (`git
commit`), moficados, etc. Esse domento é, portanto, um documento
reproduzível.

Para compilar o documento você deve abrir uma sessão R onde o diretório
de trabalho é o que contém o arquivo `git_tuto.Rmd` e rodar uma chamada
da função render. Usuários do RStudio poder fazer isso diretamento pelo
botão de compilar na barra de ferramentas.

    ```{r, engine="sh"}
    library(rmarkdown)

    render("git_tuto.Rmd")
    ```

Você sempre deve remover os diretórios criados durante a compilação para
compilar novamente. Isso porque o projeto cria tudo de novo e é essa a
intenção, apensar do custo em recriar tudo. Se os diretórios não forem
deletados antes de uma nova compilação, você irá receber erros de
compilação.

Esse documento usa instruções no terminal que podem ser particulares do
Linux, como o comando `tree` e `sed`. Portando, a reprodutibilidade da
compilação pode não acontecer em outros sistemas operacionais.

## O fluxo de trabalho

Esse projeto terá dois ramos persistentes:

  * `devel`: é o ramo que irá imediatamente recever a contribuição dos
    membros e será submetido a teste (no caso compilação). Se bem
    sucedido, a contribuição é movida para o ramo `master`.
  * `master`: é o da versão estável do projeto.

Os membros devem criar ramos de demanda para adicionarem suas
contribuições. Por se existe a demanda de acrescentar uma sessão sobre o
uso do programa `meld` para resolver conflitos de merge, deve-se criar
um ramo para isso, adicionar as contribuições e subir esse ramo para o
repositório remoto.

```sh
git branch -b usaMeld

... trabalha, git add, git commit ...
... trabalha, git add, git commit ...
... trabalha, git add, git commit ...

git push origin usaMeld
```

Assim que der o `git push`, a próxima etapa é fazer uma requisição de
merge que se dá pela interface do GitLab clicando em [merge request][]
no menu da esquerda, dentro da página do projeto. Lá é inde se designa o
responsável por avaliar e fazer o merge.

## Mensagens de commit

É extremamente recomendado, por questões de organização e produtividade,
que as mensagens de commit sejam apropriadas. Não use mensagens vagas ou
óbvias do tipo *Modificações feitas*, *Arquivos incluídos*. Procure algo
como *Incluí arquivo de estilo CSS*, *Modifica preâmbulo*, *Troca
'require' por 'library'* ([5 dicas para melhores commits][]).

Exitem formas especiais de escrever um *commit* que tenha ações do
repositório remoto como fechar um *issue* ou fazer uma referência a
outro *commit* ([ações nas mensagens de commit][]). As palavras
especiais são: `close`, `closes`, `closed`, `fix`, `fixes`, `fixed`,
`resolve`, `resolves`, `resolved`. Depois das palavras vem uma
identificação de *issue* ou *sha1*.

```sh
git commit -m "Close #4. Bug devido ao encoding."
```

## Escrita do código

Recomensa-se fortemente que ao escrever o código, não se ultrapasse 72
caracteres por linha. Isso torna o texto/código mais legível nos
arquivos fontes. Linhas longas nos monitores atuais que são grandes são
realmente difíceis de ler.

Editores de texto (de verdade) geralmente possuem formas de auto quebrar
linhas, auto indentar/acomodar ou sinalizar a margem direita. O Emacs
tem [auto break lines][] e [refluxo de texto][]. Outros editores
permitem exibir uma linha vertical para indicar o limite, como o RStudio
(> Tools > Global Options > Code > Display > Margin column).

[markdown]: http://br-mac.org/2013/09/o-que-e-markdown.html
[rmarkdown]: http://rmarkdown.rstudio.com/
[merge request]: https://gitlab.c3sl.ufpr.br/pet-estatistica/git-tutorial/merge_requests
[ações nas mensagens de commit]: https://help.github.com/articles/closing-issues-via-commit-messages/
[5 dicas para melhores commits]: https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message
[auto break lines]: http://emacswiki.org/emacs/LineWrap
[refluxo de texto]: http://www.emacswiki.org/emacs/FillParagraph
