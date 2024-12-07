---
layout: default
title: 'SOLID - Single Responsibility Principle (SRP)'
---
O **Princípio de Responsabilidade Única (Single Responsibility Principle - SRP)**, um dos pilares do SOLID, afirma que **cada classe ou componente deve ter apenas uma razão para mudar**.

Em outras palavras, um componente deve ter uma única responsabilidade ou função no sistema.

Em React, o SRP nos ajuda a criar componentes mais reutilizáveis, testáveis e fáceis de manter.

Aplicar esse princípio evita a criação de "componentes gigantes" que fazem várias coisas ao mesmo tempo.

> **Por que o SRP é Importante?**\
> **Facilidade de Manutenção:** Alterar uma funcionalidade afeta apenas o componente responsável.\
> **Reutilização:** Componentes com responsabilidades claras podem ser reutilizados em diferentes contextos.\
> **Legibilidade:** Código mais modular é mais fácil de entender e revisar.\
> **Testabilidade:** Testar componentes menores e específicos é mais simples.

## Exemplos de Componentes com SRP

### Exemplo 1: Um Componente que Viola o SRP

Imagine um componente que exibe uma lista de usuários e inclui lógica para buscar os dados da API e renderizá-los.

```jsx
import React, { useEffect, useState } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('/api/users')
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <div>
      <h1>Lista de Usuários</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default UserList;
```

> Problemas:\
> O componente é responsável por buscar os dados e renderizá-los.\
> Alterar a lógica de API ou a estrutura de renderização pode gerar conflitos desnecessários.

### Exemplo 2: Aplicando o SRP

Vamos dividir a lógica de busca e renderização em componentes separados.

#### Componente para Buscar Dados (Responsabilidade 1)

```javascript
import { useEffect, useState } from 'react';

export function useFetchUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);
    fetch('/api/users')
      .then((response) => response.json())
      .then((data) => setUsers(data))
      .then(() => setLoading(false));
  }, []);

  return [ users, loading ];
}
```

#### Componente para Renderização (Responsabilidade 2)

```jsx
function UserList({ users }) {
  return (
    <div>
      <h1>Lista de Usuários</h1>
      {users && users.length && (
        <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      )}
      </ul>
    </div>
  );
}

export default UserList;
```

#### Combinando os Componentes

```jsx
import React from 'react';
import { useFetchUsers } from './useFetchUsers';
import UserList from './UserList';

function App() {
  const { users, loading } = useFetchUsers();

  if (loading) return "loading users...";

  return <UserList users={users} />;
}

export default App;
```

> Benefícios da Refatoração:\
> Componente de Busca: Pode ser reutilizado em outras partes da aplicação.\
> Componente de Renderização: Focado exclusivamente em como exibir os dados.\
> Flexibilidade: Alterações na API ou no layout não afetam ambos os componentes.

## Refatoração de Código

Refatorar um componente para seguir o SRP envolve dividir responsabilidades distintas em componentes ou funções dedicadas.

### Exemplo Prático: Refatorando um Formulário

#### Código Original (Violando SRP)

```jsx
function ContactForm() {
  const [formData, setFormData] = useState({ name: '', email: '' });

  const handleSubmit = (e) => {
    e.preventDefault();
    fetch('/api/contact', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(formData),
    });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Nome"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
      />
      <input
        type="email"
        placeholder="Email"
        value={formData.email}
        onChange={(e) => setFormData({ ...formData, email: e.target.value })}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

> **Problemas**\
> Gerenciamento de Estado: Está diretamente acoplado ao componente.\
> Envio de Dados: Está misturado à lógica de renderização.

### Refatorando com SRP

#### Componente para Gerenciar o Estado

```javascript
import { useState } from 'react';

export function useContactForm() {
  const [formData, setFormData] = useState({ name: '', email: '' });

  const updateField = (field, value) => {
    setFormData({ ...formData, [field]: value });
  };

  return { formData, updateField };
}
```

#### Componente para Enviar Dados

```javascript
Copiar código
export async function submitContactForm(formData) {
  return fetch('/api/contact', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(formData),
  });
}
```

#### Componente de Apresentação

```jsx
import React from 'react';

function ContactForm({ formData, updateField, onSubmit }) {
  return (
    <form onSubmit={onSubmit}>
      <input
        type="text"
        placeholder="Nome"
        value={formData.name}
        onChange={(e) => updateField('name', e.target.value)}
      />
      <input
        type="email"
        placeholder="Email"
        value={formData.email}
        onChange={(e) => updateField('email', e.target.value)}
      />
      <button type="submit">Enviar</button>
    </form>
  );
}

export default ContactForm;
```

#### Integração no App

```jsx
import React from 'react';
import { useContactForm } from './useContactForm';
import { submitContactForm } from './submitContactForm';
import ContactForm from './ContactForm';

function App() {
  const { formData, updateField } = useContactForm();

  const handleSubmit = async (e) => {
    e.preventDefault();
    await submitContactForm(formData);
    alert('Formulário enviado com sucesso!');
  };

  return <ContactForm formData={formData} updateField={updateField} onSubmit={handleSubmit} />;
}

export default App;
```

## Conclusão

Aplicar o SRP em React ajuda a manter os componentes:

> Focados: Cada componente realiza apenas uma tarefa.\
> Reutilizáveis: Componentes ou funções podem ser usados em diferentes contextos.\
> Manuteníveis: Alterações em uma parte do sistema têm impacto limitado.\
> Refatorar para SRP exige prática, mas resulta em código mais limpo e eficiente, alinhado aos princípios do SOLID.

| |
|---|--:|
| [Primeiros Testes]({{ '3-componentes-testaveis/3.3-primeiros-testes' | relative_url}}) | [SOLID - Open/Closed Principle (OCP)]({{ '4-solid-no-react/4.2-ocp' | relative_url}})
