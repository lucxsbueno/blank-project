
# ES6

 Passo a passo da criação de um projeto em branco utilizando as últimas `features ` do `ES6+` compatível com outras versões do `Javascript`.

#### Iniciando o projeto

Crie um diretório e em seguida acesse ele:

```bash
$ mkdir meu-projeto
$ cd meu projeto
```
#### Iniciando o gerenciador de pacotes (package manager) 

Um `gerenciador de pacotes` é uma coleção de ferramentas de software que automatiza o processo de instalação, atualização, configuração e remoção de programas de computador para o sistema operacional de um computador de forma consistente.

```bash
$ yarn init
```

#### Babel

O Babel é um transcompilador `JavaScript` de código aberto e gratuito usado principalmente para converter o código `ECMAScript 2015+` em uma versão compatível com versões anteriores do `JavaScript` que pode ser executada por mecanismos `JavaScript` mais antigos.

Instale da interface de linha de comando do babel, e outras dependências.

```bash
$ yarn add @babel/cli --dev
$ yarn add @babel/preset-env --dev
$ yarn add @babel/core --dev
```

> O comando ```--dev``` é usado para definir que a dependência será usada apenas a nível de desenvolvimento e não de produção, caso a dependência não seja de desenvolvimento basta apenas tirar que ela será instalada em ```dependencies```

Crie um arquivo com o nome de ```.babelrc```

Ele entende qual o ambiente estamos trabalhando e converte para as `features` que navegadores mais antigos não entendem

Crie um arquivo com o nome de `index.html` e outro `main.js`

Dentro do arquivo `main.js`, adicione algum código para teste, de preferência que não exista antes do `ES6`.

Exemplo:

```js
class Teste {
    metodo(){
        console.log("Olá mundo!");
    }
}
```

No seu ```package.json```, adicione a propriedade `scripts`:

```json
"scripts": {
    "dev": "babel ./main.js -o .bundle.js -w"
}
```

> O comando ```-w ``` faz com que ele monitore o arquivo cada vez que é salvo, fazendo com que não seja necessário rodar o script todas as vezes que salvamos o arquivo. 

E por fim, execute o comando:

```bash
$ yarn dev
```

> Note que foi criado o arquivo ```bundle.js```, ele é o resultado do transcompilador do babel que como dito anteriormente, faz com que seu código seja interpretado por todos os navegadores, anteriores ao ES6.

#### Webpack Server

O `webpack` é um empacotador de módulo `JavaScript` de código aberto. É feito principalmente para `JavaScript`, mas pode transformar ativos de `front-end`, como `HTML`, `CSS` e imagens, se os carregadores correspondentes forem incluídos.

#### Instalação

```sh
$ yarn add webpack webpack-cli --dev
```

Crie o arquivo `webpack.config.js`

Ele sempre será o nosso arquivo principal de configuração do `webpack`

Dentro do arquivo de configuração do `webpack`, adicione estas linhas de código:

```js
module.exports = {
    entry: './main.js',
    output: {
        path: __dirname,
        filename: '.bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: 'babel-loader'
            }
        ]
    }
}
```

Adicione a dependência de desenvolvimento `babel-loader`

```bash
$ yarn add babel-loader@8.0.0-beta.0 --dev
```

Se caso chegou até aqui, no arquivo ```package.json``` altere o scripts para: 

```js
"scripts": {
    "dev": "webpack --mode=development -w"
}
```

Crie uma arquivo `calc.js` e adicione:

```js
export default function (a, b) {
    return a + b;
}
```

Depois importe a função na sua `main.js`:

```js
import calc from './calc';

class Teste {
    metodo() {
        console.log("Olá mundo!");
    }
}

console.log(calc(2, 2));
```

Execute o comando:

```sh
$ yarn dev
```

### Enjoy!!! :smile: