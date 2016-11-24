# Introdução ao express.js

- 10 minutos

## Definição

- o padrão *de fato* para desenvolvimento web com node
- é [opensource](https://github.com/expressjs/express)
  - mas foi vendido para uma empresa. que foi comprada pela IBM. [Long sotry](http://thefullstack.xyz/history-express-javascript-framework/).
- o express faz o papel de controlador
  - chamamos de roteamento hoje em dia

## Aplicação

- criação de aplicativos nodejs para a web
  - [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) APIs
- faz renderização server-side também, mas não vamos encostar nisso

## Exemplo

- retorne ao index.js criado no exercício anterior

```javascript
// index.js
const express = require("express");

const app = express();

app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.listen(8080);

// to be continued
```

- execute este js com **node index.js**
- abra firefox ou qualquer outro navegador
- digite o endereço http://127.0.0.1:8080/hello
- veja a mágica

## Exercício

- no index.js, mude a linha **app.listen(8080)** para **app.listen(3000)** e salve.
  - dê F5 no browser. continua funcionando?
  - agora aborte a execução do script node
  - execute novamente o index.js. ainda funciona? o que foi preciso para funcionar?
- comite as alterações feitas.

[Voltar](../README.md)
