# Componentes do React

## O que é um componente React
Um componente React é uma função JavaScript cuja responsabilidade é descrever uma parte da interface da aplicação.

Em vez de criar a interface inteira de uma vez, o React trabalha dividindo a UI em pequenas partes independentes, e cada uma dessas partes é um componente. Cada componente representa um pedaço da tela, como um botão, um título, um formulário ou uma seção completa.

Na prática, um componente recebe dados (por meio de props), pode ter seus próprios dados internos (estado) e retorna uma descrição de como aquela parte da interface deve ser exibida.

É importante entender que o componente não é a interface em si, mas sim quem gera a descrição da interface. O que aparece na tela é o resultado da renderização dos React Elements criados pelo componente.

Em resumo, um componente React existe para organizar, reutilizar e controlar partes da interface, tornando o código mais legível, modular e fácil de manter.

## Tipos de componentes
No React, existem dois tipos principais de componentes: componentes funcionais e componentes de classe. Ambos existem para resolver o mesmo problema, criar partes da interface, mas surgiram em momentos diferentes da evolução do React.

### Componentes funcionais
Os componentes funcionais são funções JavaScript que retornam uma descrição da interface. Eles são mais simples, mais diretos e hoje representam o padrão atual do React. Com a introdução dos Hooks, os componentes funcionais passaram a ter acesso a recursos como estado e ciclo de vida, tornando os componentes de classe desnecessários na maioria dos casos.

```js
function Contador() {
  const [count, setCount] = React.useState(0);

  return (
    <div>
      <p>Valor: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Incrementar
      </button>
    </div>
  );
}
```

### Componentes de classe
Os componentes de classe são uma forma mais antiga de criar componentes. Eles utilizam classes do JavaScript e métodos específicos para lidar com estado e ciclo de vida. Durante muito tempo, eram a única maneira de criar componentes mais complexos, mas hoje são considerados principalmente como contexto histórico e aparecem mais em códigos legados.

```js
class Contador extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  incrementar() {
    this.setState({
      count: this.state.count + 1
    });
  }

  render() {
    return (
      <div>
        <p>Valor: {this.state.count}</p>
        <button onClick={() => this.incrementar()}>
          Incrementar
        </button>
      </div>
    );
  }
}
```

Atualmente, a recomendação da comunidade e da própria documentação do React é utilizar componentes funcionais. Eles oferecem um código mais limpo, menor complexidade e melhor legibilidade, além de se integrarem melhor ao modelo mental moderno do React.

## Estrutura de um componente funcional
Um componente funcional em React é, antes de tudo, uma função JavaScript comum. A diferença é que essa função tem uma responsabilidade específica: retornar uma descrição da interface.

A estrutura básica de um componente funcional sempre segue a mesma ideia: definição da função, possível uso de hooks, e um return que contém JSX.

```js
function Titulo() { 
  return <h1>Olá, React</h1>;
}
```

- Titulo é o nome do componente (sempre com letra maiúscula)
- a função é o componente
- o return devolve JSX, que será transformado em React Elements

### Partes que compõem um componente funcional
Dentro de um componente funcional, podem existir:

- declarações de variáveis
- uso de hooks (como useState, useEffect)
- funções auxiliares
- lógica necessária para montar a interface

Tudo isso acontece antes do return.

O return é obrigatório, pois é nele que o componente descreve o que deve aparecer na tela. O que está no return não é HTML, mas JSX que será convertido em React Elements.

### O que não pode existir em um componente
Um componente funcional pode conter lógica JavaScript normal, mas ele não deve:

#### Modificar o DOM diretamente
```js
function Titulo() {
  document.querySelector('h1').innerText = 'Novo título';

  return <h1>Título</h1>;
}
```

- O React não controla essa mudança
- O React pode sobrescrever isso em um re-render
- Quebra o modelo declarativo do React

#### Alterar props recebidas
```js
function Saudacao(props) {
  props.nome = 'Maria';

  return <p>Olá, {props.nome}</p>;
}
```

- props são parâmetros
- alterar props quebra o fluxo de dados
- o componente deixa de ser previsível

#### Lógica pesada dentro do componente
```js
function Lista() {
  let total = 0;

  for (let i = 0; i < 100000000; i++) {
    total += i;
  }

  return <p>Total: {total}</p>;
}
```

- essa lógica roda toda vez que o componente renderiza
- deixa a interface lenta

## JSX dentro de componentes
Dentro de um componente funcional, o JSX é o que descreve a interface que aquele componente representa. Tudo o que aparece no return do componente é JSX e será convertido em React Elements.

O JSX permite misturar estrutura visual (parecida com HTML) com JavaScript, o que torna a descrição da UI mais clara e expressiva.

```js
function Saudacao() {
  const nome = 'Tifani';

  return <p>Olá, {nome}</p>; //Javascript entre chaves
}
```

## Props em componentes
As props são os parâmetros que um componente recebe quando é utilizado.
Como componentes são funções, as props funcionam exatamente como os argumentos de uma função JavaScript.

Elas servem para passar dados do componente pai para o componente filho, permitindo personalizar e reutilizar componentes.

```js
function Saudacao(props) {
  return <p>Olá, {props.nome}</p>;
}

function App() {
  return <Saudacao nome="Tifani" />;
}
```

É comum usar desestruturação para deixar o código mais limpo:

```js
function Saudacao({ nome }) {
  return <p>Olá, {nome}</p>;
}
```

### Props são somente leitura
Um componente não deve alterar suas props.
Elas pertencem a quem chamou o componente.

#### Não deve ser feito:
```js
function Saudacao(props) {
  props.nome = 'Maria';
  return <p>Olá, {props.nome}</p>;
}
```

## Estado (state) em componentes
O estado representa os dados internos de um componente que podem mudar ao longo do tempo. Diferente das props, o estado pertence ao próprio componente e pode ser alterado por ele.

Sempre que o estado muda, o React executa o componente novamente e atualiza a interface de acordo com o novo valor.

```js
function Contador() {
  const [count, setCount] = React.useState(0);
  //Count é estado e SetCount é a função responsável por atualizá-lo

  return (
    <div>
      <p>Valor: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Incrementar
      </button>
    </div>
  );
}
```

### Estado VS Props
- Props: vêm de fora do componente e não devem ser alteradas
- State: é interno ao componente e pode mudar

Podemos pensar que:
- props → configuram o componente
- state → controla o comportamento do componente

###
Quando você chama a função de atualização (setState):

1 - o React registra a mudança

2 - o componente é executado novamente

3 - novos React Elements são criados

4 - o React compara com os anteriores

5 - o DOM é atualizado se necessário

Você não atualiza a tela manualmente. O React faz isso automaticamente.

## Ciclo de vida (visão conceitual)
O ciclo de vida de um componente descreve as fases pelas quais um componente passa desde o momento em que ele aparece na tela até o momento em que ele é removido.

Mesmo em componentes funcionais, o ciclo de vida existe conceitualmente, ainda que hoje ele seja controlado principalmente por Hooks.

### As três grandes fases do ciclo de vida
Um componente React passa, de forma geral, por três momentos principais:

#### Montagem
É quando o componente é criado pela primeira vez e inserido na interface. O React executa a função do componente, cria os React Elements e coloca o resultado no DOM.

#### Atualização
Ocorre sempre que algo muda, normalmente uma mudança de estado ou de props. O componente é executado novamente e o React decide o que precisa ser atualizado na tela.

#### Desmontagem
Acontece quando o componente deixa de existir na interface. O React remove seus elementos do DOM e finaliza aquele componente.

<img src="../assets/img/ciclo-de-vida-componente.png" alt="Ciclo de vida dos componentes">

## Re-renderização de componentes
A re-renderização acontece quando o React executa novamente um componente para gerar novos React Elements. Isso não significa que o DOM inteiro será recriado, apenas que o React vai comparar o que mudou e atualizar a tela se necessário.

Um componente é re-renderizado principalmente quando:

- seu state muda
- suas props mudam
- o componente pai é re-renderizado

Durante a re-renderização, o React cria uma nova descrição da interface e compara com a anterior. Se houver diferenças, ele atualiza somente as partes necessárias do DOM.

## Comunicação entre componentes
No React, a comunicação entre componentes segue um fluxo de dados unidirecional. Isso significa que os dados sempre descem na hierarquia de componentes, do pai para o filho. Esse modelo torna a aplicação mais previsível e fácil de entender.

### Pai → Filho (props)
A forma mais comum de comunicação é o componente pai passar dados para o filho por meio de props. Como componentes são funções, as props funcionam como parâmetros.

```js
function Filho({ mensagem }) {
  return <p>{mensagem}</p>;
}

function Pai() {
  return <Filho mensagem="Olá vindo do pai" />;
}

```
O pai controla o valor e o filho apenas consome esse dado.

### Filho → Pai (funções como props)
Para um componente filho “enviar” algo para o pai, o pai passa uma função como prop. O filho chama essa função quando algum evento acontece.

```js
function Filho({ onClickBotao }) {
  return <button onClick={onClickBotao}>Clique</button>;
}

function Pai() {
  function lidarComClique() {
    console.log('Ação recebida do filho');
  }

  return <Filho onClickBotao={lidarComClique} />;
}
```
