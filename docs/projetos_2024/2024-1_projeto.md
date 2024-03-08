# Implementação de Arquitetura Cloud na AWS com CloudFormation
## **Escopo do Projeto:** 
## Atencao: O seu projeto será avaliado pelo grau de profissionalismo na DOCUMENTACAO!!!


**Objetivo:** Provisionar uma arquitetura na AWS utilizando o CloudFormation, que englobe o uso de um Application Load Balancer (ALB), instâncias EC2 com Auto Scaling e um banco de dados DynamoDb.

**Atencao: A escolha da região de implantacao deve ser baseada em custos e desempenho, isso deve aparecer no seu relatório.**

**Requisitos Técnicos do Projeto:**

### **Rubricas do projeto para tirar C+**

**Infraestrutura como Código (IaC) com CloudFormation:**

- Utilizar o CloudFormation para criar e gerenciar todos os recursos na AWS.
- Estruturar o código utilizando com comentarios explicativos em cada recurso.
- O script deve ser capaz de criar a infraestrutura completa sem a intervenção manual do usuário (comando único).
- O script deve ser capaz de atualizar a infraestrutura completa sem a intervenção manual do usuário (comando único).
- O script deve ser capaz de destruir a infraestrutura completa sem a intervenção manual do usuário (comando único).

**EC2 com Auto Scaling:**

* Criar um Launch Configuration com uma AMI que tenha a aplicação pré-instalada.
* Provisionar um Auto Scaling Group (ASG) utilizando o Launch Configuration criado.
* Definir políticas de escalabilidade baseadas em CloudWatch Alarms (ex: CPU Utilization > 70%).
* Garantir a integração do ASG com o ALB através do Target Group.

**Application Load Balancer (ALB):**

* Provisionar um ALB para distribuir o tráfego entre as instâncias EC2.
* Configurar Target Groups para gerenciar as instâncias EC2.
* Implementar Health Checks para garantir que o tráfego seja direcionado apenas para instâncias saudáveis.

**Banco de Dados DynamoDb:**

* Provisionar uma instância DynamoDb.
* Configurar Security Groups para garantir que apenas as instâncias EC2 possam se conectar ao banco de dados.

**Aplicação:**

* PONTO A SER DEFINIDO.

**Análise de Custo com a Calculadora AWS:**

* Utilizar a Calculadora de Custo da AWS para estimar os custos mensais da arquitetura proposta.
* Considerar os custos de todos os recursos utilizados (EC2, ALB, Db, etc.).

### **O que deverá ser entregue para C+ ---> Documentação:**

* Criar uma documentação técnica que inclua um diagrama da arquitetura AWS.
* Documentar todas as decisões técnicas tomadas e justificá-las.
* Incluir um guia passo a passo de como executar os scripts que você criou (não esquqeca de validar a sua infraestrutura).
* Elaborar um relatório detalhado com a previsão de custos, destacando os principais gastos e possíveis otimizações.
* Colocar o link do repositorio com o código CloudFormation no Documento.

### **Rubricas do projeto para tirar B+**

**Analise de carga:**

* Implementar uma analise de carga e desempenho da arquitetura. (escolher a ferramenta que julgar a mais apropriada para o seu projeto)

* Locust:
O Locust é uma ferramenta popular para testes de carga e desempenho, permitindo simular milhares de usuários simultâneos para testar a resistência de sistemas.


* Apache JMeter:
Uma das ferramentas de teste de carga mais populares e amplamente utilizadas.
Interface gráfica para configuração de testes.
Suporta vários protocolos, incluindo HTTP, JDBC, FTP e mais.
Extensível através de plugins.


* Gatling:
Ferramenta de teste de carga de código aberto escrita em Scala.
Focado em testes de carga para aplicações web.
Oferece relatórios detalhados e é conhecido por sua alta performance.


* Artillery:
Ferramenta moderna, leve e poderosa para testes de carga.
Escrita em Node.js.
Suporta testes de carga para WebSocket, Socket.io, AWS Kinesis e mais.


* LoadRunner:
Ferramenta comercial da Micro Focus.
Uma das ferramentas de teste de carga mais antigas e estabelecidas do mercado.
Oferece uma ampla variedade de recursos e suporte para vários protocolos.


* Taurus:
Ferramenta de automação de testes de carga de código aberto.
Permite executar testes escritos em JMeter, Gatling, Locust, Selenium e outras ferramentas sob uma interface comum.
Focado em simplificar a configuração e execução de testes.


### **O que deverá ser entregue para B+ ---> Documentação:**
* Adicionar a documentação anterior a Análise de Custo real com a utilização dos testes de carga na infraestrutura criada na AWS. Utilizar a aba de Biling da AWS, separar os custos do seu projeto via Tags

### Rubricas do projeto para tirar A

**AWS CodePipeline e AWS Secrets Manager**
O AWS CodePipeline é um serviço totalmente gerenciado de entrega contínua que ajuda a automatizar pipelines de lançamento para oferecer atualizações rápidas e confiáveis de aplicações e infraestruturas.

* Voce deve utilizar os codigo gerados e o entendimento de chaves, para criar uma pipeline na AWS, ela deve atualizar a sua infraestrutura sempre que o codigo for alterado, sem a necessiade de comando por parte de qualquer usuario.
* É obrigatório o uso de AWS Secrets Manager, para guardar as credenciais de acesso programatico da AWS.

### **O que deverá ser entregue para A+ ---> Documentação:**
* Adicionar na documentação anterior a explicacão sobre CodePipeline, como utilizar e como foi a sua infraestrutura é criada a partir de CI/CD.