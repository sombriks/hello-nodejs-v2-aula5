# Organizando os diretórios do projeto

- 10 minutos
- façam o fork e o checkout da aula 5

## Definição

- para criar um projeto node criamos uma pasta e nesta pasta damos npm init
- esta pasta é o nosso "ponto de execução"
- ela terá o node_modules com os pacotes vindo do npm
- teremos um .gitignore pra controlar o que será versionado pelo git ou não
- teremos um package.json, a maior evidência de que estamos lidando com um projeto node
- esta pasta terá nossos códigos fonte, testes e assets
  - **asset** é tudo que não é código mas precisa ter (ex. imagens, audios, documentos)

## Aplicação

- sempre que você for criar alguma coisa com node, comece criando a pasta e efetuando npm init
- sempre use o --save ao instalar. Se der errado é só dar uninstall --save , :stuck_out_tongue_winking_eye:

## Exemplo

- dentro do repositório da aula 5 crie uma pasta chamada hello-express

```bash
mkdir hello-express
cd hello-express
npm init -y
```

- o **-y** é pra aceitar todas as respostas padrão
- instale algumas dependências

```bash
npm install sqlite3 knex express --save
```

- crie um script para servir de ponto de entrada da aplicação
- chame-o de index.js

```javascript
// index.js
const express = require("express");

// to be continued
```

## Exercício

- você já fez o exercício, era isso aí
- agora falta comitar, comite aí pra dar um pull em casa depois

[Voltar](../README.md)
