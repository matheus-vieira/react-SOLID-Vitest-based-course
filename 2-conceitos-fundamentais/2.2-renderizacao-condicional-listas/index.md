---
layout: default
title: "Renderização Condicional e Listas"
---

React facilita a renderização condicional e a manipulação de listas dinâmicas.

Essas funcionalidades são essenciais para criar interfaces interativas e dinâmicas.

## Renderização Condicional

A renderização condicional em React permite exibir diferentes elementos ou componentes com base em uma condição.

### Operador ternário

O operador ternário é uma maneira concisa de renderizar elementos condicionalmente.

```jsx
import React, { useState } from 'react';

function ConditionalRendering() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {isLoggedIn ? <p>Bem-vindo, usuário!</p> : <p>Por favor, faça login.</p>}
      <button onClick={() => setIsLoggedIn(!isLoggedIn)}>
        {isLoggedIn ? 'Logout' : 'Login'}
      </button>
    </div>
  );
}

export default ConditionalRendering;
```

### Fragmentos

Fragmentos (`<></>`) permitem agrupar vários elementos sem adicionar nós extras no DOM.

```jsx
function FragmentExample() {
  return (
    <>
      <h1>Título</h1>
      <p>Este é um parágrafo dentro de um fragmento.</p>
    </>
  );
}

export default FragmentExample;
```

## Renderização de Listas

O método `map()` é amplamente utilizado para gerar listas dinâmicas em React.

### Exemplo com `map()`

```jsx
function ListExample() {
  const items = ['Item 1', 'Item 2', 'Item 3'];

  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

export default ListExample;
```

### Chave (key) em Listas

A propriedade key é essencial para ajudar o React a identificar itens únicos e otimizar a renderização.

## Organização e Reutilização

A organização do código é fundamental para manter a escalabilidade e a manutenibilidade do projeto.

> **Princípio de Responsabilidade Única (Single Responsibility Principle - SRP)**\
> Cada componente deve ter uma responsabilidade clara e única.

### Exemplo de separação de componentes

```jsx
function ListItem({ item }) {
  return <li>{item}</li>;
}

function List({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <ListItem key={index} item={item} />
      ))}
    </ul>
  );
}

export default List;

```

### Separação de Lógica e Apresentação

Mantenha a lógica de negócios separada da lógica de apresentação.

#### Exemplo

```jsx
// Lógica (API mock)
function fetchData() {
  return Promise.resolve(['Item A', 'Item B', 'Item C']);
}

// Apresentação
import React, { useEffect, useState } from 'react';

function DataList() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetchData().then((response) => setData(response));
  }, []);

  return (
    <ul>
      {data.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

export default DataList;
```

## Atividade Prática: Lista Dinâmica com API Mock

Criar uma lista dinâmica que consuma dados de uma API mock e os exiba.

### Etapas

1. Configure uma função mock que retorna dados simulados.
2. Use o hook `useEffect` para buscar os dados ao montar o componente.
3. Renderize os dados em uma lista dinâmica.

#### Código Exemplo

```jsx
// API Mock
function mockApi() {
  return Promise.resolve([
    { id: 1, name: 'Produto A' },
    { id: 2, name: 'Produto B' },
    { id: 3, name: 'Produto C' },
  ]);
}

// Componente
import React, { useState, useEffect } from 'react';

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    mockApi().then((response) => setProducts(response));
  }, []);

  return (
    <div>
      <h1>Lista de Produtos</h1>
      <ul>
        {products.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```

## Conclusão

> Renderização Condicional: Use o operador ternário e fragmentos para criar interfaces mais dinâmicas.\
> Renderização de Listas: Utilize o método map() para gerar elementos dinamicamente.\
> Organização: Separe a lógica da apresentação e mantenha cada componente focado em uma única responsabilidade.\
> Atividade Prática: Experimente criar listas dinâmicas que consomem dados de APIs mock para praticar esses conceitos.\

Pratique essas técnicas para dominar a criação de interfaces interativas e bem estruturadas em React!

| |
|---|:--:||--:|
|[Hooks Essenciais]({{ '2-conceitos-fundamentais/2.1-hooks-essenciais' | relative_url}}) | [Início]({{ '/' | relative_url}}) | [Organização e Reutilização]({{ '2-conceitos-fundamentais/2.3-organizacao-reutilizacao' | relative_url}}) |
