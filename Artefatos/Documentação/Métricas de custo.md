# Métricas de Custo e Dimensionamento de Banco de Dados

## 1. Objetivo
Com base no **Diagrama de Classes** (Modelagem Relacional), este documento projeta o volume de dados gerado por cada usuário e estima os custos de armazenamento no PostgreSQL (hospedagem de banco de dados) para o primeiro ano de MVP.

---

## 2. Estimativa de Tamanho por Entidade (Por Usuário)
Ao analisar as classes estruturadas, podemos calcular o "peso" médio de um usuário ativo ao longo de **1 ano completo** (assumindo 4 ciclos completos de 3 meses, treinando 5 vezes por semana):

| Entidade | Cálculo de Volume (Médio) | Peso Estimado Anual |
| :--- | :--- | :--- |
| **User** | 1 registro de perfil (strings curtas, UUID, Hash). | **~150 Bytes** |
| **Anamnese** | 1 a 2 formulários com JSONB de saúde por ano. | **~2 KB** |
| **CicloTreino** | 4 registros (1 por trimestre) com datas e status. | **~400 Bytes** |
| **TreinoDiario** | ~60 treinos por ciclo × 4 ciclos = **240 treinos**. Cada treino carrega o payload JSONB dos exercícios. (~1,5 KB por treino). | **~360 KB** |
| **Feedback** | Feedback diário (opcional) + Obrigatórios. ~200 avaliações por ano com textos curtos (comentários). | **~100 KB** |

**Peso Total Médio por Usuário Ativo (Ano): ~462 KB (Arredondando para 0.5 MB)**

---

## 3. Projeção de Escala e Volume do PostgreSQL
Com base no cálculo acima de **0,5 MB por usuário/ano**, projetamos os seguintes cenários de escala:

| Cenário de Adoção | Volume Total de Dados (1 Ano) | Requisito de Banco de Dados |
| :--- | :--- | :--- |
| **Pessimista** (500 usuários) | **250 MB** | Menos que um pendrive antigo. Cabe em qualquer plano Gratuito (Free Tier). |
| **Realista** (5.000 usuários) | **2,5 GB** | Banco de dados minúsculo. Roda sem esforço na instância de nuvem mais barata do mercado. |
| **Otimista** (20.000 usuários) | **10 GB** | Ainda considerado um banco de dados "pequeno". Requer alocação padrão de armazenamento. |

> **Nota:** Como o aplicativo não lida com envio de imagens, vídeos ou áudios pesados (BLOBs), lidamos apenas com Texto e JSON, que são dados incrivelmente eficientes e altamente compressíveis.

---

## 4. Análise de Custos Mensais (Banco de Dados)
Como o orçamento da dupla tem um teto de **R$ 3.000,00 mensais/anuais** para infraestrutura global (majoritariamente sugado pela IA Local), o banco de dados deve ser o menor dos custos.

| Provedor / Solução | Limite de Dados | Custo Estimado / Mês | Observação |
| :--- | :--- | :--- | :--- |
| **Supabase / Neon (Serverless)** | 500 MB (Grátis) | **R$ 0,00** | Ideal para o começo do MVP (Até ~1.000 usuários) sem pagar nada. |
| **VPS (DigitalOcean/Linode)** | 25 GB a 50 GB | **~ R$ 30,00 ($5-$6)** | Auto-hospedado via Docker. Excelente custo-benefício se os fundadores configurarem. |
| **AWS RDS (Managed Postgres)** | 20 GB (T3 Micro) | **~ R$ 90,00 ($15-$18)** | Banco gerenciado pela AWS. Maior segurança e backup automático, porém mais caro. |

---

## 5. Conclusão e Recomendação
A análise do diagrama de classes revela que **o custo de armazenamento de dados textuais e operacionais do aplicativo é irrisório.** 

**Recomendação Estratégica:** 
Não se preocupem financeiramente com o banco de dados PostgreSQL. Para o lançamento do MVP, vocês podem iniciar no plano gratuito do **Supabase/Neon** ou rodar um contêiner no mesmo servidor simples do backend por R$ 30/mês. 

Pelo menos **95% do teto financeiro do projeto** deve ser destinado exclusivamente para o Hardware do Servidor de IA Local (aluguel de GPU ou compra de servidor físico), já que o processamento do LLM para a inferência de treino é a única carga pesada real do sistema.
