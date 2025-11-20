# Comandos intermediários

## Branches

Uma branch é uma ramificação do seu projeto, basicamente como uma "linha do tempo" independente dentro do repositório. Ela representa um ponteiro para um commit, permitindo que você desenvolva novas funcionalidades, faça testes ou experimente alterações sem afetar a branch principal.
Usar branches é essencial para organizar o desenvolvimento, trabalhar em novas funcionalidades, testar soluções e colaborar em equipe. Elas permitem que cada membro desenvolva partes diferentes do projeto de forma paralela, sem interferir no código principal. Isso torna o fluxo de trabalho mais seguro, previsível e escalável, funcionando tanto para projetos individuais quanto para equipes pequenas ou grandes.

Quando você inicia um repositório, ele cria por padrão a branch principal, chamada `main` ou em alguns casos `master`.
Para ver todas as branches locais do projeto, usamos o comando:
```
git branch
```

A branch atual será marcada com um `*`.
O Git também possui outros tipos de listagens:
- `git branch -r` - mostra as branches remotas
- `git branch -a` - mostra branches locais e remotas
- `git branch -vv` - exibe mais detalhes sobre cada branch, incluindo em qual commit está baseada

---

## Criando uma nova branch

>Antes de criar uma branch, é importante saber em qual branch você está no momento, pois a nova branch será criada a partir dela.

Para criar uma nova branch é bem simples:
```
git branch <nome-da-branch>
```

Este comando cria uma nova branch, mas você ainda permanece na sua branch atual.

Para mudar de branch, podemos utilizar 2 comandos diferentes. Explicaremos logo em seguida.
```
git checkout <nome-da-branch>

git switch <nome-da-branch>
```

Ambos os comandos fazem a mesma coisa, porém o git checkout tem outras funcionalidades, enquanto o git switch é focado apenas em branches. Por agora, recomendamos utilizar apenas o `git switch`, por ser mais simples e seguro.

Você também pode criar uma branch e já mudar para ela:
```
git checkout -b <nome-da-branch>

git switch -c <nome-da-branch>
```

>Importante: quando você cria uma nova branch, ela sempre nasce a partir do commit que você está naquele momento. Isso significa que, se você estiver na branch ``main``, a nova branch será criada a partir dela. Se estiver nessa nova branch e quiser criar outra, será criada a partir dessa branch secundária. Resumidamente, você pode criar uma cadeia de branches. Mas não recomendamos fazer isso, pois cadeias muito profundas (branches dentro de branches) podem dificultar a unificação delas, complicar revisões de código e causar conflitos. Recomendamos que, sempre que possível, crie novas branches a partir da branch ``main``.

Para facilitar, você pode criar uma branch a partir de outra específica sem necessariamente precisar estar nela:
```
git branch <nova-branch> <origem-da-branch>
```
Ou de uma forma mais moderna:
```
git switch -c <nova-branch> <origem-da-branch>
```

Se em algum momento precisar renomear sua branch, você pode usar o seguinte comando:
```
git branch -m <novo-nome>
```

>Importante: se quiser renomear a branch atual, use o comando acima, mas caso queira renomear outra branch que não seja a atual, primeiro você digita o nome antigo e depois o novo:
```
git branch -m <nome-antigo> <nome-novo>
```

>Importante: se a branch já tiver sido enviada para o remoto, também será necessário renomeá-la no servidor.
Para fazer isso, é necessário dizer ao servidor que a branch com o nome antigo não existe mais:
```
git push origin --delete <nome-antigo>
```
Depois você reenvia sua branch com o novo nome:
```
git push -u origin <novo-nome>
```
Após isso, sua cópia no repositório local ainda pode estar "lembrando" da branch antiga. Nesse caso é necessário limpar todas as referências e baixar as informações atualizadas:
```
git fetch --prune
```

>O comando ``--prune`` serve quando também uma branch remota é excluída.

---

## Mesclando branches

Quando você integra o trabalho de uma branch em outra, o Git não “copia” arquivos. O que acontece é que a branch que recebe o merge passa a reconhecer os commits da outra branch como parte da sua própria linha do tempo. Nada é duplicado, e a branch original continua existindo normalmente.

Para fazer a integração, primeiro vá até a branch que deve receber as mudanças, e utilize o seguinte comando:
```
git merge <nome-da-branch>
```

Esse comando diz ao Git para mesclar a branch especificada à branch atual. É importante destacar que a branch atual na qual você está é sempre a que receberá as mudanças.

>Importante: caso ocorra um conflito, quando duas branches alteram a mesma linha de código, o Git não tem como decidir qual versão é a correta. Nesse caso, você deve corrigir o conflito manualmente, adicionar os arquivos corrigidos e realizar um novo commit.

Após realizar o merge, você pode excluir a branch secundária com segurança, pois os commits dela já fazem parte da ``main``. Isso é recomendado para manter o repositório organizado, mas algumas equipes preferem manter a branch por motivos de histórico interno. Certifique-se de que o merge foi concluído antes de apagar a branch.

Para excluir uma branch que já foi mergeada, use:
```
git branch -d <nome-da-branch>
```

Para excluir uma branch que ainda não foi mergeada:
```
git branch -D <nome-da-branch>
```

>Atenção: isso força a exclusão da branch. Os commits continuarão existindo temporariamente (até serem coletados pelo garbage collector do Git), e é possível recuperá-los, mas esse já é um assunto mais avançado. Portanto, use essa opção com cuidado.

Para excluir uma branch remota:
```
git push origin --delete <nome-da-branch>
```

>Isso não exclui sua branch local, apenas a referência remota.

---

## Git Fetch

Em projetos que têm mais de uma pessoa trabalhando na branch main, você irá precisar atualizar seu repositório local com o remoto antes de enviar qualquer alteração. Podemos usar:
```
git fetch origin main
```
Ou para buscar todas as alterações:
```
git fetch
```

Este comando buscará atualizações no repositório remoto. O comando não altera os seus arquivos e nem muda sua branch, ele apenas traz informações novas sobre o repositório remoto, atualizando apenas as referências remotas.

Para verificar o que mudou após a atualização, use:
```
git log HEAD..origin/main --oneline
```

`HEAD` aponta para o commit atual, `origin/main` é a referência remota que acabou de ser atualizada, `..` mostra os commits que estão no remoto e não na sua branch atual, e `--oneline` mostra os commits resumidamente em uma única linha.

Quando quiser integrar as alterações do remoto, garanta que está na branch correta e use:
```
git merge origin/main
```

>Importante: o comando acima é usado para integrar as alterações da branch local e referência remota. Diferentemente do comando `git merge branch-local`, que é usado para mesclar 2 branches locais.

---

Precisamos explicar alguns pontos importantes sobre esses dois comandos e o seu funcionamento. Isso será fundamental para entender sobre branches e o repositório remoto.

Podemos usar os comandos ``git fetch`` e ``git merge`` sem argumentos (conhecidos como bare commands), mas não é recomendado para iniciantes e para operações que exigem controle total. O Git, nesse caso, tenta determinar a origem (upstream) com base nas configurações da sua branch local. Para controle total, é sempre melhor especificar: ``git fetch origin main`` e ``git merge origin/main``.

Outro ponto é que existe uma diferença fundamental na sintaxe dos dois comandos. No `git fetch` usamos espaços para separar os argumentos (a menos que usado sem argumentos), pois é obrigatório. O Git exige o uso de 2 argumentos, que geralmente são:
- `origin`: é o primeiro argumento, nesse caso o nome do repositório remoto
- `nome-da-branch`: é o segundo argumento, sendo o nome da branch no servidor
O Git acessa o servidor chamado `origin`, localiza o código da branch, baixa os commits e atualiza sua referência remota local, que é nomeada como `origin/nome-da-branch`.

Já no `git merge`, você conversa com o repositório local, onde o Git mescla a referência `origin/main` na sua branch atual. Nesse caso a barra atua como uma formatação que o Git usa para o nome completo da referência de rastreamento remoto.

---

Você também pode usar:
```
git pull origin main
```

- `origin`: é o nome do repositório remoto (o padrão ao clonar um projeto, geralmente o GitHub, GitLab, etc.).
- `main`: é o nome da branch remota que você quer buscar.

>O comando `git pull` é basicamente uma maneira mais rápida e simples de atualizar seu repositório. Em resumo, é a junção do `git fetch` + `git merge`. Para iniciantes, recomendamos sempre primeiro realizar o `git fetch` e depois o `git merge`, para ter mais controle da situação e evitar conflitos.

---

## Enviando para o repositório remoto

Para mandar todas as nossas alterações do repositório local para o remoto, podemos utilizar o seguinte comando:
```
git push -u origin <nome-da-branch>
```

---

 ### Upstream

 No comando anterior utilizando a flag `-u`, abreviação de `--set-upstream`. O conceito de Upstream (ou Rastreamento Remoto) é um dos mais fundamentais e úteis do Git, pois permite que você use os comandos curtos git pull e git push sem precisar digitar o nome do repositório remoto (origin) e o nome da branch toda vez.

 Upstream é a branch remota padrão que uma branch local foi configurada para rastrear (tracking). Em outras palavras, é a configuração que o Git deve consultar para identificar alterações ou para saber para onde enviar seu trabalho.
 - branch local: onde está seu código de trabalho, por exemplo `minha-feature`
 - upstream branch: é a branch remota correspondente a sua branch local

 Quando o Git sabe qual é o seu upstream, os comandos podem ser simplificados. Em outras palavras, você pode usar um comando curto sem argumentos, como mostrado anteriormente. Por exemplo, em vez de você digitar `git pull origin main`, pode simplesmente só digitar `git pull`.

 A maneira comum de configurar o upstream é realizando a primeira publicação, ou seja, quando você for enviar uma nova branch pela primeira vez para o servidor, use a flag `-u` como mostrado no início.
 ```
 git push -u origin <nome-da-branch>
 ```

 O Git grava a configuração de que, a partir de agora, sua branch local deve rastrear a remota.

 Se você já criou a branch localmente, mas não a enviou, ou se deseja mudar o upstream de uma branch existente para outra, você usa o comando:
 ```
 git branch --set-upstream-to=origin/main
 ```

 >Importante: você deve estar na branch que deseja configurar.

 E por fim, para verificar o upstream configurado para todas as suas branches locais, use:
 ```
 git branch -vv
 ```