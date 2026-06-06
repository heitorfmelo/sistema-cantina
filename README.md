# 🍽️ ERP Gestão de Refeitório Corporativo 

![Status](https://img.shields.io/badge/Status-Em_Produ%C3%A7%C3%A3o-success?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.11+-blue?style=for-the-badge&logo=python&logoColor=white)
![Architecture](https://img.shields.io/badge/Architecture-Layered%20%7C%20Repository_Pattern-003B57?style=for-the-badge)
![Frontend](https://img.shields.io/badge/Frontend-Vanilla_JS%20%7C%20CSS3-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

> **Aviso:** Este é um repositório vitrine. O código-fonte desta aplicação é mantido em ambiente privado por questões de propriedade intelectual e regras de negócio corporativas. Este documento descreve as decisões de engenharia, a arquitetura de software e os desafios técnicos resolvidos no desenvolvimento deste sistema.

---

## 🎯 O Desafio de Negócio

Empresas com refeitórios internos (cantinas) perdem muito dinheiro e tempo com controles manuais (vales de papel ou planilhas) para gerenciar o consumo de refeições dos funcionários. O problema de negócio era criar um sistema ágil que servisse como um PDV (Ponto de Venda) para o operador do refeitório, ao mesmo tempo que atuasse como um sistema de auditoria financeira, debitando corretamente o consumo de cada colaborador no seu respectivo Centro de Custo (Departamento).

O sistema precisava ser à prova de fraudes, ter fechamento de caixa diário e gerar relatórios precisos para o RH e o setor financeiro no fechamento da folha de pagamento.

---

## 🧠 Arquitetura e Padrões de Projeto (Design Patterns)

O grande diferencial deste projeto não é apenas o que ele faz, mas *como* foi construído. O sistema foge do padrão amador de acoplar rotas diretamente ao banco de dados, utilizando uma **Arquitetura em Camadas (Layered Architecture)**:

## ⚙️ Funcionalidades Detalhadas

O sistema foi desenhado para gerir o ciclo de vida completo de uma refeição, desde a autorização de consumo até a conciliação financeira:

### 1. Módulo de Controle de Acesso e Segurança (RBAC)
*   **Autenticação Centralizada:** Controle de login via matrícula e senha, com verificação de integridade no backend.
*   **Gestão de Perfis:** Implementação de níveis de acesso (Admin, Auditor, Gestor, Operador) garantindo que as permissões de exclusão de dados e extração de relatórios sensíveis sejam restritas aos cargos administrativos.

### 2. Gestão Dinâmica de Usuários e Departamentos
*   **Hierarquia Organizacional:** Cadastro e gestão de departamentos/centros de custo, permitindo a vinculação de colaboradores e a correta alocação de despesas.
*   **Status de Atividade:** Controle de status (`Ativo`/`Inativo`) para garantir que apenas colaboradores vinculados à folha vigente possam consumir refeições.
*   **Filtros Avançados:** Busca por matrícula, nome ou departamento com paginação integrada (`usuarios.items`), otimizando a performance do banco de dados ao lidar com grandes volumes de registros.

### 3. Ponto de Venda (PDV) e Terminal de Liberação
*   **Terminal de Caixa:** Interface dedicada para operação rápida no refeitório, validando a matrícula e senha do colaborador em tempo real para liberação da refeição (Café da Manhã ou Almoço).
*   **Input de Pesagem:** Módulo integrado ao terminal que permite a entrada de peso (kg), permitindo que o sistema calcule valores variáveis se necessário.

### 4. Agendamento e Liberação de Refeições
*   **Regras de Negócio de Consumo:** Interface para liberação recorrente ou pontual, onde gestores definem janelas de datas, dias da semana específicos (ex: apenas dias úteis) e tipos de refeição permitidas por colaborador.
*   **Seleção em Lote:** Funcionalidade de seleção massiva de colaboradores para liberação de refeições, agilizando o trabalho administrativo.

### 5. Dashboards e Inteligência de Dados
*   **Monitoramento em Tempo Real:** Dashboard central que exibe o consumo atualizado de refeições (Café vs. Almoço) e a despesa acumulada.
*   **Análise de Gastos e Previsão:** Utilização de `Chart.js` para visualização de tendências e projeção de gastos (*forecast*), permitindo que o RH preveja o impacto financeiro com base no histórico de consumo do departamento.
*   **Relatórios Executivos:** Exportação de relatórios completos em formato **CSV** para planilhas e **PDF** (via `xhtml2pdf`) com layout profissional para impressão e auditoria.

## 🛠️ Stack Tecnológica

* **Backend:** Python
* **Arquitetura:** REST API, Repository Pattern, Service Layer Pattern.
* **Frontend Web:** Renderização Server-Side integrada com Vanilla JavaScript (`dashboard.js`, `caixa.js`, `liberacoes-form.js`) para reatividade no Ponto de Venda sem necessidade de *reload* da página.
* **Design & UI:** CSS3 modularizado (`liberacoes.css`, `relatorios.css`, `style.css`), desenhado para terminais de operação rápida (foco em usabilidade e redução de cliques).

---
*Este documento reflete a arquitetura de uma aplicação B2B real. Para discussões técnicas sobre a implementação do Padrão Repositório em Python, modelagem relacional de transações financeiras ou desenvolvimento da API, eu estou à disposição.*
