---
layout: default
title: "Componentes Desacoplados"
---

Desacoplar componentes significa estruturar o código de forma que cada componente seja independente, reutilizável e fácil de manter.

Dois conceitos importantes nesse contexto são a **composição de componentes** e as **estratégias para evitar o prop drilling**.

## Composição de Componentes

A composição é uma abordagem fundamental em React para criar componentes maiores a partir de componentes menores e mais específicos.

Em vez de herança, React utiliza composição para compartilhar funcionalidades entre componentes.

### **Por que usar composição?**

> **Reutilização:** Componentes menores podem ser reutilizados em diferentes partes do aplicativo.\
> **Leitura:** Componentes com responsabilidades claras são mais fáceis de entender.\
> **Manutenção:** Alterações em componentes menores têm impacto limitado.

### **Exemplo de Composição**

#### **Componentes Básicos:**

```jsx
function Header() {
  return <header><h1>Meu Aplicativo</h1></header>;
}

function Footer() {
  return <footer>© 2024 Meu Aplicativo</footer>;
}
```

#### Componente Composto

```jsx
function Layout({ children }) {
  return (
    <div>
      <Header />
      <main>{children}</main>
      <Footer />
    </div>
  );
}
```

#### Uso do Componente Composto

```jsx
function App() {
  return (
    <Layout>
      <p>Bem-vindo ao meu aplicativo!</p>
    </Layout>
  );
}

export default App;
```

> **Benefícios:**\
> Componentes menores (`Header`, `Footer`) podem ser reutilizados.\
> `Layout` serve como uma estrutura padrão para diferentes páginas ou seções.

## Estratégias para Evitar `Prop Drilling`

`Prop drilling` ocorre quando props precisam ser passadas de um componente pai para múltiplos níveis de componentes filhos apenas para chegar ao componente onde serão usadas.

### Problemas do `Prop Drilling`

> Complexidade: Componentes intermediários passam a depender de props que não usam.\
> Manutenção: Alterar props requer modificações em toda a cadeia de componentes.\
> Soluções para Evitar Prop Drilling\

#### Context API

A Context API do React permite compartilhar dados entre componentes sem a necessidade de passá-los manualmente por cada nível.

##### Exemplo com Context API

Criando o Contexto:

```jsx
import React, { createContext, useContext, useState } from 'react';

const UserContext = createContext();

export function UserProvider({ children }) {
  const [user, setUser] = useState({ name: 'João', loggedIn: true });

  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}
```

##### Usando o Contexto

```jsx
function Navbar() {
  const { user } = useContext(UserContext);

  return <nav>Bem-vindo, {user.name}!</nav>;
}

function LogoutButton() {
  const { setUser } = useContext(UserContext);

  return <button onClick={() => setUser({ name: '', loggedIn: false })}>Logout</button>;
}
```

##### Combinando Context e Composição

```jsx
import React from 'react';
import { UserProvider } from './UserContext';

function App() {
  return (
    <UserProvider>
      <Navbar />
      <LogoutButton />
    </UserProvider>
  );
}

export default App;
```

## Hooks Personalizados

Criar hooks personalizados pode encapsular a lógica e facilitar o compartilhamento de dados entre componentes.

### Exemplo de Hook Personalizado

```jsx
function useUser() {
  const [user, setUser] = useState({ name: 'Maria', loggedIn: true });
  return { user, setUser };
}

function UserComponent() {
  const { user, setUser } = useUser();

  return (
    <div>
      <p>Usuário: {user.name}</p>
      <button onClick={() => setUser({ name: 'Pedro', loggedIn: true })}>Alterar Usuário</button>
    </div>
  );
}
```

## State Management com Bibliotecas

Para aplicativos maiores, bibliotecas como Redux, Zustand ou MobX podem ser usadas para gerenciar o estado global de forma eficiente.

## Conclusão

> Composição de Componentes: Ajuda a criar componentes reutilizáveis e desacoplados, favorecendo a modularidade.\
> Evitar Prop Drilling: Use a Context API, hooks personalizados ou bibliotecas de gerenciamento de estado para compartilhar dados de forma eficiente.

### Benefícios do Desacoplamento

> Escalabilidade: Componentes e estados são fáceis de estender.\
> Manutenção: Alterações são localizadas, reduzindo impactos no sistema como um todo.\
> Reutilização: Componentes bem projetados podem ser reutilizados em diferentes projetos.

Adote essas práticas para criar aplicações React bem organizadas e de fácil manutenção.

| |
|---|:--:||--:|
| [Organização e Reutilização]({{ '2-conceitos-fundamentais/2.3-organizacao-reutilizacao' | relative_url}}) | [Início]({{ '/' | relative_url}}) | [Introdução Vitest]({{ '3-componentes-testaveis/3.2-introdução-vitest' | relative_url}}) |
