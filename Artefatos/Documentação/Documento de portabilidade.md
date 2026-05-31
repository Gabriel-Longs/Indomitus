# Documento de Portabilidade

## 1. Objetivo
Este documento define as estratégias técnicas adotadas para garantir que o ecossistema do **Indomitus** possa ser transferido, executado e implantado em diferentes plataformas, sistemas operacionais e infraestruturas (tanto locais quanto em nuvem) com o mínimo de atrito e refatoração de código.

## 2. Portabilidade do Aplicativo Mobile
A interface do aluno precisa atingir o maior número de usuários possível.

- **Framework Cross-Platform:** O aplicativo será desenvolvido utilizando **React Native**. Isso garante uma base de código único (TypeScript/React) que é compilada de forma nativa tanto para **Android** quanto para **iOS**.
- **Design Adaptativo:** As interfaces seguirão diretrizes de responsividade para se adequarem a diferentes resoluções de telas, desde pequenos smartphones até telas maiores.

## 3. Portabilidade do Backend Principal
O backend responsável pelas regras de negócio e integrações precisa ser agnóstico de servidor.

- **Conteinerização (Docker):** Todo o backend em Node.js será empacotado em contêineres Docker. Isso garante que "se funciona no computador dos desenvolvedores, funciona em qualquer servidor Linux, AWS, GCP, DigitalOcean ou Azure".
- **Externalização de Configurações:** O projeto seguirá as regras do *12-Factor App*. Todas as credenciais (URLs de banco, chaves secretas, IP do servidor da IA) estarão em variáveis de ambiente (`.env`). Nenhum dado de conexão estará "chumbado" no código (*hardcoded*).
- **Abstração de Banco de Dados:** O acesso ao PostgreSQL será feito através de um ORM. Se no futuro houver necessidade de migrar a base, a sintaxe de consultas (queries) estará protegida pelo ORM.

## 4. Portabilidade do Servidor de IA Local (Atenção Crítica)
Como o projeto hospedará a própria IA, este é o módulo mais sensível a mudanças de infraestrutura, pois depende intimamente do Hardware.

- **Agnosticismo de Hardware (Software Limiters):** Utilização de motores de inferência versáteis que conseguem rodar os modelos (LLMs) tanto em GPUs da NVIDIA (CUDA) quanto da AMD (ROCm), além de possuírem "fallback" para CPU (embora muito mais lento), garantindo que o servidor não fique preso permanentemente a uma marca de placa de vídeo.
- **Dockerização com Suporte a GPU:** O ambiente do servidor de IA deve rodar em contêineres usando ferramentas como o `NVIDIA Container Toolkit`. Isso previne o "inferno de dependências" de drivers Python, PyTorch e bibliotecas C++ no sistema operacional local.
- **API Desacoplada:** A IA se comunicará com o Backend exclusivamente via requisições HTTP REST. Assim, se o servidor físico queimar e for preciso alugar uma GPU na nuvem emergencialmente, basta mudar a URL no arquivo `.env` do Backend, sem alterar uma linha de código do aplicativo.

## 5. Estratégia de Backup e Migração
- **Portabilidade de Dados:** Scripts automatizados farão *dumps* lógicos periódicos do PostgreSQL e os enviarão para um serviço de armazenamento seguro na nuvem, garantindo que toda a inteligência e o histórico do aplicativo possam ser restaurados em um novo servidor em questão de minutos em caso de desastre.


