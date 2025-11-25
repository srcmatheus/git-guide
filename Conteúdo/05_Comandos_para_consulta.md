# Lista de comando Git

O Git possui muitos comandos diferentes e, para não ficar apenas no conteúdo básico, vou apresentar vários comandos com uma breve explicação. Isso vai ampliar seus conhecimentos sobre Git e também poderá servir como um guia de consulta.

Exibe o histórico de commits:
```
git log
```

Exibe os 3 últimos commits:
```
git log -3
```

Exibe um resumo dos commits em uma única linha:
```
git log --oneline
```

Exibir detalhes de arquivos modificados:
```
git log --stat
```

Cria o arquivo .gitignore:
```
touch .gitignore
```

Adiciona um arquivo em específico ao .gitignore:
```
echo "arquivo.txt" >> .gitignore
```

Descarta as alterações locais de um arquivo até o último commit:
```
git checkout -- nomedoarquivo	
```

Desfaz um commit mas mantém as alterações preparadas:
```
git reset --soft <commit>
```

Desfaz o commit e mantém as alterações no working directory:
```
git reset --mixed <commit>
```

Apagar o commit e as alterações locais:
```
git reset --hard <commit>
```

Descartar mudanças locais sem alterar o histórico:
```
git restore
```

Restaurar um arquivo a partir de um commit em específico:
```
git restore --source <commit> <arquivo>
```

Modificar o último commit e reescreve o histórico local:
```
git commit --amend
```

Criar um novo commit que desfaz outro:
```
git revert <hash>
```

Apagar arquivos não rastreados:
```
git clean -f
```

Apagar pastas não rastreadas:
```
git clean -fd
```

Mesclar uma branch a branch atual com uma mensagem explicativa:
```
git merge nome_branch -m "mensagem"
```

Exibir o estado atual do repositório:
```
git status
```

Exibir diferenças entre o arquivo modificado e o último commit:
```
git diff
```

Exibir as diferenças dos arquivos já adicionados ao stage:
```
git diff --staged
```

Sobrescrever o histórico remoto com seu histórico local:
```
git push --force
```

Remover um repositório remoto:
```
git remote remove <nome>
```

Renomear um repositório remoto:
```
git remote rename <nome-antigo> <nome-novo>
```

ALterar URL de um repositório:
```
git remote set-url <nome> <url>
```

Baixar todas as alterações do repositório remoto:
```
git remote set-url <nome> <url>
```

Baixar todas as alterações do repositório remoto e reaplicar ao local:
```
git pull --rebase
```

Enviar todos os commit locais para o remoto:
```
git push --all
```

Deletar uma branch remota:
```
git push <remote> --delete <nome-da-branch>
```


