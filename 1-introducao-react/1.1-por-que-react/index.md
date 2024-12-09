---
layout: default
title: "Por que React?"
---

React é uma biblioteca JavaScript popular, desenvolvida pelo Facebook, para construir interfaces de usuário (UI).

Suas vantagens são:

## Foco em Componentes Reutilizáveis

React introduz o conceito de componentes, pequenos blocos modulares que encapsulam comportamento, estilo e estrutura.

Isso facilita a manutenção e a escalabilidade do código.

### Virtual DOM

React usa o Virtual DOM para atualizar eficientemente apenas os componentes que mudam, em vez de renderizar toda a página.

> Isso melhora o desempenho.

### Ecosistema e Comunidade

A ampla comunidade e os inúmeros recursos, bibliotecas e ferramentas tornam o React uma escolha robusta e flexível.

### Adaptação Incremental

React pode ser adicionado a projetos existentes sem necessidade de reescrever todo o código, tornando-o ideal para migrações ou incrementos.

### Poderoso para Aplicações Modernas

Suporte para Single Page Applications (SPAs) e integração com ferramentas como Redux, Next.js e Apollo tornam o React ideal para construir aplicações modernas e complexas.

## Filosofia de React

### Unidirecionalidade

#### Fluxo de Dados Unidirecional

React utiliza um modelo de fluxo de dados unidirecional, o que significa que os dados fluem de componentes pais para componentes filhos via props.

Isso reduz a complexidade e facilita o rastreamento de bugs.

* Um estado gerenciado em um componente pai pode ser propagado para seus filhos, mantendo consistência.
  > Ferramentas como o Redux implementam essa filosofia, garantindo que todas as mudanças de estado sejam previsíveis e controladas.
* Benefício: Simplifica o gerenciamento do estado da aplicação, tornando o comportamento mais previsível e fácil de depurar.

### Imutabilidade

#### Estado Imutável

Em React, as mudanças no estado ou nos dados são feitas criando novas cópias desses dados em vez de modificar os originais. Isso facilita a detecção de mudanças e a renderização otimizada.

* Ao comparar objetos antigos e novos (shallow comparison), o React identifica facilmente o que precisa ser re-renderizado.
  > Por exemplo, funções como setState e hooks como useState seguem essa abordagem.
* Benefício: Promove código mais seguro e menos propenso a erros, além de facilitar o uso do Virtual DOM.

## Diferenças principais entre AngularJS e React

### AngularJS

Uma solução completa, ideal para aplicações grandes que exigem muitas funcionalidades embutidas.

### React

Mais flexível e modular, permitindo escolhas baseadas na necessidade da aplicação.

Ele é amplamente adotado para SPAs e UIs dinâmicas.

| Característica        | AngularJS                                | React                                                       |
| Tipo                  | Framework completo.                      | Biblioteca focada em UI.                                    |
| Arquitetura           | MVC (Model-View-Controller).             | Baseada em componentes reutilizáveis.                       |
| Linguagem             | Usa HTML com extensões (Directives).     | JSX, que mistura HTML e JavaScript.                         |
| Fluxo de Dados        | Bidirecional (Two-way Data Binding).     | Unidirecional (One-way Data Flow).                          |
| Estado                | Gerenciado internamente (com scope).     | Gerenciado com hooks ou bibliotecas (Redux).                |
| DOM                   | DOM real, o que pode ser mais lento.     | Virtual DOM para melhor performance.                        |
| Curva de Aprendizado  | Mais complexa devido à sua abrangência.  | Mais simples, focada em componentes.                        |
| Comunidade e Suporte  | Amplamente usado, mas menos que React.   | Muito popular, com maior comunidade ativa.                  |
| Dependências          | Inclui tudo o que precisa (completo).    | Necessita de bibliotecas externas para tarefas específicas. |
| Componentização       | Suporte inicial limitado.                | Componentes altamente reutilizáveis.                        |

| |
|---|:--:||--:|
| &nbsp; | [Início]({{ '/' | relative_url}}) | [Ambiente de Desenvolvimento]({{ '1-introducao-react/1.2-ambiente-desenvolvimento' | relative_url}}) |
