# Documento de Elicitação (Perguntas e Respostas)

## Registro Base da Elicitação de Requisitos

| Fase / Bloco | Pergunta Realizada | Resposta do Stakeholder |
| :--- | :--- | :--- |
| **Usuários** | Quais são os perfis de usuário? | Alunos e um Administrador no backend para a equipe técnica. |
| **Ações** | O que os usuários farão? | Aluno: responder anamnese para IA criar treino. Administrador: ter acesso a configurações de API, Backend e IA. |
| **Funcionalidades** | Descreva as funções essenciais. | Cadastro, Anamnese, Tela do Treino do dia, Feedbacks do treino, Geração do novo ciclo, escolha de tipo de treino (híbrido, corrida, musculação). |
| **Integrações** | Haverá sistemas externos? | A IA será uma API própria (IA local). Não há APIs externas vitais no MVP. |
| **Regras** | Quais as regras essenciais? | Ciclo dura 3 meses. Feedback extenso obrigatório no meio (1.5 mês) e no final. Menores de 18 e pessoas com doenças requerem autorização. |
| **Fluxo** | Qual o caminho principal? | Download -> Cadastro -> Escolhe modalidade -> Anamnese -> IA gera ciclo -> Treino diário marcado como concluído. |
| **Exceções** | E se der erro/demorar? | Se a IA demorar, o app libera o acesso às outras áreas e notifica quando estiver pronto. Feedbacks de meio/fim são obrigatórios, diários não. |
| **Relatórios** | Há dashboards/métricas? | Sim, progresso de desempenho, feedbacks, quilômetros e estimativa de calorias. |
| **Acesso** | Como será o Login? | Simples com e-mail/senha ou Login Social com Google. |
| **Notificações** | Como avisaremos o usuário? | Push notifications, e-mail e futuramente WhatsApp. |
| **Infra/Perf.** | Qual o limite técnico? | Mínimo de 50 usuários simultâneos no MVP. IA deve responder em no máximo 1 minuto. |
| **Segurança** | E a privacidade/LGPD? | Dados processados pela IA de forma anônima. Nome e rosto não saem do banco central para a API da IA. |
| **Disponibilidade**| O servidor pode cair? | 24/7 de operação, com servidor cloud de backup. |


