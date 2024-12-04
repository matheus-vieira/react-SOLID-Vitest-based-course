---
layout: default
title: "Introducao Vitest"
---

**Vitest** é uma biblioteca moderna para testes em JavaScript e TypeScript, com foco em simplicidade, velocidade e integração com o ecossistema de desenvolvimento atual.

Ele foi projetado para funcionar bem com ferramentas como Vite, tornando-o uma escolha ideal para projetos modernos de front-end.

## Configuração Inicial do Vitest

Configurar o Vitest em um projeto é direto e rápido, especialmente se você já usa o Vite.

### Passos para Configuração

#### Instalar as dependências necessárias

Certifique-se de que o Node.js e o npm estão instalados. Depois, instale o Vitest e seus pacotes auxiliares.

```bash
npm install --save-dev vitest @vitejs/plugin-react
```

#### Configurar o arquivo vite.config.js

Adicione o plugin React e configure o suporte ao Vitest.

```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
  },
});
```

#### Criar o script de testes

Adicione o script de testes no arquivo `package.json`.

```json
"scripts": {
  "test": "vitest"
}
```

#### 1.4. Criar um teste básico

Adicione um arquivo de teste na pasta tests. Exemplo: `tests/example.test.js`.

```javascript
import { describe, it, expect } from 'vitest';

describe('Teste Básico', () => {
  it('deve somar números corretamente', () => {
    const sum = (a, b) => a + b;
    expect(sum(2, 3)).toBe(5);
  });
});
```

#### Executar os testes

Execute os testes usando o comando:

```bash
npm run test
```

### Recursos do Vitest

> Globais: Métodos de teste como describe, it e expect são globais, dispensando imports manuais.\
> Ambiente Rápido: Integra-se perfeitamente ao Vite, aproveitando sua velocidade.

## Comparação com Jasmine e Jest

Embora Vitest, Jasmine, e Jest sejam bibliotecas para testes, há diferenças significativas que as tornam adequadas para diferentes cenários.

### Jasmine

#### Características do Jasmine

> **Nativo:** Não depende de outras bibliotecas para executar testes.\
> **Interface Simples:** Possui métodos como describe, it, e expect.\
> **Sem Mocking Avançado:** Não oferece ferramentas avançadas para mocks (bibliotecas externas são necessárias).

#### Limitações do Jasmine

> Configuração manual mais trabalhosa.\
> Não possui integração nativa com ferramentas modernas como Vite.

### Jest

#### Características do Jest

> **Ampla Adoção:** Ideal para testes em aplicações React.\
> **Mocking Poderoso:** Ferramentas nativas para mocks, spies e manipulação de timers.\
> **Configuração Completa:** Funciona em projetos novos ou legados.

#### Limitações do Jest

> Mais pesado e mais lento em comparação ao Vitest.
> Pode ser excessivo para projetos simples ou baseados em Vite.

### Vitest

#### Característicasdo Vitest

> **Integração com Vite:** Extremamente rápido para projetos modernos.\
> **Configuração Simplificada:** Suporte nativo ao TypeScript e React.\
> **Compatível com Jest:** APIs similares para facilitar a migração de Jest para Vitest.

#### Vantagens

> Velocidade superior graças à integração com Vite.\
> Arquitetura moderna e leve.\
> Funciona bem com testes unitários, de integração e E2E em projetos modernos.

### Tabela Comparativa

| Característica                 | Jasmine           | Jest   | Vitest |
| Integração com Vite            | ✖️                | ✖️    | ✔️     |
| Mocking Nativo                 | ✖️ (não nativo)   | ✔️    | ✔️     |
| Velocidade                     | Média             | Média  | Alta   |
| Configuração Simples           | ✖️                | ✔️    | ✔️     |
| Compatibilidade com TypeScript | ✖️                | ✔️    | ✔️     |

## Conclusão

> Vitest

É ideal para projetos modernos baseados em Vite, oferecendo uma configuração rápida e excelente desempenho.

> Jest

É a escolha para projetos maiores ou que necessitem de ferramentas avançadas de mocking.

> Jasmine

Ainda é relevante em sistemas legados ou para quem busca simplicidade em testes unitários.

### Quando Usar o Vitest?

Projetos React com Vite.

Necessidade de testes rápidos e leves.

Reutilização de familiaridade com APIs semelhantes às do Jest.

Pratique configurando o Vitest em um projeto e compare o desempenho com outras bibliotecas de teste para entender como ele pode beneficiar o seu fluxo de trabalho.

| |
|---|--:|
| [Componentes Desacoplados]({{ '3-componentes-testaveis/3.1-componentes-desacoplados' | relative_url}}) | [Primeiros Testes]({{ '3-componentes-testaveis/3.3-primeiros-testes' | relative_url}}) |
