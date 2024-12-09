---
layout: default
title: "SOLID - Princípio da Segregação de Interface (Interface Segregation Principle - ISP)"
---

> S - Single Responsibility Principle\
> O - Open/Closed Principle\
> L - Liskov Substitution Principle\
> ***I - Interface Segregation Principle***\
> D - Dependency Inversion Principle

O **Princípio da Segregação de Interface (ISP)**, parte dos princípios SOLID, afirma que **nenhum cliente deve ser forçado a depender de métodos ou propriedades que não utiliza**.

Em outras palavras, as interfaces devem ser pequenas, específicas e adaptadas ao cliente, ao invés de genéricas e infladas.

No contexto do React, o ISP pode ser aplicado às **props** dos componentes, garantindo que cada componente receba apenas os dados e funcionalidades necessários para seu funcionamento.

## Por que Segregar Interfaces?

Em React, as **props** desempenham o papel das interfaces.

Fornecer props irrelevantes ou excessivas a um componente:

> **Aumenta a complexidade:** O componente precisa lidar com dados desnecessários.\
> **Viola a coesão:** O componente pode acabar executando tarefas que não são de sua responsabilidade.\
> **Dificulta a manutenção:** Alterar ou adicionar funcionalidade em componentes com props genéricas pode causar efeitos colaterais inesperados.

## Estratégias para Interfaces (Props) Limpas

### Criação de Componentes Focados

Evite componentes que tentam fazer "tudo ao mesmo tempo".

Divida responsabilidades em componentes menores.

#### Exemplo de Componente Inflado (Violação do ISP)

```jsx
function UserProfile({ name, email, avatar, onEdit, onDelete, isAdmin }) {
  return (
    <div>
      <img src={avatar} alt={`${name}'s avatar`} />
      <h2>{name}</h2>
      <p>{email}</p>
      {isAdmin && (
        <div>
          <button onClick={onEdit}>Editar</button>
          <button onClick={onDelete}>Excluir</button>
        </div>
      )}
    </div>
  );
}
```

Problema:

> O componente `UserProfile` tem responsabilidades misturadas: exibir informações e gerenciar permissões administrativas.

### Refatoração com Componentes Focados

```jsx
function UserProfile({ name, email, avatar }) {
  return (
    <div>
      <img src={avatar} alt={`${name}'s avatar`} />
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
}

function AdminControls({ onEdit, onDelete }) {
  return (
    <div>
      <button onClick={onEdit}>Editar</button>
      <button onClick={onDelete}>Excluir</button>
    </div>
  );
}
```

Uso Modular:

```jsx
function App() {
  const user = { name: "João", email: "joao@example.com", avatar: "/avatar.jpg" };
  const isAdmin = true;

  return (
    <div>
      <UserProfile {...user} />
      {isAdmin && <AdminControls onEdit={() => {}} onDelete={() => {}} />}
    </div>
  );
}
```

## Uso de Interfaces Específicas para Dados

Crie interfaces dedicadas para diferentes tipos de dados e funcionalidades, organizando props de maneira clara.

Exemplo de Interface Genérica (Violação do ISP):

```jsx
function Product({ name, price, discount, onAddToCart, onApplyDiscount, isFeatured }) {
  // Lógica inflada
}
```

### Refatoração com Interfaces Específicas

Divida as props em objetos bem definidos:

```jsx
function Product({ details, actions }) {
  return (
    <div>
      <h2>{details.name}</h2>
      <p>Preço: {details.price}</p>
      {details.discount && <p>Desconto: {details.discount}</p>}
      <button onClick={actions.onAddToCart}>Adicionar ao Carrinho</button>
      {actions.onApplyDiscount && (
        <button onClick={actions.onApplyDiscount}>Aplicar Desconto</button>
      )}
    </div>
  );
}

// Uso do componente
<Product
  details={{ name: "Produto X", price: "R$100", discount: "10%" }}
  actions={{
    onAddToCart: () => console.log("Adicionado!"),
    onApplyDiscount: () => console.log("Desconto aplicado!"),
  }}
/>
```

## Uso de TypeScript para Contratos de Interface

O uso de TypeScript em React ajuda a definir contratos claros para props, aplicando diretamente o ISP.

Exemplo:

```jsx
type UserDetails = {
  name: string;
  email: string;
  avatar: string;
};

type AdminActions = {
  onEdit: () => void;
  onDelete: () => void;
};

function UserProfile({ details }: { details: UserDetails }) {
  return (
    <div>
      <img src={details.avatar} alt={`${details.name}'s avatar`} />
      <h2>{details.name}</h2>
      <p>{details.email}</p>
    </div>
  );
}

function AdminControls({ actions }: { actions: AdminActions }) {
  return (
    <div>
      <button onClick={actions.onEdit}>Editar</button>
      <button onClick={actions.onDelete}>Excluir</button>
    </div>
  );
}
```

## Composição sobre Herança

Sempre prefira a composição para compartilhar lógica entre componentes ao invés de sobrecarregar props em componentes base.

Exemplo:

Composição para adicionar funcionalidade de exibição de tooltip:

```jsx
function Tooltip({ message, children }) {
  return (
    <div>
      {children}
      <span className="tooltip">{message}</span>
    </div>
  );
}

function App() {
  return (
    <Tooltip message="Mais informações">
      <button>Hover aqui</button>
    </Tooltip>
  );
}
```

## 3. Exercício Prático

Crie um componente Card que exibe informações de usuários e permite personalizar suas ações com interfaces específicas.

### Passo 1: Defina o Componente Base

```jsx
function Card({ details, actions }) {
  return (
    <div className="card">
      <h2>{details.title}</h2>
      <p>{details.description}</p>
      {actions && (
        <div className="actions">
          {actions.map((action, index) => (
            <button key={index} onClick={action.onClick}>
              {action.label}
            </button>
          ))}
        </div>
      )}
    </div>
  );
}
```

Passo 2: Implemente um Card Dinâmico

```jsx
function App() {
  const cardDetails = {
    title: "Usuário Premium",
    description: "Acesso exclusivo a recursos avançados.",
  };

  const cardActions = [
    { label: "Atualizar", onClick: () => console.log("Atualizado!") },
    { label: "Cancelar", onClick: () => console.log("Cancelado!") },
  ];

  return <Card details={cardDetails} actions={cardActions} />;
}
```

## Conclusão

O Princípio da Segregação de Interface em React é essencial para:

> Reduzir a complexidade: Props pequenas e focadas tornam os componentes mais simples.\
> Melhorar a manutenção: Componentes com interfaces limpas são mais fáceis de alterar e escalar.\
> Garantir modularidade: Componentes podem ser usados em diferentes contextos sem dependências desnecessárias.

Aplicar o ISP resulta em um código mais coeso, reutilizável e alinhado às melhores práticas de desenvolvimento.

|   |
|---|:--:||--:|
| [SOLID - Liskov Substitution Principle - (LSP)]({{ '4-solid-no-react/4.3-lsp' | relative_url}}) | [Início]({{ '/' | relative_url}}) | [SOLID - Dependency Inversion Principle (DIP)]({{ '4-solid-no-react/4.5-dip' | relative_url}}) |
