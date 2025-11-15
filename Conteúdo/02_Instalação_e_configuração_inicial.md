# Instalando e configurando o Git

## Instalação
Para instalar o Git no Windows, basta clicar aqui: [Git Windows](https://git-scm.com/install/windows). Você será redirecionado para o site oficial do Git, baixe a versão recomendada e depois execute o arquivo _.exe_. Após a execução, aparecerá a tela de instalação do Git, que apresenta várias abas de configuração. Não se desespere, não há necessidade de se preocupar com isso agora. Mantenha as opções pré-selecionadas, pois serão as recomendadas para o seu sistema.
Depois de finalizar toda a instalação, abra o Git Bash, que é o terminal Git onde você poderá executar os comandos.

Para testar, digite o seguinte comando:

`git -v`

Este comando serve para exibir a versão atual do Git. Caso apareça, está tudo certo.

**Para instalar o Git no Linux ou macOS, entre no link acima, selecione a aba correspondente ao seu sistema operacional, copie o comando e cole no terminal do seu sistema.**

---

## Configuração inicial

Primeiramente, você precisa configurar os dados que aparecerão em seus commits:

- Para configurar seu nome de usuário: `git config --global user.name "Seu nome"`

- Para configurar seu e-mail: `git config --global user.email "seuemail@exemplo.com"`

Essas configurações são globais, ou seja, serão o padrão para todos os seus projetos. Caso queira definir apenas para um projeto específico, basta omitir a flag `--global`.

Se quiser verificar a configuração, use: `git config --global --list`

Algumas instalações usam "master" como padrão para a branch principal. Atualmente se usa "main" como novo padrão. Para nos mantermos atualizados, podemos definir a branch principal para "main" usando o seguinte comando:

`git config --global init.defaultBranch main`

> Nota: caso ainda não conheça o conceito de "branch", fique tranquilo, veremos mais a seguir. O comando acima serve apenas para nos mantermos no padrão.

---

## Chave SSH

Uma chave SSH é uma forma muito segura de se conectar a um servidor, como o GitHub, sem precisar usar uma senha. Existem outras maneiras de estabelecer essa conexão entre o Git e o GitHub, mas utilizaremos esta por ser mais segura e menos complicada.

Primeiro devemos gerar a chave SSH no Git Bash:  
`ssh-keygen -t ed25519 -C "seuemail@example.com"`

> Nota: existem outros tipos de chaves, mas utilizaremos essa por ser a mais recomendada e segura atualmente.

O terminal perguntará em qual caminho deve salvar a chave. Apenas pressione Enter, pois o Git definirá um caminho automaticamente. Em seguida, ele pedirá para você digitar uma senha. É recomendável, pois se alguém acessar seu computador, sua chave SSH estará protegida pela senha. Mas, caso não queira, pressione Enter novamente.  
O comando gerará uma chave pública e uma chave privada. Utilizaremos apenas a chave pública no GitHub; a chave privada servirá para a autenticação.

> Atenção: nunca compartilhe suas chaves SSH, pois quem tiver acesso a elas pode facilmente te causar problemas.

Você também pode usar um agente SSH para não precisar digitar sua senha toda vez que usar sua chave SSH. Dessa forma, você a mantém segura e evita digitar a senha repetidamente.

No Windows, inicie o agente SSH desta forma:  
`eval $(ssh-agent -s)`  

Caso esteja usando Linux ou macOS, use:  
`eval "$(ssh-agent -s)"`

Depois, adicione sua chave ao agente:  
`ssh-add ~/.ssh/id_ed25519`

Pronto: seu agente SSH está configurado com sua chave.  
Para listar as chaves carregadas no agente, use: `ssh-add -l`

---

## Conexão com o GitHub

Primeiro, copie sua chave pública. No Git Bash, digite:  
`cat ~/.ssh/id_ed25519.pub`

A chave será exibida no terminal Git — copie-a.

No seu perfil do GitHub, vá em configurações, depois selecione a opção "SSH and GPG keys". No campo de SSH keys, clique em **"New SSH key"**. Adicione um nome para sua chave e, em **"Key type"**, selecione **"Authentication Key"**. No último campo, cole sua chave pública e finalize clicando em **"Add SSH key"**. Pronto, sua chave estará adicionada.

Para testar a conexão, digite no Git Bash:  
`ssh -T git@github.com`

Digite sua senha caso tenha criado uma, e se aparecer a mensagem:  
**"Hi 'seu usuário'! You've successfully authenticated..."**  
está tudo certo!

Caso contrário, verifique se a chave que você adicionou no GitHub é a mesma que você copiou do terminal.

---

Pronto, seu Git está configurado e sincronizado com seu GitHub.  
Lembrando que esta é apenas a configuração básica, pois o intuito do repositório é apresentar e ensinar a base do Git. Existem diversas outras configurações que você pode fazer, então leia, pesquise e busque conhecimento!
