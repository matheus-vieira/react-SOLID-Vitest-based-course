---
layout: default
title: "Hooks Essenciais"
---

React Hooks são funções que permitem usar o estado e outras funcionalidades do React sem escrever classes.

Dois dos hooks mais fundamentais são `useState` e `useEffect`.

Eles tornam a gestão de estado e efeitos colaterais mais simples e declarativa.

## `useState`

O hook `useState` é usado para adicionar e gerenciar estado local em componentes funcionais.

### `useState` sintaxe

```javascript
const [state, setState] = useState(initialValue);
```

> `state`: O valor atual do estado.\
> `setState`: Função que atualiza o valor do estado.\
> `initialValue`: O valor inicial do estado.

### `useState` exemplo prático

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

> **Explicação:**\
> `useState(0)` inicializa o estado com valor 0.\
> A função `setCount` atualiza o estado e força uma re-renderização do componente.

## `useEffect`

O hook `useEffect` lida com efeitos colaterais, como chamadas a APIs, assinaturas de eventos ou manipulações diretas do DOM.

### `useEffect` sintaxe

```javascript
useEffect(() => {
  // Código do efeito
  return () => {
    // Cleanup (opcional)
  };
}, [dependencies]);
```

> **Callback**: Função contendo o efeito.\
> **Dependencies**: Array opcional que controla quando o efeito é executado.

### `useEffect` exemplo prático

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(interval); // Cleanup
  }, []);

  return <p>Tempo: {seconds} segundos</p>;
}

export default Timer;

```

> **Explicação:**
>
> O intervalo é iniciado quando o componente é montado.
>
> A função de limpeza (`clearInterval`) é chamada quando o componente é desmontado.

## Comparação com Ciclos de Vida do AngularJS

No AngularJS, os ciclos de vida dos componentes são gerenciados por métodos como `ngOnInit`, `$watch`, e `$destroy`.

React substitui esses métodos por hooks mais declarativos.

Tabela de Comparação

| React (Hooks)        | AngularJS (Ciclos de Vida) | Comparação                                        |
| useState             | `$scope` ou `this`         | React isola o estado dentro do componente.        |
| useEffect (mount)    | `ngOnInit`                 | Executa código inicial ao montar o componente.    |
| useEffect (update)   | `$watch`                   | Monitora mudanças específicas no estado ou props. |
| useEffect (cleanup)  | `$destroy`                 | Código de limpeza executado automaticamente.      |

### Principais Diferenças

Em React, o gerenciamento de estado e efeitos colaterais é mais granular e modular.
React Hooks eliminam a necessidade de um ciclo de vida complexo como o `$digest` do AngularJS.

| |
|---|:--:||--:|
|[Primeiro Componente]({{ '1-introducao-react/1.3-primeiro-componente' | relative_url}}) | [Início]({{ '/' | relative_url}}) | [Renderização condicional e listas]({{ '2-conceitos-fundamentais/2.2-renderizacao-condicional-listas' | relative_url}}) |
