---
layout: default
title: "1.3 Primeiro Componente"
---

Aprender React começa com a criação e renderização de componentes.

Nesta seção, exploraremos como criar componentes funcionais, usar **props** e **estado**, e finalizaremos com uma atividade prática.

### 1. Criar e Renderizar um Componente Funcional

Um componente em React é uma função ou classe que retorna uma interface de usuário (UI).

Vamos começar com um **componente funcional**, que é a abordagem moderna e mais usada.

#### Exemplo:

```jsx
// Componente funcional simples
function Greeting() {
  return <h1>Olá, Mundo!</h1>;
}

// Renderizando o componente
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<Greeting />, document.getElementById('root'));
```

> **Explicação:**
>
> - O componente `Greeting` retorna um elemento JSX (`<h1>`), que será renderizado no DOM.
> - O `ReactDOM.render` insere o componente no elemento com o ID `root` no HTML.

### 2. Uso de Props e Estado (State)

Os componentes podem receber entradas chamadas **props** (propriedades) e gerenciar dados locais com o **estado**.

### **Props**

Props permitem passar dados de um componente pai para um componente filho.

```jsx
function Greeting(props) {
  return <h1>Olá, {props.name}!</h1>;
}

// Usando o componente com props
ReactDOM.render(<Greeting name="João" />, document.getElementById('root'));
```

### **Estado**:

O estado é gerenciado internamente e permite que os componentes sejam dinâmicos.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button onClick={() => setCount(count + 1)}>Clique aqui</button>
    </div>
  );
}

// Renderizando o componente
ReactDOM.render(<Counter />, document.getElementById('root'));
```

> **Explicação:**
>
> - `useState(0)` define o estado inicial (`count`) como 0.
> - A função `setCount` atualiza o estado, e o React re-renderiza o componente.

## 3. Atividade Prática

Página "Olá, Mundo" com Componentes Reutilizáveis

Vamos criar uma página simples que exibe uma mensagem de boas-vindas e um contador de cliques, utilizando componentes reutilizáveis.

### Estrutura do Projeto:

### **`App.jsx`**

```jsx
import React from 'react';
import Greeting from './Greeting';
import Counter from './Counter';

function App() {
  return (
    <div>
      <Greeting name="Visitante" />
      <Counter />
    </div>
  );
}

export default App;
```

### **`Greeting.jsx`**

```jsx
import React from 'react';

function Greeting({ name }) {
  return <h1>Bem-vindo, {name}!</h1>;
}

export default Greeting;
```

### **`Counter.jsx`**

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button onClick={() => setCount(count + 1)}>Clique aqui</button>
    </div>
  );
}

export default Counter;
```

### Resultado

- A página mostrará uma saudação personalizada e um botão para incrementar o contador.

## **Conclusão**

**Componentes** tornam o código modular e reutilizável.

**Props** permitem a passagem de dados para componentes.

**Estado** adiciona interatividade e dinamicidade.

Siga os exemplos acima para dominar os fundamentos e pratique criando outros componentes!

| |
|---|--:|
|[Primeiro Componente]({{ '1-introducao-react/1.3-primeiro-componente' | relative_url}}) | [Hooks Essenciais]({{ '2-conceitos-fundamentais/2.1-hooks-essenciais' | relative_url}}) |
