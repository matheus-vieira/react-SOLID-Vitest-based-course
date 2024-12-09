---
layout: default
title: "SOLID - Princípio da Substituição de Liskov (Liskov Substitution Principle - LSP)"
---

> S - Single Responsibility Principle\
> O - Open/Closed Principle\
> ***L - Liskov Substitution Principle***\
> I - Interface Segregation Principle\
> D - Dependency Inversion Principle

O **Princípio da Substituição de Liskov (Liskov Substitution Principle - LSP)**, parte dos princípios SOLID, afirma que **uma classe derivada deve ser substituível por sua classe base sem alterar o comportamento esperado do sistema**.

No contexto do React, o LSP é aplicado para garantir que componentes ou funções reutilizáveis possam ser trocados ou estendidos sem impactar negativamente o restante do sistema.

## Entendendo o LSP

### Definição Formal

Se `S` é uma subclasse de `T`, então os objetos do tipo `T` devem poder ser substituídos por objetos do tipo `S` sem alterar o comportamento do programa.

### Exemplo Intuitivo

Se você tem um componente genérico que exibe um botão, ele deve poder ser substituído por uma variante de botão sem causar erros ou mudanças inesperadas no funcionamento.

## Aplicando o LSP em React

Para aplicar o LSP em React:

> **Abstração bem definida:** Garanta que as interfaces de entrada (props) de componentes sejam consistentes.\
> **Evite restrições desnecessárias:** Não limite a reutilização de componentes por meio de validações ou comportamentos não flexíveis.\
> **Comportamento previsível:** Os componentes derivados devem manter o contrato funcional do componente base.

## Exemplo de Violação do LSP

### Componente Base

```jsx
function Button({ label, onClick }) {
  return <button onClick={onClick}>{label}</button>;
}
```

Componente Derivado que Viola o LSP:

```jsx
function DisabledButton({ label, onClick }) {
  return <button disabled>{label}</button>; // Ignora o onClick
}
```

Problema

A substituição de Button por DisabledButton pode quebrar funcionalidades, pois o contrato de permitir cliques (onClick) é violado.

#### Exemplo Correto: Componentes Intercambiáveis

Refatorando com o LSP:

Componente Base:

```jsx
function Button({ label, onClick, disabled = false }) {
  return (
    <button onClick={!disabled ? onClick : undefined} disabled={disabled}>
      {label}
    </button>
  );
}
```

Componente Derivado:

```jsx

function DisabledButton(props) {
  return <Button {...props} disabled />;
}
```

Uso Intercambiável:

```jsx
function App() {
  return (
    <div>
      <Button label="Clique Aqui" onClick={() => alert('Botão clicado!')} />
      <DisabledButton label="Desativado" onClick={() => alert('Não clicável')} />
    </div>
  );
}
```

Por que Respeita o LSP?

> Comportamento Consistente: O botão desativado ainda respeita o contrato de aceitar onClick e label.\
> Intercambiabilidade: Você pode trocar Button por DisabledButton sem alterar a funcionalidade principal.

### Garantindo Intercambiabilidade com Validação e Abstração

Uso de PropTypes:

Valide as propriedades dos componentes para garantir que as entradas esperadas sejam consistentes.

```jsx
import PropTypes from 'prop-types';

function Button({ label, onClick, disabled }) {
  return (
    <button onClick={!disabled ? onClick : undefined} disabled={disabled}>
      {label}
    </button>
  );
}

Button.propTypes = {
  label: PropTypes.string.isRequired,
  onClick: PropTypes.func,
  disabled: PropTypes.bool,
};
```

Abstração com Interfaces Simples:

Defina uma API de props consistente para componentes relacionados.

Exemplo: Interface para Entrada de Dados:

```jsx

function TextInput({ value, onChange, placeholder }) {
  return <input value={value} onChange={onChange} placeholder={placeholder} />;
}

function PasswordInput(props) {
  return <TextInput {...props} type="password" />;
}
```

Uso Intercambiável:

```jsx

function App() {
  return (
    <div>
      <TextInput
        value=""
        onChange={(e) => console.log(e.target.value)}
        placeholder="Digite algo"
      />
      <PasswordInput
        value=""
        onChange={(e) => console.log(e.target.value)}
        placeholder="Senha"
      />
    </div>
  );
}
```

## Atividade Prática: Criando Componentes Intercambiáveis

Crie um sistema de alertas com diferentes variantes (SuccessAlert, ErrorAlert) respeitando o LSP.

Passo 1: Componente Base

```jsx

function Alert({ message, type = 'info' }) {
  const getClassName = () => {
    switch (type) {
      case 'success':
        return 'alert-success';
      case 'error':
        return 'alert-error';
      default:
        return 'alert-info';
    }
  };

  return <div className={getClassName()}>{message}</div>;
}
```

Passo 2: Componentes Derivados

```jsx
function SuccessAlert(props) {
  return <Alert {...props} type="success" />;
}

function ErrorAlert(props) {
  return <Alert {...props} type="error" />;
}
```

Passo 3: Uso no App

```jsx

function App() {
  return (
    <div>
      <SuccessAlert message="Operação bem-sucedida!" />
      <ErrorAlert message="Ocorreu um erro!" />
    </div>
  );
}
```

## Conclusão

Aplicar o LSP em React significa:

Garantir que os componentes derivados respeitem as expectativas de comportamento do componente base.

Manter interfaces consistentes para permitir substituições sem impactar o sistema.

Criar componentes testáveis e extensíveis que promovem reutilização e modularidade.

O uso do LSP resulta em um código mais robusto, previsível e fácil de escalar.

|   |
|---|--:|
| [SOLID - Open/Closed Principle - (OCP)]({{ '4-solid-no-react/4.2-ocp' | relative_url}}) | [SOLID - Interface Segregation Principle (ISP)]({{ '4-solid-no-react/4.4-isp' | relative_url}}) |
