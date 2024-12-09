# Curso de React com SOLID e Testes com Vitest

Bem-vindo ao **Curso de React para Programadores Experientes**! Este curso foi projetado para desenvolvedores que já possuem experiência em outras tecnologias e desejam aprender React, aplicando princípios de SOLID e desenvolvendo componentes testáveis com Vitest.

## Objetivo Geral

Aprender e dominar os conceitos fundamentais de React, aplicando princípios de SOLID e práticas de desenvolvimento orientado a testes (TDD) utilizando Vitest.

### Executando com Jekyl

Este curso foi estruturado para ser compatível com o framework Jekyll, permitindo sua visualização como um site estático.

#### Pré-requisitos

1. Ruby: Certifique-se de que o Ruby está instalado em sua máquina. Você pode verificar instalando Ruby para seu sistema operacional.
2. Jekyll: Instale o Jekyll e o Bundler (gerenciador de dependências Ruby):

   ```bash
   gem install bundler jekyll
   ```

#### Passos para executar

1. Clone este repositório:

   ```bash
   git clone https://github.com/seu-usuario/react-solid-vitest-course.git
   cd react-solid-vitest-course
   ```

2. Instale as dependências do projeto:

   ```bash
   bundle install
   ```

3. Inicie o servidor de desenvolvimento:

   ```bash
   bundle exec jekyll serve
   ```

4. Abra o navegador e acesse: [http://localhost:4000](http://localhost:4000)

#### Personalização

Você pode editar os arquivos Markdown em qualquer editor de texto e recarregar o navegador para ver as alterações.
Configure o `_config.yml` para alterar detalhes como o título do site ou base URL.

### Estrutura do Curso

Cada módulo está organizado em pastas, com arquivos Markdown detalhando cada tópico e exercícios. Abaixo está a estrutura:

#### Módulo 1: Introdução ao React

- [Por que React?](1-introducao-react/1.1-por-que-react)
- [Ambiente de Desenvolvimento](1-introducao-react/1.2-ambiente-desenvolvimento)
- [Primeiro Componente](1-introducao-react/1.3-primeiro-componente)

#### Módulo 2: Conceitos Fundamentais do React

- [Hooks Essenciais](02_Conceitos_Fundamentais/01_hooks_essenciais.md)
- [Renderização Condicional e Listas](02_Conceitos_Fundamentais/02_renderizacao_condicional_listas.md)
- [Organização e Reutilização](02_Conceitos_Fundamentais/03_organizacao_reutilizacao.md)

#### Módulo 3: Componentes Testáveis

- [Componentes Desacoplados](03_Componentes_Testaveis/01_componentes_desacoplados.md)
- [Introdução ao Vitest](03_Componentes_Testaveis/02_introducao_vitest.md)
- [Primeiros Testes](03_Componentes_Testaveis/03_primeiros_testes.md)

#### Módulo 4: Aplicando SOLID no React

- [Single Responsibility Principle (SRP)](04_SOLID_no_React/01_srp.md)
- [Open/Closed Principle (OCP)](04_SOLID_no_React/02_ocp.md)
- [Liskov Substitution Principle (LSP)](04_SOLID_no_React/03_lsp.md)
- [Interface Segregation Principle (ISP)](04_SOLID_no_React/04_isp.md)
- [Dependency Inversion Principle (DIP)](04_SOLID_no_React/05_dip.md)

#### Módulo 5: Projetos Avançados e TDD

- [Hooks Customizados](05_Projetos_Avancados_TDD/01_hooks_customizados.md)
- [Gerenciamento de Estado](05_Projetos_Avancados_TDD/02_gerenciamento_estado.md)
- [TDD com Vitest](05_Projetos_Avancados_TDD/03_tdd_vitest.md)
- [Deploy](05_Projetos_Avancados_TDD/04_deploy.md)
- [Projeto Final](05_Projetos_Avancados_TDD/05_projeto_final.md)

#### Perguntas Frequentes

- [Perguntas comuns em entrevistas](perguntas-frequentes)

### Como Usar este Repositório

#### Configuração Inicial

1. Clone o repositório:

   ```bash
   git clone https://github.com/seu-usuario/react-solid-vitest-course.git
   cd react-solid-vitest-course
   ```

2. Instale as dependências do projeto React (quando aplicável):

   ```bash
   npm install
   ```

3. Para rodar um servidor de desenvolvimento (usando Vite):

   ```bash
   npm run dev
   ```

4. Para rodar os testes com Vitest:

   ```bash
   npm test
   ```

### Contribuição

Contribuições são bem-vindas! Siga estas etapas:

1. Faça um fork do repositório.
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`).
3. Commit suas alterações (`git commit -m 'Adicionei nova feature'`).
4. Envie para a branch principal (`git push origin feature/nova-feature`).
5. Abra um Pull Request.

### Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.
