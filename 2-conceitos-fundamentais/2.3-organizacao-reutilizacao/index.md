---
layout: default
title: "Organização e Reutilização"
---

Manter um código bem organizado e reutilizável é essencial para criar projetos escaláveis e de fácil manutenção.

Em React, conceitos como o **Princípio de Responsabilidade Única** e a **Separação de Lógica e Apresentação** ajudam a alcançar esse objetivo.

## Princípio de Responsabilidade Única (Single Responsibility Principle - SRP)

O Princípio de Responsabilidade Única (SRP) estabelece que cada componente deve ter **uma única responsabilidade** ou função bem definida.

## **Por que seguir o SRP?**

> Facilita a **reutilização** de componentes.\
> Melhora a **legibilidade** do código.\
> Simplifica os **testes unitários** e a depuração.

### Exemplo: Componentes com SRP

Vamos criar dois componentes: um para exibir um item da lista e outro para renderizar a lista completa.

```jsx
// Componente responsável por exibir um único item
function ListItem({ item }) {
  return <li>{item}</li>;
}

// Componente responsável por renderizar a lista
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

> Vantagens:\
> `ListItem` cuida apenas da exibição de um item.\
> `List` é responsável apenas por iterar sobre os dados e renderizar itens.

## Separação de Lógica e Apresentação

Separar a lógica de negócios da apresentação melhora a clareza e modularidade do código.

A lógica deve ser encapsulada em funções, hooks personalizados ou serviços, enquanto a apresentação deve focar na renderização de elementos visuais.

### Exemplo: Lógica e Apresentação Separadas

Lógica (API mock):

```jsx
// Lógica de negócio
function fetchMockData() {
  return Promise.resolve([
    { id: 1, name: 'Produto A' },
    { id: 2, name: 'Produto B' },
    { id: 3, name: 'Produto C' },
  ]);
}
```

Apresentação (Componente React):

```jsx
import React, { useState, useEffect } from 'react';
import { fetchMockData } from './api'; // Importando a lógica

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetchMockData().then((data) => setProducts(data));
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

> **Benefícios da Separação:**\
> Reutilização: A função `fetchMockData` pode ser reutilizada em diferentes componentes.\
> Testabilidade: É mais fácil testar a lógica isoladamente.\
> Manutenção: Alterações na lógica ou na apresentação não impactam diretamente a outra parte.

## Exercício Prático: Lista Dinâmica com API Mock

Criar uma aplicação React que consuma dados de uma API mock, organize a lógica e a apresentação separadamente, e aplique o Princípio de Responsabilidade Única.

> Passo a Passo\
> Crie uma função para simular uma API que retorna dados.\
> Desenvolva um componente para exibir os itens da lista.\
> Implemente a separação entre lógica e apresentação.

### Código Completo

#### Lógica (API Mock)

```javascript
// api.js
export function fetchMockData() {
  return Promise.resolve([
    { id: 1, name: 'Produto A' },
    { id: 2, name: 'Produto B' },
    { id: 3, name: 'Produto C' },
  ]);
}
```

#### Apresentação (Componente)

```jsx
// ProductList.js
import React, { useState, useEffect } from 'react';
import { fetchMockData } from './api';

// Componente responsável por exibir um único produto
function ProductItem({ product }) {
  return <li>{product.name}</li>;
}

// Componente principal que exibe a lista de produtos
function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetchMockData().then((data) => setProducts(data));
  }, []);

  return (
    <div>
      <h1>Lista de Produtos</h1>
      <ul>
        {products.map((product) => (
          <ProductItem key={product.id} product={product} />
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```

## Conclusão

> Princípio de Responsabilidade Única: Garante que cada componente tem uma responsabilidade clara.\
> Separação de Lógica e Apresentação: Facilita a reutilização, teste e manutenção do código.\
> Exercício Prático: Aplicar esses conceitos criando uma lista dinâmica com dados provenientes de uma API mock.

Praticar esses padrões de organização ajudará a escrever um código React mais limpo, escalável e fácil de entender.

| |
|---|--:|
| [Renderização condicional e listas]({{ '2-conceitos-fundamentais/2.2-renderizacao-condicional-listas' | relative_url}}) | [Componentes Desacoplados]({{ '3-componentes-testaveis/3.1-componentes-desacoplados' | relative_url}}) |
