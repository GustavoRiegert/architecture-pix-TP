# Análise da Arquitetura AWS Lambda

## Introdução

AWS Lambda, desenvolvido pela Amazon Web Services (AWS), é uma plataforma serverless que revolucionou a maneira como aplicações são desenvolvidas e executadas na nuvem. Permite aos desenvolvedores executar código em resposta a eventos sem a necessidade de gerenciar servidores, oferecendo escalabilidade automática e eliminando a complexidade da infraestrutura.

## Integrantes do Grupo

- Gabriel Fernandes
- Gustavo Riegert
- Marcos Paulo
- Samuel Lincoln

## Caracterização do Sistema

AWS Lambda é uma plataforma de computação serverless que permite executar código em resposta a eventos, eliminando a necessidade de provisionar ou gerenciar servidores. Ideal para construir aplicações escaláveis e event-driven, a arquitetura do AWS Lambda é desenhada para atender às necessidades de diversos nichos de mercado, incluindo número de clientes, acessos simultâneos e requisitos de segurança. Vamos explorar detalhadamente os componentes e conceitos envolvidos nesta arquitetura.

## Componentes da Arquitetura AWS Lambda
### Fontes de Eventos (Event Sources)

- APIs REST: Métodos de chamada de API via API Gateway da AWS.
- CloudWatch Events: Disparam funções Lambda com base em mudanças no estado de recursos AWS.
- Streams de DynamoDB: Invocam funções Lambda quando há novos registros ou alterações em tabelas DynamoDB.
- Notificações de S3: Triggers baseados em eventos de upload ou alteração de arquivos em buckets S3.
- Agendamento (Cron): Eventos agendados via CloudWatch para execução periódica de funções.

### Função Lambda (Lambda Function)

- Execução do Código: O núcleo da arquitetura, onde o código é executado em resposta aos eventos recebidos.
- Idiomas Suportados: Node.js, Python, Java, Go, entre outros.
- Desempenho e Escalabilidade: Criação de instâncias de forma horizontal para lidar com a carga, conhecido como concorrência.

### Exemplo da Função Lambda

![Exemplo da Função Lambda em funcionamento](https://d2908q01vomqb2.cloudfront.net/d435a6cdd786300dff204ee7c2ef942d3e9034e2/2023/05/31/comofornecercredenciaisdebanco-1.png)

1. Os clientes chamam a API RESTful hospedada no AWS API Gateway
2. O API Gateway executa a função Lambda
3. A função Lambda recupera os segredos do banco de dados usando a API Secrets Manager
4. A função Lambda se conecta ao banco de dados do RDS usando segredos do banco de dados do Secrets Manager e retorna os resultados da consulta

### Versionamento e Alias (Versioning and Alias)

- Versionamento: Funções podem ter múltiplas versões, permitindo gerenciamento de mudanças.
- Alias: Recursos nomeados que apontam para versões específicas de funções, facilitando a implementação de ambientes de desenvolvimento, teste e produção.

### Concorrência (Concurrency)

- Concorrência Não Reservada: Usando a concorrência padrão de 1000 invocações simultâneas por região.
- Concorrência Reservada: Configuração de um limite máximo para evitar impacto em outras funções.
- Concorrência Provisionada: Manutenção de instâncias pré-inicializadas para reduzir a latência e evitar cold starts.

### Variáveis de Ambiente (Environment Variables)

- Armazenamento de Configurações: Permite armazenar dados de configuração e credenciais de forma segura, podendo ser criptografados usando KMS.

### Configurações VPC (VPC Configurations)

- Conectividade de Rede: Lambda pode ser configurado para acessar recursos dentro de uma VPC gerenciada pela AWS.

### Destinações Lambda (Lambda Destinations)

- Integração Sem Código: Permite que funções Lambda se conectem diretamente a outros serviços AWS como SQS, outra função Lambda ou EventBridge sem necessidade de código adicional.

### Acesso IAM (IAM Access)

- Papéis e Políticas: Gerenciamento de permissões através de IAM roles, incluindo AWSLambdaBasicExecutionRole para execuções básicas.

### Monitoramento (Monitoring)

- CloudWatch Logs: Registro de eventos de funções Lambda.
- CloudWatch Metrics: Métricas de desempenho, invocações e concorrência.
- X-Ray: Rastreio distribuído para análise detalhada de desempenho e latência.
- Lumigo: Plataforma de monitoramento serverless que facilita o debugging e análise de desempenho.

### Testes de Funções (Testing Lambda Functions)

- Console AWS: Testes unitários e de integração usando eventos simulados no console da AWS.

### Consumidores de Eventos (Event Consumers)

- Serviços AWS: DynamoDB, S3, SQS, SNS, outras funções Lambda, e APIs RESTful.

### Tecnologias, Padrões e Conceitos Envolvidos na Arquitetura do AWS Lambda 
Serverless Computing

- Definição: Modelo de execução onde o provedor de cloud gerencia a infraestrutura, permitindo que os desenvolvedores foquem no código.
- Benefícios: Redução de custos, escalabilidade automática e menor necessidade de gerenciamento de infraestrutura.

### Event-driven Architecture

- Definição: Arquitetura onde eventos disparam e comunicam entre serviços, promovendo um sistema desacoplado e escalável.
- Componentes: Produtores de eventos, roteadores de eventos e consumidores de eventos.

### Function-as-a-Service (FaaS)

- Definição: Executar funcionalidades individuais como serviços independentes, permitindo modularidade e escalabilidade.
- Implementação: AWS Lambda, onde cada função é invocada em resposta a eventos específicos.

### Microservices

- Definição: Dividir a aplicação em serviços menores e gerenciáveis que podem ser desenvolvidos, implantados e escalados independentemente.
- Benefícios: Maior flexibilidade, facilidade de manutenção e atualização, e isolamento de falhas.

### APIs RESTful

- Implementação: Uso do API Gateway para criar e gerenciar APIs RESTful que se integram com funções Lambda.
- Benefícios: Facilita a comunicação entre diferentes serviços e plataformas.

### Gerenciamento de Identidade e Acesso (IAM)

- Implementação: Uso de roles e políticas do IAM para controlar o acesso às funções Lambda e outros recursos AWS.
- Segurança: Garantia de que apenas serviços e usuários autorizados possam interagir com funções Lambda.

### Monitoramento e Logging

- CloudWatch: Serviço para monitoramento e logging de funções Lambda.
- X-Ray: Ferramenta para rastreamento distribuído e análise de desempenho.
- Lumigo: Plataforma de monitoramento para facilitar o debugging e a análise de desempenho.

### Configuração de Ambiente e VPC

- Variáveis de Ambiente: Armazenamento seguro de configurações e credenciais.
- Configuração VPC: Conexão segura entre funções Lambda e recursos dentro de uma VPC.

### Referências

MUDAR REFERENCIAS 
- Livro Engenharia de Software Moderna: [Capítulo 7 - Arquitetura de Software](https://engsoftmoderna.info/cap7.html#introdu%C3%A7%C3%A3o)
- Documentação oficial da AWS
- Artigos e vídeos sobre a implementação do Pix
