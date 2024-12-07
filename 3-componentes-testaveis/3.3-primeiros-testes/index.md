---
layout: default
title: "Primeiros Testes em React"
---

Escrever testes para componentes React garante a qualidade e a confiabilidade do código.

Este guia aborda como testar a lógica de estados com hooks e como realizar testes de renderização usando `@testing-library/react`.

## Testando Lógica de Estados com Hooks

Hooks como `useState` e `useEffect` são fundamentais em React.

Testar sua lógica garante que os estados e efeitos funcionem corretamente.

### Exemplo: Testando um Componente com useState

Componente Simples

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Contador: {count}</p>
      <button onClick={() => setCount(count + 1)}>Incrementar</button>
    </div>
  );
}

export default Counter;
```

#### Teste para o Componente

Usaremos o Vitest para verificar se o estado e o comportamento do botão funcionam corretamente.

```typescript
import { render, fireEvent, screen } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import Counter from './Counter';

describe('Counter Component', () => {
  it('deve iniciar com valor zero', () => {
    render(<Counter />);
    expect(screen.getByText(/Contador: 0/)).toBeInTheDocument();
  });

  it('deve incrementar o contador ao clicar no botão', () => {
    render(<Counter />);
    const button = screen.getByText(/Incrementar/);

    fireEvent.click(button);
    expect(screen.getByText(/Contador: 1/)).toBeInTheDocument();
  });
});
```

> Conceitos Importantes:\
> `render`: Renderiza o componente para teste.\
> `fireEvent`: Simula interações do usuário (cliques, teclas, etc.).\
> `screen`: API para localizar elementos renderizados.

## 2. Testes de Renderização com @testing-library/react

A biblioteca `@testing-library/react` foca em testes que simulam o comportamento do usuário, verificando como o componente se apresenta e responde às interações.

### Exemplo: Testando Renderização com Props

Componente Baseado em Props

```jsx
function Greeting({ name }) {
  return <h1>Olá, {name}!</h1>;
}

export default Greeting;
```

#### Teste para Renderização

```javascript
import { render, screen } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import Greeting from './Greeting';

describe('Greeting Component', () => {
  it('deve renderizar a saudação com o nome fornecido', () => {
    render(<Greeting name="João" />);
    expect(screen.getByText(/Olá, João!/)).toBeInTheDocument();
  });

  it('deve falhar se o nome não corresponder', () => {
    render(<Greeting name="Maria" />);
    expect(screen.queryByText(/Olá, João!/)).toBeNull();
  });
});
```

> Métodos Importantes do screen:\
> `getByText`: Busca um elemento com o texto exato (lança erro se não encontrar).\
> `queryByText`: Busca um elemento com o texto exato, mas retorna null se não encontrar (não lança erro).

## Melhorando os Testes com Hooks Personalizados

Testar lógica encapsulada em hooks personalizados melhora a cobertura de testes e organiza o código.

Exemplo: Hook Personalizado

O Hook

```javascript
import { useState } from 'react';

export function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return { count, increment, decrement };
}
```

Testando o Hook

```javascript
import { renderHook, act } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import { useCounter } from './useCounter';

describe('useCounter Hook', () => {
  it('deve iniciar com o valor inicial fornecido', () => {
    const { result } = renderHook(() => useCounter(5));
    expect(result.current.count).toBe(5);
  });

  it('deve incrementar o contador', () => {
    const { result } = renderHook(() => useCounter());
    act(() => result.current.increment());
    expect(result.current.count).toBe(1);
  });

  it('deve decrementar o contador', () => {
    const { result } = renderHook(() => useCounter(10));
    act(() => result.current.decrement());
    expect(result.current.count).toBe(9);
  });
});
```

## Conclusão

### Testando Lógica de Estados

Garantimos que estados sejam atualizados corretamente.
Usamos fireEvent para simular interações do usuário.

### Testando Renderização

Verificamos a apresentação do componente com base em diferentes estados e props.

Usamos `@testing-library/react` para testes orientados ao usuário.

### Hooks Personalizados

`renderHook` e `act` são ferramentas essenciais para testes de hooks.

Com esses conceitos, você pode escrever testes mais confiáveis e criar componentes React robustos.

Experimente aplicar os exemplos em um projeto real para consolidar os conhecimentos!

| |
|---|--:|
| [Introdução Vitest]({{ '3-componentes-testaveis/3.2-introdução-vitest' | relative_url}}) | [SOLID - Single Responsibility Principle (SRP)]({{ '4-solid-no-react/4.1-srp' | relative_url}})
