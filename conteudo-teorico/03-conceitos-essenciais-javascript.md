# JavaScript essencial para React

## Funções
Em JavaScript, funções são blocos de código reutilizáveis que podem receber valores (parâmetros), executar uma lógica e devolver um resultado (retorno).
No contexto do React, funções são ainda mais importantes porque componentes são funções

A forma mais tradicional de criar uma função é usando a palavra-chave function.
```js
function somar(a, b) {
  return a + b;
}
```

### Funções como valores
Em JavaScript, funções são valores, assim como números ou strings.
Isso significa que elas podem ser:

- armazenadas em variáveis
- passadas como argumento
- retornadas por outras funções

```js
const multiplicar = function (a, b) {
  return a * b;
};
```

### Arrow functions (() => {})
Arrow functions são uma forma mais curta de escrever funções.
Elas são muito usadas no React por serem mais simples e legíveis.

```js
const dividir = (a, b) => {
  return a / b;
};
```

Quando a função tem uma única expressão, o return pode ser implícito:

```js
const dobrar = (n) => n * 2;
```

No React, componentes funcionais geralmente são escritos assim:
```js
const Titulo = () => <h1>Olá</h1>;
```

### Parâmetros e retorno
Parâmetros são os dados de entrada da função.
O retorno é o resultado que a função produz.

```js
function saudacao(nome) {
  return `Olá, ${nome}`;
}
```

Se uma função não tem return, ela retorna undefined.
```js
function logar(msg) {
  console.log(msg);
}
```

## Escopo e contexto
Esses conceitos explicam onde variáveis e funções podem ser acessadas e como o JavaScript decide a quem this se refere. Eles são fundamentais para evitar bugs, especialmente em React.

### Escopo global e local
Escopo define onde uma variável existe e pode ser usada.

#### Escopo global
Uma variável declarada fora de qualquer função está no escopo global e pode ser acessada em qualquer lugar do código.

```js
const appName = 'Meu App';

function mostrarNome() {
  console.log(appName);
}
//appName é global
```

#### Escopo local (de função)
Variáveis declaradas dentro de uma função só existem dentro dela.
```js
function exemplo() {
  const mensagem = 'Olá';
  console.log(mensagem);
}

console.log(mensagem); //❌ erro

```

#### Escopo de bloco
O escopo de bloco é criado por {} em estruturas como if, for e while.

- let e const respeitam escopo de bloco
- var não respeita, pois ele vaza para fora desse bloco

```js
if (true) {
  const x = 10;
  let y = 20;
}

// x e y não existem aqui
console.log(x + y); //❌ erro
```

### Hoisting 
Hoisting é o comportamento em que declarações são “movidas” para o topo do escopo durante a execução.

#### Funções declaradas
```js
mostrar();

function mostrar() {
  console.log('Oi');
}

//Isso funciona por causa do hoisting.
```

#### Variáveis
```js
console.log(a);
var a = 10;
```

O javascript interpreta como:
```js
var a;
console.log(a); // undefined
a = 10;
```

Com let e const, isso não acontece:
```js
console.log(b);
const b = 5; // ❌ erro
```

### this (noções importantes)
O this representa o contexto de execução de uma função.
O valor de this depende de como a função é chamada, não de onde ela foi escrita.

```js
const pessoa = {
  nome: 'Ana',
  falar() {
    console.log(this.nome);
  }
};

pessoa.falar(); // Ana
//Aqui, this se refere ao objeto pessoa.
```

