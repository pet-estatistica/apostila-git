# Apostila de Git

## Conteúdo previsto

1. Sistemas de controle de versão
   1. Por que versionar?
   2. Git
   3. ...
2. Instalação e configuração
   1. O que instalar
   2. Instalação em
      1. Windows
      2. Linux (Debian, Arch, Fedora, ...)
      3. Mac
   3. Configurando perfil
3. Projetos locais
   1. init, add, commit, branch, merge, checkout, reset
   2. ...
4. Projetos remotos
   1. Configuração de conexão ssh com servidor
   2. Chaves públicas
   3. clone, push, pull, fetch
5. Serviços web para Git
   1. Serviços
      1. GitHub
      2. GitLab
      3. Outros
   2. Criar perfil
      1. Habilitar comunicação
      2. Gerenciar repositórios
   3. Fluxo de trabalho
   4. Mecanismos de colaboração
      1. Issues e merge request
      2. Fork e pull request
   5. Integração contínua
6. Ferramentas gráficas
   1. Git GUI
   2. Gitk, Gitg, Giggle
   3. Meld, Kdiff3
   4. Plugins para Geany, Gedit, Nautilus, Nemo
   5. Emacs??
7. Git no Rstudio
   1. Interface
   2. Configuração
   3. Gestionando Projeto
8. Trabalhando em equipe
   1. Boas práticas de colaboração
   2. Modelos de fluxos de trabalho
   3. Fluxo de trabalho PET no GitLab
9. Apêndice
   1. Dicionário de termos
   2. Cheat sheet
   3. Exemplos de rotinas
      1. Clonar, modificar e subir
      2. Resolver um bug
      3. Incorporar o remoto ao local
      4. Resolver conflito de merge
      5. Voltar o projeto para um commit
      6. Deletar ramos
      7. Criar ramo de um commit passado
      8. Rescrever uma mensagem de commit
      9. ...

## Produto e prazo

  + Tipo de arquivo final: Apostila em pdf com capa, folhas de rosto,
    prefácio, sumário, capítulos e apêndices.
  + Prazo para o produto final: 2015-12-15.

## Afazeres

1. 2015-10-27 [week01]:
   + Ângela, Gabriel, Jhenifer e Alessandra: Criar o *milestone* (MS),
     criar o primeiro *issue* (IS) e adicionar arquivo com o anteprojeto
     (AP), que são as seções se subseções acompanhadas de um breve
     descritivo.
   + Eduardo: transferir o `issue#4` para um IS novo em sua MS e
     adicionar o AP.
   + Daniel: Criar MS e IS com arquivo de AP para o capítulo 1, RStudio
     e *Cheat Sheet*.
   + Walmes: Deixar pronto o conteúdo referente ao GitHub dentro do
     capítulo 5.
2. 2015-11-03 [week02]:
   + Walmes: terminar o que tem para ser feito para GitHub, adicionar
     chaves, verificar conexão, criar renomear projeto, clonar,
     modificar e subir. Renomear, deletar e transferir projeto.
   + Gabriel: Descrever o uso do `init`, `add`, `commit`, definir as
     três áreas de presença das modificações e acompanhar modificações
     com `diff`, `log`, `status` e `reflog`.
   + Ângela: Incluir as ilustrações dos modelos de workflow.
   + Jhenifer: migrar o conteúdo sobre instalação e configuração da
     versão preliminar da apostila correspondentes à Linux e Windows.
   + Eduardo: concluir as seções sobre uso da `git gui`, `gitk`, `gitg`
     e `gitx`.
   + Alessandra: configurar conexão servidor via ssh, criar e
     transferir as chaves públicas, criar um repositório no servidor e
     cloná-lo.
   + Alcides: concluir o dicionário de termos.
   + Daniel: concluir o conteúdo do *cheat sheet*.
3. 2015-11-10 [week03]:
   + Walmes: escrever para o GitLab o mesmo conteúdo para presente para o
     GitHub. Isso vai de uma breve descrição das funcionalidades, como
     criar conta e gerenciar um repositório.
   + Gabriel: **finalizar o trabalho da semana anterior**. Escrever
     sobre o uso de *branches*, *checkout* e *merge*.
   + Ângela: fazer revisão, acréscimos e acabamento.
   + Jhenifer: escrever sobre configurações pessoais: aliases para o
     Git, para o sistema operacional e como ignorar arquivos.
   + Eduardo: **finalizar o trabalho da semana anterior**. Documentar o
     uso da gitk, gitg e gitx para assim terminar a parte de interfaces
     de execução e exibição com Git.
   + Alessandra: Correções e acréscimos.
   + Alcides: Concluir os exemplos de rotinas. Revisar o capítulo da
     Jhenifer.
   + Daniel: Definir o conteúdo previsto no *cheat sheet* e concluir o
     capítulo sobre SCV. Revisar o capítulo da Ângela.
4. 2015-11-17 [week04]:
   + Walmes: descrever os mecanismos de colaboração com interfaces web:
     issue, fork e merge request.
   + Gabriel: Acréscimos de revisão do capítulo. Revisar os apêndices do
     Alcides.
   + Ângela: Descrever o fluxo de trabalho do PET. Revisar o capítulo da
     Jhenifer.
   + Jhenifer: Acréscimos de revisão. Revisão do capítulo da Alessandra.
   + Eduardo: Documentar o uso das ferramentas de merge: meld, kdiff3 e
     p4merge.
   + Alessandra: Acréscimos e revisão. Revisar o capítulo da Ângela.
   + Alcides: Acréscimos e revisão. Revisar o capítulo do Gabriel.
   + Daniel: **finalizar todo o trabalho da semana anterior**. Concluir
     o capítulo sobre Git com o RStudio
5. 2015-11-24 [week05]:
   + Gabriel: Concluir a revisão **pendente** do próprio capítulo e
     revisar o capítulo da Ângela que foi assumido pelo Daniel.
   + Ângela: Corrigir o que estiver disponível do capítulo do Walmes.
   + Jhenifer: Corrigir o que estiver disponível do capítulo do Eduardo.
   + Alessandra: Fazer uma leitura e revisão do próprio capítulo para
     deixá-lo mais claro.
   + Eduardo: Incluir screenshots das GUI para Git que ficou
     **pendente** e revisar o capítulo do Gabriel.
   + Alcides: Finalizar a correção do capítulo do Gabriel que ficou
     **pendente** e colecionar exemplos de rotinas disponíveis em todos
     os capítulos e incluir nos Exemplos de Rotina.
   + Walmes: Escrever sobre o fluxo de trabalho e integração contínua.
   + Daniel: Concluir o trabalho **acumulado de 2 semanas** e assim
     concluir sobre Sistemas de Controle de Versão, *Cheat Sheet* e uso
     de Git no RStudio.
6. 2015-12-01 [week06]:
   + TODOS: colocar as figuras em ambiente Latex (`center > figure >
     includegraphics + caption`). Controlar o tamanho das figuras para
     não ultrapassarem as margens nem ficarem pequenas demais. Colocar
     os links com âncoras (os não presentes no texto, como
     `[google](http://www.google.com)`) em
     `google\footnote{\url{http://www.google.com}}` para aparecer no
     rodapé das páginas. Usar seções numeradas. Considerar como exemplo
     o YAML do arquivo `cap05.Rmd`.
   + Walmes: Fazer revisão completa do capítulo 5 até sexta para o
     Alcides. Disponibilizar o template para cada um fazer os ajustes
     finais no seu capítulo.
   + Alessandra: Corrigir o capítulo 1.
   + Daniel: Concluir o capítulo de RStudio e o *Cheat Sheet*
     (**pendencias**). Revisar o dicionário de termos e exemplos de
     rotinas.
   + Gabriel: Fazer revisão e acréscimos no capítulo 3 e disponibilizar
     até sexta para o Eduardo.
   + Jhenifer: Corrigir o capítulo do Eduardo que será disponibilizado
     na sexta.
   + Ângela: Corrigir o capítulo de RStudio disponibilizado na sexta.
   + Eduardo: Revisar o capítulo 6 até sexta para a Jhenifer. Corrigir o
     capítulo 3 depois de sexta.
   + Alcides: Corrigir o capítulo 5 disponibilizado na sexta.
   + Quem se interessar: Pensar numa capa para a apostila, fazer esboço,
     *brainstorm*.
7. 2015-12-08 [week07]:
   + Alcides: Terminar de corrigir o cap 5 (**pendencia**) e colocar o
     dicionário de termos em um ambiente LaTex apropriado.
   + Alessandra: Fazer adequações no capítulo 4 e depois de sexta
     corrigir o capítulo 6.
   + Ângela: Corrigir o capítulo de RStudio.
   + Daniel: Concluir todas as **pendências** (RStudio e *Cheat Sheet*),
     disponibilizar o capítulo de RStudio o quanto antes para Ângela.
   + Eduardo: Expandir o exemplo de rotinas e depois de sexta corrigir o
     capítulo 3.
   + Jhenifer: Concluir correção no capítulo 6 (**pendencia**).
   + Gabriel: Disponibilizar o capítulo 3 para o Eduardo até sexta.
   + Walmes: Juntar todos os capítulos e gerar a Apostila Git.
8. 2015-12-15: Apostila Git concluída!
   + Daniel: Não concluiu nenhum dos compromissos assumidos. As
     pendências devem ser incorporadas na segunda fase do Projeto.
   + Gabriel: Enviou de forma inacabada os compromissos que assumiu;
   + Ângela: Fez a capa. Concluiu a primeira fase da apostila sem nenhuma
     pendência;
   + Jhenifer: Concluiu a primeira fase da apostila sem nenhuma
     pendência;
   + Walmes: Concluiu a primeira fase da apostila sem nenhuma pendência;
   + Eduardo: Concluiu com tudo em dia
   + Alessandra: Concluiu a primeira fase da apostila sem nenhuma
     pendência;
   + Alcides: Fez as modificações mas não pediu MR.

[week01]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week01
[week02]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week02
[week03]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week03
[week04]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week04
[week05]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week05
[week06]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week06
[week07]: https://gitlab.c3sl.ufpr.br/pet-estatistica/apostila-git/commits/week07
