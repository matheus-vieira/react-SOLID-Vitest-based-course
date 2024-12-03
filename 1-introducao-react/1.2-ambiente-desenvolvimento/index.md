---
layout: default
title: "1.2 Ambiente de Desenvolvimento"
---

Para desenvolver em React com ferramentas modernas, é importante configurar corretamente o ambiente.

Isso envolve a instalação de ferramentas essenciais, configuração de projetos e integração de bibliotecas para testes.

Vamos detalhar cada passo.

## Instalação do Node.js e npm

O Node.js é um runtime JavaScript que permite executar JavaScript fora do navegador.

Ele vem com o npm (Node Package Manager), usado para gerenciar pacotes e dependências.

### Passos para Instalação

#### Baixe o instalador do Node.js

Acesse [Node.js](https://nodejs.org/pt) e escolha a versão LTS (Long Term Support), recomendada para estabilidade em projetos de produção.

#### Instale o Node.js

Siga as instruções do instalador para o seu sistema operacional.

#### Verifique a instalação

Execute os seguintes comandos no terminal para verificar a instalação:

```bash
node -v
npm -v
```

Isso retornará as versões do Node.js e npm instalados.

> Opcional: Use um Gerenciador de Versão de Node.js (nvm):

Para gerenciar múltiplas versões do Node.js em seu sistema, instale o [nvm](https://github.com/nvm-sh/nvm).

## Configuração do Projeto com Vite para React

Vite é uma ferramenta moderna para criar e configurar projetos frontend.

É rápida, simples e altamente otimizada para desenvolvimento com React.

### Criando o Projeto

#### Inicialize um novo projeto React com Vite:

```bash
npm create vite@latest my-react-app -- --template react
```

> Substitua `my-react-app` pelo nome do seu projeto.

O template react já configura um ambiente básico para React.

#### Navegue até o diretório do projeto

```bash
cd my-react-app
```

#### Instale as dependências:

```bash
npm install
```

#### Inicie o servidor de desenvolvimento

```bash
npm run dev
```

O terminal exibirá um link como [`http://localhost:5173`](http://localhost:5173).

Acesse no navegador para visualizar o projeto.
