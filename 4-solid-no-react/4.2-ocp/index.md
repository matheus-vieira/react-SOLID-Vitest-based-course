---
layout: default
title: "SOLID - Princípio Aberto/Fechado (Open/Closed Principle - OCP)"
---

> S - Single Responsibility Principle\
> ***O - Open/Closed Principle***\
> L - Liskov Substitution Principle\
> I - Interface Segregation Principle\
> D - Dependency Inversion Principle

O **Princípio Aberto/Fechado (OCP)**, parte do SOLID, afirma que **o software deve estar aberto para extensão, mas fechado para modificação**.

Isso significa que podemos adicionar novas funcionalidades ao sistema sem alterar o código existente, reduzindo o risco de introduzir bugs.

No contexto do React, o OCP pode ser aplicado usando técnicas como **High Order Components (HOCs)** e **`Render Props`**, que permitem adicionar funcionalidades a componentes de maneira extensível.

## Entendendo o OCP no React

### O que o OCP Representa?

> **Aberto para Extensão:** Você pode adicionar funcionalidades sem alterar o código original.\
> **Fechado para Modificação:** A lógica existente permanece intacta e segura.

Esses objetivos são alcançados ao abstrair comportamentos e permitir que novos elementos estendam a funcionalidade sem modificar a base.

## Uso de High Order Components (HOCs)

### O que são HOCs?

Um **High Order Component** é uma função que recebe um componente como argumento e retorna um novo componente, adicionando comportamentos ou lógica.

#### **Estrutura Básica:**

```javascript
function withFeature(WrappedComponent) {
  return function EnhancedComponent(props) {
    // Lógica adicional
    return <WrappedComponent {...props} />;
  };
}
```

##### Exemplo: Logging com HOC

Adicionamos um comportamento de logging sem modificar o componente original.

HOC para Logging:

```javascript
function withLogging(WrappedComponent) {
  return function EnhancedComponent(props) {
    console.log(`Componente renderizado com props:`, props);
    return <WrappedComponent {...props} />;
  };
}
```

Componente Base:

```javascript
function Button({ label }) {
  return <button>{label}</button>;
}
```

Componente Estendido:

```javascript

const LoggedButton = withLogging(Button);

function App() {
  return <LoggedButton label="Clique Aqui" />;
}
```

> **Vantagens**\
> Reutilizabilidade: Lógica pode ser aplicada a vários componentes.\
> Modularidade: O componente base permanece inalterado.

## Uso de `Render Props`

O que são `Render Props`?

`Render Props` é um padrão em que um componente aceita uma função como prop para determinar o que será renderizado.

Essa técnica é útil para compartilhar lógica entre componentes.

### Estrutura Básica

```javascript
function RenderPropComponent({ render }) {
  const data = "Olá, mundo!";
  return render(data);
}
```

#### Exemplo: Componente de Toggle

Componente Base com `Render Props`:

```javascript
function Toggle({ render }) {
  const [isToggled, setToggled] = React.useState(false);

  const toggle = () => setToggled(!isToggled);

  return render({ isToggled, toggle });
}
```

#### Uso do Componente

```jsx
function App() {
  return (
    <Toggle
      render={({ isToggled, toggle }) => (
        <div>
          <p>Status: {isToggled ? "Ligado" : "Desligado"}</p>
          <button onClick={toggle}>Alternar</button>
        </div>
      )}
    />
  );
}
```

> Vantagens\
> Flexibilidade: A lógica do comportamento é separada da renderização.\
> Reutilização: O mesmo componente pode ser usado para diferentes apresentações.\

## Comparando HOCs e `Render Props`

| Aspecto        | HOCs                                              | `Render Props`                                        |
| Estrutura      | Função que retorna um novo componente             | Componente que aceita uma função como prop            |
| Uso            | Extensão de lógica ou comportamento               | Compartilhamento de lógica com renderização flexível  |
| Composição     | Pode ser aninhado (decoradores)                   | Mais claro quando usado para casos específicos        |
| Complexidade   | Pode gerar problemas como "aninhamento de HOCs"   | Mais explícito e fácil de depurar                     |

## Exercício Prático

Crie um componente que registra cliques no botão e compartilha essa lógica entre diferentes implementações.

### Passo 1: Crie o HOC

```jsx
function withClickLogger(WrappedComponent) {
  return function EnhancedComponent(props) {
    const handleClick = () => console.log("Botão clicado!");
    return <WrappedComponent {...props} onClick={handleClick} />;
  };
}
```

### Passo 2: Crie o Componente Base

```jsx
function Button({ label, onClick }) {
  return <button onClick={onClick}>{label}</button>;
}
```

### Passo 3: Use o HOC

```jsx
const LoggedButton = withClickLogger(Button);

function App() {
  return <LoggedButton label="Clique Aqui" />;
}
```

### Passo 4: Alternativa com Render Props

```jsx
function ClickLogger({ render }) {
  const handleClick = () => console.log("Botão clicado!");
  return render(handleClick);
}

function App() {
  return (
    <ClickLogger
      render={(handleClick) => (
        <button onClick={handleClick}>Clique Aqui</button>
      )}
    />
  );
}
```

## Conclusão

HOCs e `Render Props` no Contexto do OCP:

Ambos ajudam a estender funcionalidades sem modificar o código original, seguindo o princípio aberto/fechado.

Escolha entre HOCs ou `Render Props` depende da clareza e do uso pretendido.

Aplicar o OCP com HOCs e `Render Props` resulta em componentes modulares, reutilizáveis e alinhados com boas práticas de desenvolvimento.

| |
|---|--:|
| [SOLID - Open/Closed Principle - (OCP)]({{ '4-solid-no-react/4.1-srp' | relative_url}}) | [SOLID - Liskov Substitution Principle (LSP)]({{ '4-solid-no-react/4.3-lsp' | relative_url}}) |
