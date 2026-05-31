# Matriz de Rastreabilidade

## 1. Requisitos vs Regras de Negócio

| ID Requisito | Descrição | ID Regra Negócio | Descrição da Regra |
| :--- | :--- | :--- | :--- |
| **RF-02** | Anamnese e modalidade | **RN-01** | Menores de 18 anos ou pessoas com comorbidades requerem autorização médica ou de responsável. |
| **RF-03** | Solicitar treino à IA | **RN-02** | A geração compreende um ciclo exato de 3 meses de prescrição. |
| **RF-06** | Feedbacks do ciclo | **RN-03** | Feedback aos 45 dias e 90 dias são obrigatórios para liberar o próximo ciclo. |
| **RNF-03** | Dados para a IA | **RN-04** | A LGPD exige desvinculação de dados sensíveis da identidade física do aluno na base da inteligência artificial. |

## 2. Requisitos vs Casos de Uso

| ID Requisito | Caso de Uso Associado | Ação do Sistema |
| :--- | :--- | :--- |
| **RF-01** | Cadastro e Autenticação | Cria novo registro de aluno no banco. |
| **RF-02** | Configuração Inicial | Exibe formulário e bloqueia avanço sem resposta. |
| **RF-03** | Geração de Treino | Dispara requisição HTTP interna para a API da IA local. |
| **RF-04** | Execução de Treino | Exibe interface de exercícios e atualiza a flag de 'done'. |
| **RF-06** | Checkpoint de Retenção | Verifica a data e exibe pop-up compulsório pedindo feedback extenso. |

> **`[A DEFINIR]`** — Necessidade de parecer legal (ou consulta informal) a respeito de diretrizes do CREF (Conselho Regional de Educação Física) e termos de isenção de responsabilidade médica para uso de treinos gerados via software no Brasil.


