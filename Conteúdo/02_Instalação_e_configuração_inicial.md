# Instalando e configurando o Git

## Instalação

Para instalar o Git no Windows, acesse a página oficial de instalação do Git para Windows: [Git para Windows](https://git-scm.com/install/windows)

No site, baixe a versão recomendada e execute o arquivo .exe. Ao iniciar o instalador, você verá várias telas com opções de configuração.
Não é necessário alterar nada neste momento, mantenha as opções pré-selecionadas, pois elas são adequadas para a maior parte dos usuários.
Após concluir a instalação, abra o Git Bash, que é o terminal onde você poderá executar os comandos Git.

Para testar se a instalação funcionou corretamente, use o seguinte comando:
```
git --version
```
Esse comando exibe a versão instalada do Git. Se a versão aparecer no terminal, significa que o Git foi instalado com sucesso.

Para instalar o Git no Linux ou no macOS, acesse o mesmo link acima, selecione a seção referente ao seu sistema operacional e siga as instruções apresentadas.
No Linux, geralmente será necessário copiar e executar um comando no terminal. No macOS, você poderá baixar o instalador ou usar o Homebrew.

---

## Configuração inicial

Primeiro, vamos configurar os dados que aparecerão nos seus commits. Os comandos abaixo são utilizados para registrar seu nome e e-mail:
```
git config --global user.name "Seu nome"
git config --global user.email "seuemail@exemplo.com"
```

Essas configurações são globais, ou seja, serão o padrão para todos os seus projetos. Caso queira definir apenas para um projeto específico, basta omitir a flag `--global`.

Caso queira conferir as configurações, podemos usar os seguintes comandos:
```
git config --list           #Para exibir todas as configurações
git config --global --list  #Exibe apenas as configurações globais
```

Algumas instalações ainda usam "master" como padrão para a branch principal. Porém, desde 2020, o Git usa "main" como novo padrão.
Para nos mantermos atualizados, podemos definir a branch principal para "main" usando o seguinte comando:
```
git config --global init.defaultBranch main
```

> Nota: caso ainda não conheça o conceito de "branch", não se preocupe, veremos mais adiante. O comando acima serve apenas para nos mantermos no padrão.

---

## Chave SSH

Uma chave SSH é uma forma muito segura de se conectar a um servidor, como o GitHub, sem precisar usar uma senha.
Existem outras maneiras de estabelecer essa conexão entre o Git e o GitHub, mas utilizaremos esta por ser mais segura e menos complicada.

Primeiro devemos gerar a chave SSH no terminal do Git Bash:
```
ssh-keygen -t ed25519 -C "seuemail@example.com"
```

>Nota: Existem diferentes tipos de chaves, mas o modelo ed25519 é o mais recomendado atualmente, por ser seguro e rápido.

O terminal perguntará em qual caminho deve salvar a chave. Apenas pressione Enter, pois o Git definirá um caminho automaticamente.
Em seguida, ele pedirá para você digitar uma _passphrase_, que pode ser entendida como uma senha.
É recomendável, pois se alguém acessar seu computador, sua chave SSH estará protegida.
Mas, caso não queira, pressione Enter novamente.  
O comando gerará uma chave pública e uma chave privada. Utilizaremos apenas a chave pública no GitHub; a chave privada servirá para a autenticação.

Podemos usar o comando abaixo para listar todos os arquivos armazenados na pasta ´.ssh´, incluindo chaves SSH e outros arquivos relacionados:
```
ls ~/.ssh
```

> Atenção: nunca compartilhe sua chave privada, pois quem tiver acesso a elas pode facilmente te causar problemas.

Você também pode usar um agente SSH para não precisar digitar sua senha toda vez que usar sua chave SSH, pois ele mantém sua chave desbloqueada em memória com segurança.
Dessa forma, você a mantém segura e evita digitar a senha repetidamente. Para fazer a ativação do agente, use o seguinte comando:
```
# Windows
eval $(ssh-agent -s) 

# Linux/macOS
eval "$(ssh-agent -s)"
```

Em seguida, adicione sua chave SSH ao seu agente:
```
ssh-add ~/.ssh/id_ed25519
```

> Nota: o comando acima leva em conta o nome padrão dado pelo Git a chave SSH. Caso tenha colocado algum outro nome, deve ser alterado, por exemplo: `ssh-add ~/.ssh/minhaChave`.

Pronto, seu agente está configurado. Caso queira listar as chaves carregadas no agente, use:
```
ssh-add -l
```

---

## Conexão com o GitHub

Para conseguir realizar a conexão do Git com o GitHub, precisamos primeiro copiar a sua chave SSH pública. O comando a seguir exibirá sua chave pública, copie-a normalmente:
```
cat ~/.ssh/id_ed25519.pub
```

No seu perfil do GitHub, vá em configurações, depois selecione a opção "SSH and GPG keys".
No campo de SSH keys, clique em **"New SSH key"**. Adicione um nome para sua chave e, se caso houver o campo **"Key type"**, selecione **"Authentication Key"**.
No último campo, cole sua chave pública e finalize clicando em **"Add SSH key"**. Pronto, sua chave estará adicionada.

Para realizar o teste de conexão, use o seguinte comando:
```
ssh -T git@github.com
```

Digite sua _passphrase_ caso tenha criado uma, e se aparecer a mensagem:  
**"Hi 'seu usuário'! You've successfully authenticated..."**  
está tudo certo!

Caso contrário, verifique se a chave que você adicionou no GitHub é a mesma que você copiou do terminal.

---


Pronto, seu Git está configurado e sincronizado com seu GitHub.  
Lembrando que esta é apenas a configuração básica, pois o intuito do repositório é apresentar e ensinar a base do Git.
Existem diversas outras configurações que você pode fazer, então leia, pesquise e busque conhecimento!