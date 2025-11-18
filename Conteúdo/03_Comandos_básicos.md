# Primeiros Comandos

Antes de começarmos a usar o Git, precisamos entender alguns conceitos e comandos fundamentais. Vamos aprender como iniciar um repositório, acompanhar as mudanças nos arquivos e registrar alterações com commits de forma simples e organizada.

## Iniciando um repositório

Primeiro, entre na pasta onde ficará seu repositório. Veja um exemplo de como acessar o diretório pelo Git Bash:

`cd /c/pasta01/pasta02`

Após isso, inicialize o repositório usando o seguinte comando:

`git init`

Este comando irá criar uma pasta oculta chamada `.git`, onde será guardado todo o histórico do seu projeto.

A partir desse momento, os arquivos modificados passam por algumas etapas antes de serem registrados:

- **Working Directory:** é a pasta do projeto no seu computador. São os arquivos que você pode ver, abrir, editar e excluir. O Git entende que há arquivos modificados ou novos, mas ainda não faz nada com eles. Se você verificar o status do repositório usando `git status`, ele mostrará algo como **“Changes not staged for commit”** ou **“Untracked files”**, ou seja, os arquivos ainda não estão sendo rastreados pelo Git.

Agora vamos começar a adicionar os arquivos que foram modificados ou que acabaram de ser criados.

Para adicionar um arquivo específico, usamos o comando seguido do nome do arquivo e sua extensão. Por exemplo:

`git add index.html`

Para adicionar todos os arquivos de uma só vez:

`git add .`

Os arquivos adicionados estarão na **Staging Area**, algo como uma sala de espera. Nessa fase, os arquivos estão prontos para serem registrados em um commit e incluídos no repositório Git.

## Registrando tudo em um Commit

>Um commit é como um ponto de salvamento permanente no seu projeto. Ele registra o estado atual dos seus arquivos em um momento específico, permitindo que você acompanhe e recupere o histórico do seu trabalho.

Chegamos agora ao momento de registrar nossas alterações criando um commit. Depois de adicionar todos os arquivos desejados à **Staging Area**, é hora de fazer um commit. Podemos utilizar o seguinte comando:

`git commit`

Isso fará com que o Git abra um editor de texto padrão para que você digite a mensagem do seu commit, pois ela é obrigatória. Mas, se quiser algo mais simples e rápido, com a mensagem já embutida, use:

`git commit -m "Sua mensagem"`

Caso queira adicionar uma descrição um pouco maior, use:

`git commit -m "Sua mensagem" -m "Descrição mais detalhada"`

> **Nota:** Caso você tenha aberto o editor de texto e queira adicionar uma mensagem detalhada, siga esta estrutura:
> - Na primeira linha, escreva o **título** do commit.
> - Na segunda linha, deixe um **espaço em branco**, para que o Git entenda a separação.
> - Na terceira linha, escreva a **descrição detalhada** das suas modificações.

Caso você queira desfazer as alterações feitas em um arquivo específico e voltar ao estado do último commit registrado, use:

`git restore arquivo.html`

>Mas atenção: isso descarta todas as mudanças feitas no arquivo desde o último commit.

Se quiser apenas retirar o arquivo da **Staging Area**, use:

`git restore --staged arquivo.html`

Com esse comando, seu arquivo volta para o **Working Directory** e as mudanças não são descartadas.

---

# Git e GitHub

Podemos trabalhar com um repositório de duas maneiras: enviando um projeto que já existe na sua máquina para um repositório remoto ou fazendo o caminho inverso, clonando um repositório remoto para o seu computador. Vamos ver primeiro como subir um projeto para o GitHub:

No GitHub, você deve criar um repositório vazio, sem nenhum arquivo. Não marque as opções para adicionar `README.md`, `.gitignore` ou `LICENSE`. Depois que o repositório estiver criado, será necessário conectá-lo ao Git na sua máquina. Esse processo pode ser feito usando o link HTTPS ou o link SSH do repositório.

Para conectar o repositório remoto ao local, use:

`git remote add origin <link do repositório>`

Para verificar se deu certo, execute:

`git remote -v`

O Git deve retornar o link do seu repositório remoto.

Agora, vamos enviar os arquivos locais para o repositório remoto usando o comando `push`:

`git push -u origin main`

“Push” significa “empurrar”, ou seja, estamos enviando nosso repositório local para o GitHub.  
A flag `-u` cria um vínculo com a branch `main`, informando ao Git que essa será a branch padrão.  
O nome `origin` é o identificador padrão do repositório remoto, e `main` é o nome da branch.  

Depois disso, os próximos envios poderão ser feitos apenas com:

`git push`

Para trazer as alterações que foram feitas no repositório remoto, usamos o comando `pull`:

`git pull`

Se você quiser clonar um repositório remoto para a sua máquina, utilize:

`git clone <link do repositório> <nome da pasta> (opcional)`

O Git irá baixar todos os arquivos do projeto e configurar automaticamente a conexão com o repositório remoto, ou seja, você não precisará usar `git remote add` depois.
