---
layout: default
title: "SOLID - Princípio da Inversão de Dependência (Dependency Inversion Principle - DIP)"
---

> S - Single Responsibility Principle\
> O - Open/Closed Principle\
> L - Liskov Substitution Principle\
> I - Interface Segregation Principle\
> ***D - Dependency Inversion Principle***

O **Princípio da Inversão de Dependência (DIP)**, parte dos princípios SOLID, afirma que **módulos de alto nível não devem depender de módulos de baixo nível; ambos devem depender de abstrações**.

Além disso, **as abstrações não devem depender de detalhes, mas os detalhes devem depender de abstrações**.

Em React, esse princípio pode ser implementado utilizando **Context API** e **hooks customizados** para desacoplar funcionalidades e facilitar a reutilização e manutenção do código.

## Aplicando o DIP em React

### Por que Usar o DIP?

> **Desacoplamento:** Reduz o impacto de alterações nos módulos de baixo nível.\
> **Facilidade de Testes:** Permite substituir dependências por mocks durante os testes.\
> **Reutilização:** Componentes e funcionalidades podem ser reutilizados em diferentes contextos.

### DIP no Contexto de React

React facilita o DIP por meio de:

> **Context API:** Fornece dependências (dados ou lógica) de forma centralizada e acessível a qualquer componente.\
> **Hooks Customizados:** Encapsulam lógica específica e permitem abstrair dependências.

## Uso de Contextos e Hooks Customizados

### Exemplo Sem DIP

#### Problema: Dependência Direta

Imagine um sistema que exibe notificações diretamente em componentes de UI:

```jsx
function Notification({ message }) {
  return <div className="notification">{message}</div>;
}

function App() {
  const notify = (msg) => {
    alert(msg); // Lógica acoplada
  };

  return <button onClick={() => notify("Notificação enviada!")}>Notificar</button>;
}
```

Problema:

> A lógica de notificação (`alert`) está diretamente integrada ao componente de UI.\
> Substituir ou estender a lógica requer alterações no componente App.

### Aplicando DIP com Context API

#### Passo 1: Crie um Contexto

```jsx
import { createContext, useContext, useState } from "react";

const NotificationContext = createContext();

export function NotificationProvider({ children }) {
  const [message, setMessage] = useState(null);

  const notify = (msg) => setMessage(msg);

  return (
    <NotificationContext.Provider value={{ message, notify }}>
      {children}
    </NotificationContext.Provider>
  );
}
```

#### Passo 2: Crie um Hook Customizado

```jsx
export function useNotification() {
  return useContext(NotificationContext);
}
```

#### Passo 3: Consuma o Contexto em Componentes

```jsx
function Notification() {
  const { message } = useNotification();
  return message ? <div className="notification">{message}</div> : null;
}

function App() {
  const { notify } = useNotification();

  return (
    <div>
      <button onClick={() => notify("Notificação enviada!")}>Notificar</button>
      <Notification />
    </div>
  );
}
```

#### Envolva o Aplicativo com o Provedor

```jsx
import ReactDOM from "react-dom";
import { NotificationProvider } from "./NotificationContext";
import App from "./App";

ReactDOM.render(
  <NotificationProvider>
    <App />
  </NotificationProvider>,
  document.getElementById("root")
);
```

## Benefícios do DIP com Context e Hooks

> Desacoplamento: A lógica de notificação está isolada no contexto, permitindo alterar sua implementação sem impactar os componentes consumidores.\
> Facilidade de Testes: Você pode substituir o provedor real por um mock durante os testes.\
> Escalabilidade: Novas funcionalidades podem ser adicionadas ao contexto sem alterar os componentes consumidores.

## Exercício Prático: Sistema de Notificação SOLID

Crie um sistema de notificação que:

> Permita múltiplas mensagens.\
> Utilize o DIP para abstrair a lógica.\
> Inclua a opção de remover notificações.

### Passo 1: Atualize o Contexto

```jsx
export function NotificationProvider({ children }) {
  const [notifications, setNotifications] = useState([]);

  const addNotification = (msg) => {
    setNotifications((prev) => [...prev, { id: Date.now(), message: msg }]);
  };

  const removeNotification = (id) => {
    setNotifications((prev) => prev.filter((n) => n.id !== id));
  };

  return (
    <NotificationContext.Provider value={{ notifications, addNotification, removeNotification }}>
      {children}
    </NotificationContext.Provider>
  );
}
```

### Passo 2: Crie o Componente de Notificações

```jsx
function NotificationList() {
  const { notifications, removeNotification } = useNotification();

  return (
    <div className="notification-list">
      {notifications.map((n) => (
        <div key={n.id} className="notification">
          {n.message}
          <button onClick={() => removeNotification(n.id)}>Fechar</button>
        </div>
      ))}
    </div>
  );
}
```

### Passo 3: Integre na Aplicação

```jsx
function App() {
  const { addNotification } = useNotification();

  return (
    <div>
      <button onClick={() => addNotification("Nova Notificação!")}>Adicionar Notificação</button>
      <NotificationList />
    </div>
  );
}
```

### Passo 4: Estilização (CSS)

```css
.notification-list {
  position: fixed;
  top: 10px;
  right: 10px;
}

.notification {
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 5px;
  display: flex;
  justify-content: space-between;
}

.notification button {
  background: none;
  border: none;
  color: red;
  cursor: pointer;
}
```

## Conclusão

O Princípio da Inversão de Dependência (DIP) em React pode ser aplicado com:

> Context API: Para compartilhar dependências de forma centralizada.\
> Hooks Customizados: Para encapsular lógica e promover abstrações reutilizáveis.

Essa abordagem melhora a modularidade, testabilidade e escalabilidade do sistema, criando componentes mais robustos e alinhados aos princípios SOLID.

|   |
|---|--:|
| [SOLID - Interface Segregation Principle (ISP)]({{ '4-solid-no-react/4.4-isp' | relative_url}}) | [SOLID - Open/Closed Principle - (OCP)]({{ '5-projetos-avancados-tdd/5.1-hooks-customizados' | relative_url}}) |
