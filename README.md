# Build Pipeline Refactoring Kata

Este repositório contém a minha solução para o [BuildPipeline-Refactoring-Kata](https://github.com/emilybache/BuildPipeline-Refactoring-Kata). O objetivo deste Kata é praticar técnicas de refatoração em um código legado que sofre de forte acoplamento e más práticas de Orientação a Objetos.

---

## Problema Principal

A classe `Pipeline` original atuava como um orquestrador de build e deploy, mas apresentava diversos "Code Smells":
* **(Aninhamento profundo):** Múltiplos blocos de `if/else` aninhados faziam com que o fluxo de execução fosse difícil de ler.
* **Alto Acoplamento:** A classe dependia fortemente de implementações concretas, como a classe `Emailer`, dificultando a extensão para novos meios de notificação.

---

## Melhorias Realizadas

### 1. Guard Clauses (Retornos Antecipados)
* **Ação:** A lógica de condicionais foi invertida para tratar os cenários de falha primeiro, retornando imediatamente.
* **Justificativa:** Eliminou a necessidade de blocos `else`. O código agora possui uma leitura linear, facilitando o entendimento do fluxo.

### 2. Remoção de Variáveis Temporárias
* **Ação:** Variáveis booleanas - `testsPassed` e `deploySuccessful` - que guardavam estado dentro dos métodos de validação foram removidas. Os métodos agora retornam `true` ou `false` diretamente.
* **Justificativa:** Torna as funções mais diretas e com responsabilidade única.

### 3. Princípio da Inversão de Dependência (SOLID - DIP)
* **Ação:** Criação da interface `NotificationService` para substituir o acoplamento com a classe concreta `Emailer`. 
* **Justificativa:** O `Pipeline` agora depende de uma abstração, não de uma implementação. Isso respeita o **Open/Closed Principle** (podemos adicionar notificações via Slack ou SMS no futuro sem alterar o `Pipeline`) e permite a injeção de *Mocks* para a criação de testes de unidade isolados.

---

## Tecnologias Utilizadas
* Java
* Princípios SOLID
* Refatoração (Clean Code)
