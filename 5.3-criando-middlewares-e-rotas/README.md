# Criando middleware e rotas

- 60 minutos
- rotas e verbos http (ou: introdução ao HTTP)
- criando rotas
- query parameters
- path parameters
- wildcards

## Definição

- outra forma de explicar o express é dizer que ele traz o [HTTP](https://pt.wikipedia.org/wiki/Hypertext_Transfer_Protocol) para o javascript
- o [node sozinho já fazia isso](http://nodebr.com/exemplo-hello-world-em-node-js/), mas [o express é mais amigável](http://expressjs.com/pt-br/starter/hello-world.html)
- do mesmo modo que o knex tem os verbos do SQL representados em sua API, o express tem os verbos do HTTP na dele
- adicionalmente, no express temos a ideia de **[middleware](http://expressjs.com/en/guide/using-middleware.html)**
  - parecido com os filtros do java, as rotas do express podem compor uma pipeline de processamento

## Aplicação

```javascript
// index.js
const express = require("express");

const app = express();

// rota com seu middleware
app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.listen(3000);

// to be continued
```

- **app.get** é parte da API express para receber uma requisição HTTP GET
- **"/hello"** é o que chamamos de URI, aquele caminho no endereço do browser
- **(req,res) => res.send("Olá mundo!")** é o middleware.
  - poderia ser escrito assim: **(req,res,next) => res.send("Olá mundo!")**
  - ou ainda **function (req,res,next){ res.send("Olá mundo!"); }**
- podemos adicionar várias rotas em nosso app express

## Exemplo

- o express tem [vários métodos](http://expressjs.com/en/4x/api.html#routing-methods) para usar os vários verbos HTTP, mas hoje usaremos apenas o **get**

```javascript
// index.js
const express = require("express");

const app = express();

app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.get("/greet", (req,res) => res.send(`Olá, ${req.query.nome}!`));

app.listen(3000);

// to be continued
```

- execute o script modificado com node index.js
- abra http://127.0.0.1:3000/greet e veja o resultado
- agora chame http://127.0.0.1:3000/greet?nome=serumaninho e veja a diferença
- experimente trocar o valor de nome na url acima
- comite as alterações para o seu git

- **IMPORTANTE** rotas atendem de modo assíncrono, como tudo no ecosistema node
  - elas são, entretanto, **definidas** da esquerda para a direita, de cima para baixo

```javascript
// problema-sombreamento.js
const express = require("express");

const app = express();

app.get("/hello", function (req,res) {
  res.send("Olá mundo!"));
});

app.get("/hello", function (req,res) {
  res.send("Olá pessoal!!!"));
});

app.listen(3000);
```

- se a sua rota algum dia não lhe der o valor que você espera, veja se ela não foi sombreada

```javascript
// index.js
const express = require("express");

const app = express();

app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.get("/greet", (req,res) => res.send(`Olá, ${req.query.nome}!`));

app.get("/queryparams", (req,res) => {
  console.log(req.query);
  res.send("Veja no console");
});

app.listen(3000);

// to be continued
```

- rode a nova versão do script
- visite http://127.0.0.1:3000/queryparams?a=b&c=d&anakin=vader e veja seu console
- tem outras formas de fornecer dados ao express usando o browser
- comite a versão acima também

```javascript
// index.js
const express = require("express");

const app = express();

app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.get("/greet", (req,res) => res.send(`Olá, ${req.query.nome}!`));

app.get("/queryparams", (req,res) => {
  console.log(req.query);
  res.send("Veja no console");
});

app.get("/pathparams/:nome/:time",  (req,res) => {
  res.send("Veja no console");
  console.log(req.params);
  console.log(`Meu nome é ${req.params.nome} e eu sou ${req.params.time} desde sempre`);
});

app.listen(3000);

// to be continued
```

- salve e reinice o script **node index.js**
- agora visite http://127.0.0.1:3000/pathparams/joão/vasco
- veja seu console
- no caso dos parâmetros de caminho (path parameters) temos pleno controle sobre a presença deles

```javascript
// index.js
const express = require("express");

const app = express();

app.get("/hello", (req,res) => res.send("Olá mundo!"));

app.get("/greet", (req,res) => res.send(`Olá, ${req.query.nome}!`));

app.get("/queryparams", (req,res) => {
  console.log(req.query);
  res.send("Veja no console");
});

app.get("/pathparams/:nome/:time",  (req,res) => {
  res.send("Veja no console");
  console.log(req.params);
  console.log(`Meu nome é ${req.params.nome} e eu sou ${req.params.time} desde sempre`);
});

app.get("/optional(/:maybe)?", function (req,res){
  if(req.params.maybe)
    res.send("Call me " + req.params.maybe)
  else
    res.send("I just met you");
  console.log(req.params)
});

app.listen(3000);
```

- se uma variável de uma rota for opcional você deve lembrar disso na hora de usar esta variável
- você pode combinar o knex com o express e usar a interface web pra salvar coisas no seu banco

## Exercício

- mas você já fez  e já comitou :+1:
- aliás, façam isso aqui functionar e comitem:

``` javascript
// exemplo-express-knex.js
const express = require("express");
const knex = require("./db");

const app = express();

app.get("/convidados", (req,res) => {
  knex("convidado").select().then((ret) => {
    res.send(ret)
  });
});

app.listen(3000);
```

- quando dá erro
  - o que você vê no browser?
  - o que você vê no console?
- vocês precisarão do db.js da aula passada
- precisarão garantir que a tabela **convidado** exista no banco. criem migrates ou usem o banco da aula anterior. o que estiver mais fácil.
  - caso não recordem como fazer um migrate olhem a aula 4 novamente

[Voltar](../README.md)
