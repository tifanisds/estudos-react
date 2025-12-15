# React Element

## O que é o React Element
React Element é a menor unidade que o React utiliza para descrever a interface.
Ele é um objeto JavaScript que representa o que deve aparecer na tela, **mas não é o HTML real e não é um componente**.

Quando você escreve JSX, o que o React realmente cria por baixo dos panos é um React Element. Esse elemento contém informações como o tipo do que será renderizado (uma tag HTML ou um componente), as propriedades e o conteúdo. O React usa essa descrição para decidir como montar ou atualizar a interface.

### Diferença entre elemento e componente
Um componente é uma função (ou classe) cuja responsabilidade é criar e retornar React Elements.
Já o React Element é o resultado dessa execução, ou seja, o objeto que descreve a interface naquele momento.

Toda vez que um componente é utilizado, ele é executado e retorna um novo React Element. O React nunca renderiza o componente diretamente; ele sempre renderiza os elementos que o componente gera.


## React Element como objeto JavaScript
O React Element não é HTML e nem um elemento real do DOM. Ele é, antes de tudo, um objeto JavaScript comum, criado pelo React para descrever como a interface deve ser naquele momento.

Podemos pensar no React Element como um projeto de uma casa.
O projeto não é a casa de verdade, mas contém todas as informações necessárias para que a casa seja construída. O HTML/DOM seria a casa pronta; o React Element é o projeto.

### React Element não é HTML
Quando você escreve algo como:

```js
<h1>Olá</h1> 
//JavaScript não entende HTML dentro do código. Então isso não pode ser HTML de verdade

React.createElement('h1', null, 'Olá')
//Esse JSX é transformado em uma chamada de função: 
```

isso parece HTML, mas não é.
Esse código é convertido em um objeto JavaScript, que apenas descreve:

- qual tipo de elemento deve existir
- quais dados ele possui
- o que ele contém

O HTML real só é criado depois, quando o React decide renderizar esse elemento no DOM.

## Criando React Elements
Criar um React Element significa criar um objeto JavaScript que descreve a interface.
A forma mais direta e “pura” de fazer isso é usando a função React.createElement(). Tudo o que o React renderiza passa, em algum momento, por essa função, mesmo quando você usa JSX.

### Parâmetros da função
A função recebe três partes principais, que juntas formam a descrição do elemento.

O primeiro parâmetro é o **type**, que define o que está sendo criado.
Ele pode ser:
- uma string ('**div**', '**h1**', '**button**') quando é um elemento **HTML**
- um componente React quando se trata de outro componente

O segundo parâmetro é o **props**, um objeto com as propriedades daquele elemento.
Aqui entram atributos, valores e qualquer dado necessário para configurar o elemento.
Quando não há propriedades, esse valor costuma ser **null**.

O terceiro parâmetro (e os seguintes) representa o conteúdo interno, chamado de **children**.
Esse conteúdo pode ser texto, outro React Element ou vários elementos ao mesmo tempo.

### Exemplo sem JSX
Vamos criar um React Element sem usar JSX, apenas JavaScript puro:
```js
const element = React.createElement(
  'h1',
  {
    id: 'titulo',
    className: 'titulo-principal',
    title: 'Título da página'
  },
  'Olá, React'
);
```

## JSX e React Element
JSX é uma sintaxe, criada para facilitar a escrita de React Elements. Ele existe apenas para o desenvolvedor; o React nunca trabalha diretamente com JSX.

Quando você escreve JSX, você está apenas usando uma forma mais legível de criar React Elements, sem precisar chamar React.createElement manualmente o tempo todo.

### O que é JSX de verdade
JSX é uma extensão de sintaxe do JavaScript que permite escrever estruturas parecidas com HTML dentro do código. Porém, esse código não é executado como HTML.

Antes de rodar no navegador, o JSX é transformado em chamadas para React.createElement. Ou seja, todo JSX vira React Element.

```js
//Ao escrever
<h1 id="titulo">Olá</h1>

//o que realmente será executado é algo conceitualmente equivalente a:
React.createElement(
  'h1',
  { id: 'titulo' },
  'Olá'
);

```

## Renderização de React Elements
Um React Element é apenas uma descrição da interface em forma de objeto JavaScript. Para que ele apareça na tela, é necessário o processo de renderização, que é feito pelo ReactDOM.

O ReactDOM é a parte do React que se comunica diretamente com o navegador. Ele recebe o React Element e cria os elementos reais do DOM a partir dessa descrição.

Para iniciar esse processo, usamos ReactDOM.createRoot, que define qual elemento do HTML será controlado pelo React. Esse elemento funciona como o ponto onde toda a interface React será exibida.

Em seguida, utilizamos root.render(element), que envia o React Element para o ReactDOM. A partir disso, o React cria ou atualiza apenas o que for necessário no DOM, tornando o elemento visível para o usuário.

Em resumo: o React cria a descrição da interface, o ReactDOM transforma essa descrição em DOM real e o render é o comando que coloca a interface na tela.

```html
<!-- index.html -->
<div id="root"></div>
```

---

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom/client';

// 1. Criação de um React Element
const element = React.createElement(
  'h1',
  { id: 'titulo' },
  'Olá, React'
);

// 2. Criação do root (ponto de ligação com o DOM)
const root = ReactDOM.createRoot(
  document.getElementById('root')
);

// 3. Renderização do React Element na tela
root.render(element);

```

## Atualização de React Elements
Um ponto central do React é que React Elements são imutáveis.
Isso significa que, depois de criado, um React Element não é alterado. Ele representa uma “foto” da interface em um determinado momento.

Quando algo muda na aplicação, como um dado, uma interação do usuário ou um estado — o React não modifica o elemento antigo. Em vez disso, ele cria novos React Elements que representam a nova versão da interface.

Esses novos elementos são então comparados com os elementos anteriores. A partir dessa comparação, o React descobre exatamente o que mudou e decide quais partes do DOM real precisam ser atualizadas. Assim, apenas os trechos necessários da interface são modificados.

