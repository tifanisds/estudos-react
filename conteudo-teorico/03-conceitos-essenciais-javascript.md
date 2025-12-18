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


