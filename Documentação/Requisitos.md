# Documentação de Requisitos

## Requisitos Funcionais (RF)

| ID | Descrição | Prioridade | Critério de Aceite |
| :--- | :--- | :--- | :--- |
| **RF-01** | O sistema deve permitir login via e-mail/senha e Google. | Alta | Cadastro concluído com sucesso e sessão iniciada. |
| **RF-02** | O sistema deve apresentar anamnese inicial e seleção de tipo de treino (corrida, musculação, híbrido). | Alta | Formulário preenchido salva no banco os parâmetros do aluno. |
| **RF-03** | O sistema deve solicitar a geração de treino à API de IA local. | Alta | Comunicação entre backend e API de IA funcionando e retornando payload do treino. |
| **RF-04** | O sistema deve exibir o treino do dia para o aluno e permitir marcar como concluído. | Alta | Ação de check atualiza o progresso do aluno no banco de dados. |
| **RF-05** | O sistema deve coletar feedbacks diários (opcionais). | Média | Interface permite nota rápida após o treino. |
| **RF-06** | O sistema deve bloquear a criação de novo ciclo até que os feedbacks obrigatórios sejam respondidos. | Alta | Sem o feedback de 1.5 mês ou de 3 meses, o novo ciclo não inicia. |
| **RF-07** | O sistema deve apresentar dashboards de calorias, quilômetros, desempenho e evolução. | Média | Gráficos e números populados com base no histórico do aluno. |
| **RF-08** | O sistema deve enviar notificações Push e E-mail. | Alta | Disparo de aviso de treino pronto ou lembretes via serviço integrado. |
| **RF-09** | O sistema web (Backoffice) deve gerenciar acesso à API e dados dos servidores. | Alta | Admin visualiza métricas de carga de sistema. |

## Requisitos Não Funcionais (RNF)

| ID | Descrição | Prioridade | Critério de Aceite |
| :--- | :--- | :--- | :--- |
| **RNF-01** | O aplicativo e backend devem suportar ao menos 50 usuários conectados operando simultaneamente. | Alta | Testes de carga atestam estabilidade. |
| **RNF-02** | A API de IA local deve gerar o treino completo em, no máximo, 1 minuto (60 segundos). | Alta | Logs provam tempo médio < 60s. |
| **RNF-03** | O sistema deve garantir anonimização total dos dados de saúde antes de enviá-los à IA (compliance com LGPD). | Alta | Logs provam que nenhum dado PII trafega para a API de IA. |
| **RNF-04** | O sistema operará 24/7 com fallback (backup) em ambiente de Nuvem. | Alta | Teste de disaster recovery (desligar local e assumir cloud) concluído com sucesso. |
| **RNF-05** | O sistema será desenvolvido em idioma Português (PT-BR). | Alta | Textos nativos em PT-BR. |


