# Padronização de commits e boas práticas

## Conventional Commits

Conventional Commits é uma convenção para padronizar mensagens de commit no Git, conectando cada commit com o tipo de mudança que ele representa e com versionamento semântico. É o ideal para padronizar seus commits e manter um projeto organizado e dentro do padrão. Caso queira ver o site oficial, acesse https://www.conventionalcommits.org/pt-br/v1.0.0/

### Estrutura básica

Todos os commits devem seguir uma estrutura básica:
```
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé(s) opcional(is)]
```
- Linha 1: obrigatória, pois é a principal mensagem do commit.
- Linha 2: opcional, descrição mais longa
- Linha 3: opcional, usado como rodapé

>Nota: A comunidade open source recomenda, como boa prática, que o título do commit tenha no máximo 50 caracteres e o corpo do commit tenha suas linhas quebradas a cada 72 caracteres. O Conventional Commits não define limites de tamanho de linha, essa é uma recomendação da comunidade. Mesmo assim, tornou-se comum combinar a estrutura do Conventional Commits com essas boas práticas clássicas de formatação.

Veja alguns exemplos referentes à linha 1:
```
fix: corrige bug na validação

feat(lang): adiciona suporte a pt-BR

feat(api): altera formato da resposta
```

Abaixo estão os tipos e tipos adicionais que você pode usar em seus commits. Diferentes tipos podem ser adotados dependendo da sua equipe:
- feat: novo recurso
- fix: correção de bug
- docs: mudança apenas em documentação
- style: formatação, espaços, ponto e vírgula, sem alterar comportamento
- refactor: refatoração sem mudar comportamento externo
- perf: melhorias de performance
- test: adição/ajuste de testes

O escopo indica a parte do sistema que será afetada. É opcional, mas altamente recomendado em projetos maiores.
A descrição deve ser um resumo curto, explicando a mudança de forma clara.

O corpo, se existir, vem depois de uma linha em branco e pode ter quantos parágrafos forem necessários, explicando o “porquê” ou detalhes técnicos.

Os rodapés também vêm após uma linha em branco (depois do corpo ou direto após a descrição, se não houver corpo):
- Cada rodapé segue o padrão Token: valor ou Token #id (inspirado em Git trailers).
- Tokens usam - no lugar de espaços, como Reviewed-by, Refs, Acked-by.​
- Uma exceção é BREAKING CHANGE, que pode ser usado com espaço mesmo.

>Nota: Um breaking change é quando sua alteração quebra compatibilidade com versões anteriores.

Vejamos exemplos de rodapés:
```
Closes: #22
Co-authored-by: Fulano <email>
BREAKING CHANGE: mudou tal coisa
```
```
Resolves: #302
Co-authored-by: Ana Lima <ana@exemplo.com>
Reviewed-by: Pedro Souza
```

>Nota: você não precisa necessariamente colocar todas as informações mostradas no exemplo acima. Geralmente isso é definido pela equipe ou projeto.

Você também pode indicar um breaking change usando `!` no título e, nesse caso, não precisará adicionar um breaking change no rodapé. Veja um exemplo:
```
feat!: remover função de login antigo
```

Adotar Conventional Commits traz vários benefícios práticos no fluxo de Git e entrega contínua. Então, busque sempre praticar e se manter atualizado.

## Boas práticas

Aprender sobre boas práticas para a utilização do Git é fundamental para garantir que o desenvolvimento do projeto seja eficiente, organizado e colaborativo. Ferramentas de controle de versão, como o Git, permitem que várias pessoas trabalhem no mesmo projeto simultaneamente. Mas isso pode gerar problemas se não houver uma boa gestão organizacional dos commits e branches, então apresentaremos boas práticas para você utilizar o Git e manter uma rotina de trabalho organizada e eficiente. Caso você vá trabalhar em equipe, esse conhecimento será essencial.

Um dos princípios mais importantes no uso do Git é realizar commits claros e frequentes, onde cada commit representa uma etapa de trabalho bem definida. Isso ajuda a manter o histórico limpo e o rastreamento de mudanças.

Commits grandes demais podem conter muitas mudanças, o que pode dificultar o entendimento das alterações e a identificação de problemas. O ideal é dividir o trabalho em partes menores e mais gerenciáveis.

Um dos pontos mais importantes na hora de realizar um commit é a mensagem, que deve ser clara e descritiva, explicando o que foi alterado e o porquê. Uma boa mensagem é fundamental para que outros desenvolvedores possam entender de maneira clara e rápida as mudanças realizadas. Além disso, o título do commit não deve ser tão extenso. Caso precise descrever mais sobre as mudanças, utilize o corpo do commit.

Siga um padrão nas mensagens de commit, isso ajuda a manter o repositório organizado. Em alguns casos, são adotadas convenções para manter estilo e consistência, como, por exemplo, usar sempre o tempo verbal no presente e definir um limite de caracteres para o título e corpo do commit.

Sobre branches, é recomendado criar uma branch para cada nova funcionalidade ou correção de bug, evitando que o código principal seja alterado diretamente. Evite branches muito longas, pois podem gerar conflitos difíceis de resolver. Mantenha as branches pequenas e frequentes, realizando merges regularmente.

Manter a comunicação sempre ativa é extremamente importante se você estiver trabalhando em equipe. Sempre comunique outros desenvolvedores envolvidos para garantir soluções alinhadas com as intenções do projeto.

Seguir boas práticas no uso do Git e na criação de commits não apenas melhora a qualidade do código, mas também facilita a colaboração em equipe, a manutenção do projeto e a solução de problemas. Busque sempre manter seus projetos alinhados com essas práticas para manter um fluxo de trabalho eficiente e organizado.

---

Se você leu todo o conteúdo, colocou em prática e chegou até aqui, isso significa que aprendeu muita coisa sobre Git! Fico realmente feliz em saber disso. Espero que este material tenha agregado aos seus conhecimentos e contribuído para o seu desenvolvimento profissional. Agradeço a todos que dedicaram seu tempo à leitura deste trabalho. Continue sempre buscando conhecimento!