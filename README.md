# LearningJS

## Tópicos estudados

* [ArrowFunctions](#ArrowFunctions)
* [Desctructuring](#Desctructuring)
* [Spread Operator](#SpreadOperator)
* [Set](#Set)
* [WeakSet](#WeakSet)
* [Map](#Map)
* [Copy Array](#CopyArray)
* [IIFE](#IIFE)
* [Symbol](#Symbol)
* [Promises](#Promises)
* [Proxy](#Proxy)

## ArrowFunctions <a id="ArrowFunctions"></a>

As ArrowFunctions são expressões que possuem as seguintes regras:

* Quando possuir mais de um parametro, eles devem ser passados em parênteses ();
* Quando o código dentro da função possui mais de uma linha é necessário ficar entre chaves {};
* Ao utilizá-la em somente uma linha automaticamente você assume que o valor passado após a *arrow* é o `return` daquela função;


### Exemplo 01
Retorna o Array com todas as letras maiúsculas

```js
let nomes = ['Felipe', 'Siqueira', 'Dev'].map( nome => nome.toUpperCase());
console.log(nomes);

//["FELIPE", "SIQUEIRA", "DEV"]

 ```

### Exemplo 02
Retorna o Array com uma frase

```js
let nomes = ['Felipe', 'Siqueira', 'Dev'].map( nome => {
    nome = nome.toUpperCase();
    return `${nome} tem ${nome.length} caracteres`;
});
console.log(nomes);

//["FELIPE tem 6 caracteres", "SIQUEIRA tem 8 caracteres", "DEV tem 3 caracteres"]

 ```

 ### Exemplo 03
 Retorna o primeiro número primo de um Array

```js
let arr = [1, 6, 8, 2, 4].findIndex((element, index, array) => {
        let start = 2;
        while (start <= Math.sqrt(element)) {
          if (element % start++ < 1) {
            return false;
          }
        }
        return element > 1;
    });
console.log(arr);

//3

```

 ## Desctructuring <a id="Desctructuring"></a>

 Desctructuring é uma forma de substituir valores de Array ou Object para variáveis.

### Exemplo 01

```js
let arr = [10, 20, 30];

let [x, y, z] = arr;

console.log(x, y, z);
//10, 20, 30

```

### Exemplo 02

```js
let carro = {  
  cor: 'preto',
  peso: 808,
  airbag: true
};

let {cor, peso, airbag} = carro;

console.log(cor, peso, airbag);
//preto 808 true
 ```

### Exemplo 03

```js
function setarTamanho([width = 5, height = 5] = []) {
  return `Largura de ${width}px e altura de ${height}px`;
}

setarTamanho([10, 10]);
//"Largura de 10px e altura de 10px"

setarTamanho();
//"Largura de 5x e altura de 5px"

```


 ## Spread Operator <a id="SpreadOperator"></a>
 O Spread Operator serve para passar vários parametros para uma função sem declarar cada parametro separadamente.

 Serve também para concatenar mais de um Array

### Exemplo 01

```js
function imprimirConteudo(...itens){
    for (let item of itens){
        console.log(item);
    }
}

imprimirConteudo('cão', 'gato', 'pato', 'pássaro');
/*
cão
gato
pato
pássaro
*/
```

### Exemplo 02

```js
let comidas = ['queijo', 'ovos', 'pão'];
let bebidas = ['leite', 'suco', 'café'];

let alimentos = [...comidas, ...bebidas];
console.log(alimentos);
//queijo ovos pão leite suco café

```


## Set <a id="Set"></a>

O Objeto Set é parecido com Array, mas não possuem indices, ou seja, os itens de um Set não podem ser acessados individualmente.
E também não aceita itens duplicados como em Array.
Para inserir ou remover itens em um Set, basta usar as funções "add" e "delete".
A função "has" serve para verificar se um item existe dentro do Set.

### Exemplo 01

```js
let jogos = new Set(['Super Mario', 'Top Gear', 'Mortal Kombat', 'Super Mario']);
console.log(jogos);
//Set {'Super Mario', 'Top Gear', 'Mortal Kombat'}
```

### Exemplo 02

```js
let jogos = new Set(['Super Mario', 'Top Gear', 'Mortal Kombat', 'Super Mario']);
jogos.add('Street Figther');
console.log(jogos);
//Set {'Super Mario', 'Top Gear', 'Mortal Kombat', 'Street Fighter'}
```

### Exemplo 03

```js
let jogos = new Set(['Super Mario', 'Top Gear', 'Mortal Kombat', 'Super Mario']);
console.log(jogos.has('Street Figther'));
//true
```


## WeakSet <a id="WeakSet"></a>

O Objeto WeakSet é parecido com Set, mas só aceita Objetos.
Não é possível fazer iteração com um WeakSet

### Exemplo 01

```js
let pessoa01 = { nome: 'Felipe', peso: 60, altura: 1.6};
let pessoa02 = { nome: 'Lucas', peso: 75, altura: 1.75};

let pessoas = new WeakSet([pessoa01, pessoa02]);
console.log(pessoas);
//WeakSet [{ nome: 'Felipe', peso: 60, altura: 1.6}, { nome: 'Lucas', peso: 75, altura: 1.75}]
```

## Map <a id="Map"></a>

Maps são parecidos com Objeto, tendo chave e valor, mas tanto a chave quanto o valor podem ser objetos.
Para inserir valores a uma váriavel do tipo Map é usado a função "set" e para remover usa-se a função delete.

Se inserir uma informação com a chave repetida o valor será substituido pelo novo valor.

### Exemplo 01

```js
let empregados = new Map();

empregados.set("felipe@email.com", {
  nome: "Felipe",
  idade: 26,
  funcao: "Dev"
});

empregados.set("lucas@email.com", {
  nome: "Lucas",
  idade: 27,
  funcao: "FrontEnd"
});
```


### Exemplo 02

```js
empregados.delete("felipe@email.com");

```

## WeakMap <a id="WeakMap"></a>

Parecido com o Map, mas a chave deve ser obrigatóriamente um objeto

### Exemplo 01

```js
let pessoa = new WeakMap();
pessoa.set({nome: "Felipe", sobrenome: "Siqueira"}, {profissao: "Dev", salario: "$$$"});
```

## Copiar Array <a id="CopyArray"></a>

A forma mais correta para copiar um array é usando a função "Slice", pois uma variável do tipo Array é referenciada com um apontamento de mémoria.
Por isso se simplesmente associar um váriavel a outra irá somente apontar para o mesmo endereço de mémoria.

### Exemplo 01

```js
function CopyArray(arr){
    return Array.prototype.slice.call(arr);
}

let myArr = [1, 2, 3, 4, 5];
let myArr2 = myArr;
let myArr3 = copyArray(myArr);

console.log(myArr === myArr2);
//true

console.log(myArr === myArr3);
//false
```

## Função IIFE <a id="IIFE"></a>

A função IIFE é uma função auto-executavel e deve ser executada no inicio do arquivo

### Exemplo 01
```js
(function(){
  //codigo da função
}());

```

## Symbol <a id="Symbol"></a>

O Symbol é usado para se ter um objeto com mais de uma própriedade com o mesmo nome

### Exemplo 01

```js
const bowl1 = {
    [Symbol('apple')]: { color: 'red', weight: 136.078 },
    [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
    [Symbol('orange')]: { color: 'orange', weight: 170.097 },
    [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
};
```

## Promises <a id="Promises"></a>

Promises é uma nova forma de fazer chamadas assincronas.
Ao se criar uma Promises é passado 2 funções como parametros, uma para retorno com sucesso (resolve) e outra para retorno de erro (reject)
O retorno das funções são acessados dentro da função "then" da Promise

### Exemplo 01

```js
let myPromise = new Promise(function(resolve, reject){
  //caso retorno com erro
  if (/*condição do erro*/){
    reject('Erro ao executar Promise');
  }
  resolve('Objeto de retorno de sucesso');
});

myPromise.then(function resolve(objSucesso){
  console.log(objSucesso);
}, function reject(objErro){
  console.log(objErro);
});
```

## Proxy <a id="Proxy"></a>

O Objeto do tipo Proxy serve que um objeto possa responder por outro.
O construtor do objeto do tipo Proxy recebe dois parametros. 
1º - Objeto que ele representará
2º um objeto com os métodos que serão usados no acesso aos dados do primeiro. Este é chamado de handler

### Exemplo 01

```js
var pessoa = {nome: 'Felipe'};
var dev = new Proxy(pessoa, {});

console.log(dev.nome);
//Felipe
```

### Exemplo 02

```js
var pessoa = {nome: 'Felipe'};
var dev = new Proxy(pessoa, {
  get(target, propName){
    console.log(target);
    console.log(propName);
    return target[propName];
  }
});

console.log(dev.nome);
//{nome: "Felipe"}
//nome
//Felipe
```