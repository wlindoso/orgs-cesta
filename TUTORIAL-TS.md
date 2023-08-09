# Criando arquivo package.json

no prompt: `npm init` ou `npm init -y`

# Instalando Typescript

no prompt: `npm install -q typescript` global (-g),estará presente em todos os projetos

# Criando arquivo tsconfig.json

no prompt: `tsc --init`

- Dentro da raíz, vamos criar pasta src(códigos ts) e dist(códigos compilados em js)
- Dentro da pasta src, vamos criar nosso primeiro arquivo chamado de index.ts
- Para rodar um código typescript não podemos utilizar o comando _node caminho/index.ts_, ocorreia um _SyntaxError_

# Configurando o Typescript

- Abrir arquivo tscionfig.json e modificar o _"target": "es2016"_ para _"target": "es6"_
- Adicionar logo na linha abaixo do _target_ a linha _"moduleResolution": "node"_ informando que irá rodar código node.
- Informar a pasta do projeto(src) e a pasta destino(dist)
- Ainda no arquivo tsconfig.json procurar a linha: _"rootDir": "./src"_ e _"outDir": "./dist"_

no prompt: `npm install --save-dev @types/node` estará presente apenas no desenvolvimento e não no projeto final.

- Algumas pastas irão aparecer:
- node_modules\@types\node -> módulos do node
- Caso tenha baixado esse projeto do git sem a pasta do node_modules

no prompt: `npm install` e o arquivo package.json será lido e instalado os módulos necessários

# Testando o projeto

- Deixar o TS monitorando apra semrpe que houver modificações, criar o compilado na pasta dist
- utilizando dois terminais:

no primeiro prompt: `tsc -w` watch mode(-w) _monitorando..._

no segundo prompt: `node .\dist\index.js` rodar nosso arquivo JS dentro da pasta _dist_

# Scripts do package.json

"scripts": {
"start": "node dist/index.js",
"watch-ts": "tsc -w"
}

no prompt: `npm run start` ou `npm start` atalho para o start do nosso projeto
no prompt: `npm run watch-ts` atalho para o modo watch mode

# Importando/exportando funções com CommonJS

- Utilizar `module.exports.somar = somar;` Exportando utilizando o nome da função(indicado)
- Utilizar `const Matematica = require("./Matematica");` Importando em uma const com o nome do módulo
- Utilizar `Matematica.somar(10, 2);` para utilizar a função desejada

# Importando/exportando funções com ES6 - mais moderno

- Utilizar `export function somar(x: number, y: number): number {return x + y;}` Exportando a função somar
- Utilizar `import { somar, subtrair } from "./Matematica";` Importando apenas a função somar e subtrair do módulo Matemática
- Utilizar `somar(10, 2);` para utilizar a função desejada
- Utilizar `import * as Matematica from "./Matematica";` Importando o módulo Matemática inteiro
- Utilizar `Matematica.somar(10, 2);` para utilizar a função desejada

- Outra forma seria:
- Utilizar `export default { somar };` Exportando a função somar
- Utilizar `import Matematica from "./Matematica";` Importando o módulo Matemática inteiro
- Utilizar `Matematica.somar(10, 2);` para utilizar a função desejada

# Instalando bibliotecas de terceiros

no prompt: `npm i nome_da_biblioteca` ou `npm install nome_da_biblioteca`

- Instalando a biblioteca _validator_ `npm install validator`
- A validator é uma biblioteca que podemos instalar tb o seu types `npm install --save-dev @types/validator`
- No projeto utilizar o código: `import validator from 'validator';` importando a biblioteca validator
- Utilizar `validator.isIP(192.168.1.256);` nome do import seguido da função.

# Instalando o Nodemon

- no prompt: `npm install -g nodemon` ela possui um DT porém não precisamos dele por eqnuanto
- para instalar o types(DT) no prompt: no prompt: `npm install -g @types/nodemon`
- Agora para rodar nossos códigos utilizamos o comando `nodemon ./dist/index.js`
- para interromper um prompt onde o nodemon esteja rodando: CTRL + C

# Nodemon com o Typescript - ts-node

- Vamos passar a utilizar apenas um terminal o ts-node
- no prompt: `npm intall -g ts-node`
- Para rodar, no prompt: `ts-node src/index.js`
- Desta forma ele verificar que é um arquivo _.ts_ e converte nas pasta _dist_ e depois roda.
- A partir de agora não preciso mais utilizar dois terminais para rodar o watch mode e o codigo `dist/index.js`
- Na verdade nem precisamos mais da pasta _dist_, podemos até apagar.
- Daí o nodemon já estará integrado com o ts-node e funcionará sempre que alterações forem salvas em noso projeto _.ts_
- Podemos simplificar ainda mais, indo no _package.json_ em nossos scripts e criar um script especifico.
  ex.: "start-dev": "nodemon src/index.ts" e remover o "watch-ts": "tsc -w" já que não precisamos monitorar separadamente mais.

# Instalando o Express (criação de servidores web)

- no prompt: `npm install express`
- Agora precisamos importar para poder utilizar em nosso projeto
- Criando um novo arquivo _server.ts_ utilizamos: `import express from "express";`
- Agora precisaremos de uma const para capturar o express(); `const server = express();`
- o express tem DT(types) e para instalar vamos no prompt: `npm install @types/express`
- Para que nosso projeto rode no _server.ts_ podemos modificar apeans o "start-dev": "nodemon src/server.ts"

## Arquivo básico / servidor no express / _server.ts_

import express, { Request, Response } from "express";
const server = express();
server.get("/", (req: Request, res: Response) => {
res.send("Olá mundo!");
});
server.listen(3000); _porta padrão é 80_

- para testar podemos em um navegador digitar o endereço: _http://localhost:3000_

# Rotas - "/" | "/contato" | "/logos/imagem.jpg" | "/noticias/noticia-01"

# Instalando Mustache - template engine

no prompt: `npm install mustache-express`
no prompt: `npm install --save-dev @types/mustache-express` (DTs)

# Padrão MVC (um conceito)

M -> Model => Regras de negócio, processamento dos dados
V -> View => Visualização, parte visual(html, css ...)
C -> Controller => Faz o gerenciamento de tudo
