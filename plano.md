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
   4. Macanísmos de colaboração
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
      4. Resolver confito de merge
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
2. 2015-11-03:
   + Walmes: terminar o que tem para ser feito para GitHub, adicionar
     chaves, verificar conexão, criar renomear projeto, clonar,
     modificar e subir. Renomear, deletar e transferir projeto.
   + Gabriel: Descrever o usdo do `init`, `add`, `commit`, definir as
     três áreas de presença das modificações e acompanhar modificações
     com `diff`, `log`, `status` e `reflog`.
   + Ângela: Incluir as ilustrações dos modelos de workflow.
   + Jhenifer: migrar o conteúdo sobre instalação e configuração da
     versão preliminar da apostila correspondentes à Linux e Windows.
   + Eduardo: concluir as seções sobre uso da `git gui`, `gitk`, `gitg`
     e `gitx`.
   + Alessandra: configurar conexão serviador via ssh, criar e
     transferir as chaves públicas, criar um repositório no servidor e
     cloná-lo.
   + Alcides: concluir o dicionário de termos.
   + Daniel: concluir o conteúdo do *cheat sheet*.
3. 2015-11-10:
   + Walmes: escrever para o GitLab o mesmo contúdo para presente para o
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
4. 2015-11-17:
   + Walmes: descrever os mecanísmos de colaboração com interfaces web:
     issue, fork e merge request.
   + Gabriel: Acréscimos de revisão do capítulo. Revisar os apêndices do
     Alcides.
   + Ângela: Descrever o fluxo de trabalho do PET. Revisar o capítulo da
     Jhenifer.
   + Jhenifer: Acrécimos de revisão. Revisão do capítulo da Alessandra.
   + Eduardo: Documentar o uso das ferramentas de merge: meld, kdiff3 e
     p4merge.
   + Alessandra: Acréscismos e revisão. Revisar o capítulo da Ângela.
   + Alcides: Acréscismos e revisão. Revisar o capítulo do Gabriel.
   + Daniel: **finalizar todo o trabalho da semana anterior**. Concluir
     o capítulo sobre Git com o RStudio
5. 2015-11-24:
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
6. 2015-12-01:
   + TODOS: colocar as figuras em ambiente Latex (`center > figure >
     includegraphics + caption`). Controlar o tamanho das figuras para
     não ultrapassarem as margens nem ficarem pequenas demais. Colocar
     os links com âncoras (os não presentes no texto, como
     `[google](http://www.google.com)`) em
     `google\footnote{\url{http://www.google.com}}` para aparecer no
     rodapé das páginas. Usar seções numeradas.
7. 2015-12-08:
8. 2015-12-15: Apostila Git concluída!

