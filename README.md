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

- [Por que React?]({{ '1-introducao-react/1.1-por-que-react' | relative_url}})
- [Ambiente de Desenvolvimento]({{ '1-introducao-react/1.2-ambiente-desenvolvimento' | relative_url}})
- [Primeiro Componente]({{ '1-introducao-react/3-primeiro-componente' | relative_url}})

#### Módulo 2: Conceitos Fundamentais do React

- [Hooks Essenciais]({{ '2-conceitos-fundamentais/2.1-hooks-essenciais' | relative_url}})
- [Renderização Condicional e Listas]({{ '2-conceitos-fundamentais/2.2-renderizacao-condicional-listas' | relative_url}})
- [Organização e Reutilização]({{ '2-conceitos-fundamentais/2.3-organizacao-reutilizacao' | relative_url}})

#### Módulo 3: Componentes Testáveis

- [Componentes Desacoplados]({{ '3-componentes-testaveis/3.1-componentes-desacoplados' | relative_url}})
- [Introdução ao Vitest]({{ '3-componentes-testaveis/3.2-introdução-vitest' | relative_url}})
- [Primeiros Testes]({{ '3-componentes-testaveis/3.2-introdução-vitest' | relative_url}})

#### Módulo 4: Aplicando SOLID no React

- [Single Responsibility Principle (SRP)]({{ '4-solid-no-react/4.1-srp' | relative_url}})
- [Open/Closed Principle (OCP)]({{ '4-solid-no-react/4.2-ocp' | relative_url}})
- [Liskov Substitution Principle (LSP)]({{ '4-solid-no-react/4.3-lsp' | relative_url}})
- [Interface Segregation Principle (ISP)]({{ '4-solid-no-react/4.4-isp' | relative_url}})
- [Dependency Inversion Principle (DIP)]({{ '4-solid-no-react/4.5-dip' | relative_url}})

#### Módulo 5: Projetos Avançados e TDD

- [Hooks Customizados]({{ '5-projetos-avancados-tdd/5.1-hooks-customizados.md' | relative_url}})
- [Gerenciamento de Estado]({{ '5-projetos-avancados-tdd/5.2-gerenciamento-estado' | relative_url}})
- [TDD com Vitest]({{ '5-projetos-avancados-tdd/5.3-tdd-vitest' | relative_url}})
- [Deploy]({{ '5-projetos-avancados-tdd/5.4-deploy' | relative_url}})
- [Projeto Final]({{ '5-projetos-avancados-tdd/5.5-projeto-final' | relative_url}})

#### Perguntas Frequentes

- [Perguntas comuns em entrevistas]({{ 'perguntas-frequentes' | relative_url}})

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
