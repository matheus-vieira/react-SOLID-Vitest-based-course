---
layout: default
title: Perguntas Frequentes sobre React
---

## O que é React e por que ele é usado?

**React** é uma biblioteca de JavaScript de código aberto, desenvolvida pelo Facebook, usada para criar interfaces de usuário (UI) interativas e dinâmicas.

---

## Por que ele é usado?

1. **Componentização:** Permite dividir a UI em componentes reutilizáveis e independentes.
2. **Virtual DOM:** Oferece atualizações eficientes no DOM real, melhorando o desempenho.
3. **Ecossistema robusto:** Com uma ampla comunidade e ferramentas, React se adapta a vários cenários, desde aplicações simples até sistemas complexos.
4. **Unidirecionalidade:** O fluxo de dados unidirecional facilita a depuração e a compreensão do código.

---

## Diferenças entre React e outras bibliotecas de front-end

1. React vs AngularJS:
   - React é uma **biblioteca** focada em UI, enquanto AngularJS é um **framework** completo com funcionalidades embutidas, como injeção de dependência.
   - React utiliza **JSX**, enquanto AngularJS usa templates HTML com diretivas.

2. React vs Vue.js:
   - React tem uma curva de aprendizado um pouco mais íngreme devido ao JSX.
   - Vue.js é mais opinativo, com integração nativa para várias funcionalidades, enquanto React exige mais configurações.

3. React vs jQuery:
   - jQuery manipula diretamente o DOM, enquanto React utiliza o **Virtual DOM** para maior eficiência.
   - React segue o paradigma declarativo, enquanto jQuery é imperativo.

---

## Como você escolhe entre componentes React e elementos HTML?

- **Elementos HTML:** Usados para criar estrutura básica de um componente, como `<div>`, `<button>` ou `<input>`.
- **Componentes React:** Usados quando uma lógica, comportamento ou estilização específica é necessária. Componentes permitem encapsular lógica de estado, eventos e estilização.

**Regra geral:** Use elementos HTML para partes estáticas da UI e componentes React para partes dinâmicas ou reutilizáveis.

---

## Como você gerencia o estado em React?

1. **Estado Local:** Gerenciado dentro de um único componente usando o hook `useState`.

   ```javascript
   const [count, setCount] = useState(0);
   ```

2. **Estado Global:** Gerenciado com ferramentas como:
    - Context API: Para compartilhar estado entre componentes.
    - Redux: Para aplicações maiores com requisitos complexos de estado.

3. **Bibliotecas de Gerenciamento de Estado:** `Recoil`, `MobX`, ou `Zustand` para cenários específicos.

---

## O que é o lifecycle e como você o utiliza?

O lifecycle refere-se ao ciclo de vida de um componente React, desde sua criação até sua desmontagem.

### Fases do Lifecycle

1. **Montagem (Mounting):** Quando o componente é criado e inserido no DOM.
    - `useEffect` com dependência vazia: Para lógica executada apenas na montagem.
2. **Atualização (Updating):** Quando o componente é atualizado devido a alterações de estado ou props.
    - `useEffect` com dependências específicas: Para executar lógica com base em mudanças.
3. **Desmontagem (Unmounting):** Quando o componente é removido do DOM.
    - Retorno do useEffect`: Para limpar recursos, como timers.

---

## Como você lida com erros em React?

1. Error Boundaries: Componentes que capturam erros JavaScript em sua árvore de componentes.

    ```jsx
    class ErrorBoundary extends React.Component {
        constructor(props) {
            super(props);
            this.state = { hasError: false };
        }

        static getDerivedStateFromError() {
            return { hasError: true };
        }

        componentDidCatch(error, errorInfo) {
            console.error("Error:", error, errorInfo);
        }

        render() {
            if (this.state.hasError) {
            return <h1>Algo deu errado.</h1>;
            }
            return this.props.children;
        }
    }
    ```

2. Hook de Tratamento de Erros: Use hooks para capturar e tratar erros em componentes funcionais.

---

## Como você testa e depura seu código React?

### Testes

1. Unitários: Teste de componentes isolados usando ferramentas como Jest ou Vitest.
2. Integração: Teste de componentes em conjunto usando @testing-library/react.
3. E2E: Testes completos da aplicação com Cypress ou Playwright.

### Depuração

1. React DevTools: Para inspecionar a árvore de componentes e seu estado/props.
2. Ferramentas do navegador: Como console e debugger.

---

## Como você otimiza o desempenho do React?

1. Memoização: Use React.memo para evitar renderizações desnecessárias.
2. Hooks de Otimização:
    - `useMemo`: Para memorizar valores calculados.
    - `useCallback`: Para memorizar funções.
3. Code Splitting: Divida o código em partes carregadas sob demanda com React.lazy.
4. Evite Prop Drilling: Use Context API ou gerenciadores globais para evitar passar props profundamente.
5. Virtualização: Use bibliotecas como react-window para renderizar apenas os elementos visíveis.

---

## Como você trabalha com estados globais?

1. Context API:
    - Ideal para aplicações pequenas ou médias.
    - Crie um provedor de contexto para compartilhar estado.
2. Redux:
    - Melhor para estados complexos com muitas interações.
    - Usa uma abordagem centralizada e imutável.
3. Outras opções: `Recoil`, `Zustand`, ou `MobX` podem ser escolhidas com base na complexidade e preferências.

---

## Como você lida com dependências entre componentes?

1. Composição: Estruture componentes como blocos reutilizáveis que recebem dependências via props.
2. Context API: Compartilhe dependências entre componentes sem passar props intermediárias.
3. Custom Hooks: Encapsule lógica compartilhada em hooks reutilizáveis.
4. Design com Responsabilidade Única: Garanta que cada componente tenha uma única responsabilidade, minimizando dependências desnecessárias.

|   |
|---|:--:||--:|
| &nbsp; | [Início]({{ '/' | relative_url}}) | &nbsp; |
