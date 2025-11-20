# Primeiros comandos

Antes de começarmos a usar o Git, precisamos entender alguns conceitos e comandos fundamentais.
Vamos aprender como iniciar um repositório, acompanhar as mudanças nos arquivos e registrar alterações com commits de forma simples e organizada.

## Iniciando um repositório

A primeira coisa que devemos fazer é ir até o diretório onde vamos iniciar nosso projeto. Podemos acessar esse local usando o Git Bash.
Mas atenção: no Git Bash, o formato dos caminhos é um pouco diferente do utilizado no Windows. No exemplo abaixo acessamos o disco local C.

Veja um exemplo de como acessar o diretório desejado:
```
cd /c/pasta01/pasta02
```

Após isso, inicialize o repositório usando o seguinte comando:
```
git init
```

Esse comando cria uma pasta oculta chamada **.git**, onde o Git armazena todo o histórico e as informações internas do seu projeto.

Assim que o repositório é iniciado, qualquer arquivo novo ou modificado passa a ser identificado pelo Git.
A partir desse momento, esses arquivos percorrem algumas etapas antes de serem registrados no histórico do repositório.

Working Directory (ou Diretório de Trabalho):
É a pasta do projeto no seu computador, onde você abre, cria, edita e exclui arquivos.
Quando você altera ou adiciona um arquivo, o Git detecta essa mudança, mas ainda não a registra.
Podemos verificar o status usando o seguinte comando:
```
git status
```

O Git pode exibir uma das seguintes mensagens:
- Untracked files: são arquivos novos que ainda não fazem parte do controle de versão.
- Changes not staged for commit: arquivos já rastreados que foram modificados, mas ainda não foram adicionados ao próximo commit.

Ou seja, essas alterações ainda não estão no **Staging Area** e, portanto, não serão incluídas em um commit até que você as adicione manualmente.

Para adicionar um arquivo específico, usamos o comando seguido do nome do arquivo e sua extensão. Por exemplo:
```
git add index.html
```

Se quiser adicionar todos os arquivos novos e modificados de uma só vez, use:
```
git add .
```

Depois de executado o comando, os arquivos passam para a **Staging Area** (ou área de preparação).
Você pode pensar nela como uma “sala de espera”: apenas os arquivos que estão nessa área serão incluídos no próximo commit.
Ou seja, eles já foram selecionados e estão prontos para serem registrados no histórico do repositório.

---

## Registrando com um commit

Um commit é como um ponto de salvamento permanente no seu projeto.
Ele registra o estado dos arquivos que estão na **Staging Area** em um momento específico,
o que permite acompanhar o histórico das alterações e voltar a versões anteriores sempre que necessário.

Para registrar as alterações em um commit, podemos utilizar o seguinte comando:
´´´
git commit
´´´

Isso fará com que o Git abra um editor de texto padrão para que você digite a mensagem do seu commit, pois ela é obrigatória.
Mas, se quiser algo mais simples e rápido, com a mensagem já embutida, use:
´´´
git commit -m "sua mensagem"
´´´

Caso queira adicionar uma descrição um pouco maior, use o seguinte comando:
```
git commit -m "Sua mensagem" -m "Descrição mais detalhada"
```

Onde o primeiro `-m` se refere ao título e o segundo `-m` se refere ao corpo do commit.

Caso você tenha aberto o editor de texto e queira adicionar uma mensagem detalhada, siga esta estrutura:
- Na primeira linha, escreva o título do commit.
- Na segunda linha, deixe um espaço em branco, para que o Git entenda a separação.
- Na terceira linha, escreva a descrição detalhada das suas modificações.

Se você quiser desfazer as alterações feitas em um arquivo específico e voltar ao estado registrado no último commit, use, por exemplo:
```
git restore arquivo.html
```

> Atenção: esse comando descarta todas as mudanças feitas no arquivo desde o último commit. Elas não poderão ser recuperadas.

Se você quiser apenas remover um arquivo da **Staging Area**, mas manter suas alterações no diretório de trabalho, use:
```
git restore --staged arquivo.html
```

Nesse caso, o arquivo volta para o **Working Directory**, pronto para ser editado, mas não será incluído no próximo commit até ser adicionado novamente com `git add`.

---

## Git e GitHub

Podemos trabalhar com um repositório de duas maneiras: enviando um projeto que já existe na sua máquina para um repositório remoto ou
fazendo o caminho inverso, clonando um repositório remoto para o seu computador. Vamos ver primeiro como subir um projeto para o GitHub:

No GitHub, você deve criar um repositório vazio, sem nenhum arquivo.
Não marque as opções para adicionar `README.md`, `.gitignore` ou `LICENSE`.
Depois que o repositório estiver criado, será necessário conectá-lo ao Git na sua máquina.

Para conectar o repositório remoto ao local, use:
```
git remote add origin <link-do-repositório>
```

- origin: é o nome padrão do repositório remoto
- <link-do-repositório>: deve ser substituído pelo URL HTTPS ou SSH do repositório que você criou no GitHub.

Para verificar se ocorreu tudo certo com a conexão, use este comando:
```
git remote -v
```

Esse comando lista os repositórios remotos associados ao projeto e mostra suas URLs. Você deverá ver algo assim:
```
origin  https://github.com/usuario/repositorio.git (fetch)
origin  https://github.com/usuario/repositorio.git (push)
```

Isso confirma que o repositório local está conectado ao remoto.

---

## Enviando as alterações locais para o repositório remoto

Para enviar os arquivos do seu repositório local para o GitHub, usamos o comando:
```
git push -u origin main
```

- push significa “empurrar”, ou seja, estamos enviando as alterações do repositório local para o remoto.
- A flag -u (ou --set-upstream) cria um vínculo entre a branch local main e a branch remota main.
Isso permite que, nas próximas vezes, você possa apenas usar `git push` sem precisar especificar o repositório e a branch.
origin é o nome padrão do repositório remoto.
- main é o nome da branch principal. Dependendo do seu repositório, o nome da branch pode ser diferente, como master.

Para trazer as alterações que foram feitas no repositório remoto, usamos o comando:
´´´
git pull
´´´

Esse comando busca alterações no repositório remoto e as integra a sua branch local. É útil quando você está trabalhando em equipe e um outro programador faz
alterações no repositório remoto. Você pode atualizar apenas usando o `git pull`.

Caso queira clonar um repositório remoto, pode usar:
```
git clone <link do repositório> <nome da pasta> # o nome da pasta é opcional
```

O Git irá baixar todos os arquivos e commits do projeto.
Além disso, ele já configura automaticamente a conexão com o repositório remoto, ou seja, você não precisará usar git remote add depois.
Por padrão, a branch principal será configurada como main ou master, dependendo do repositório.