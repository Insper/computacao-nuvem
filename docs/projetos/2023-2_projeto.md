# **Escopo do Projeto:** 
## Implementação de Arquitetura Cloud na AWS com Terraform
**Objetivo:** Provisionar uma arquitetura na AWS utilizando o Terraform, que englobe o uso de um Application Load Balancer (ALB), instâncias EC2 com Auto Scaling e um banco de dados RDS.
**Atencao: A escolha da região de implantacao deve ser baseada em custos e desempenho, isso deve aparecer no seu relatório.**

## **Rubricas do projeto para tirar C+**
**Requisitos Técnicos do Projeto:**

1.
**Infraestrutura como Código (IaC) com Terraform:**

- Utilizar o Terraform para criar e gerenciar todos os recursos na AWS.
- Estruturar o código Terraform utilizando módulos para separar responsabilidades (ex: módulo para EC2, módulo para RDS, etc.).
- Armazenar o estado do Terraform em um bucket S3 para o lock do estado.
- O script deve ser capaz de criar a infraestrutura completa sem a intervenção manual do usuário (comando único).
- O script deve ser capaz de destruir a infraestrutura completa sem a intervenção manual do usuário (comando único).


2.
**Application Load Balancer (ALB):**

* Provisionar um ALB para distribuir o tráfego entre as instâncias EC2.
* Configurar Target Groups para gerenciar as instâncias EC2.
* Implementar Health Checks para garantir que o tráfego seja direcionado apenas para instâncias saudáveis.

3.
**EC2 com Auto Scaling:**

* Criar um Launch Configuration com uma AMI que tenha a aplicação pré-instalada.
* Provisionar um Auto Scaling Group (ASG) utilizando o Launch Configuration criado.
* Definir políticas de escalabilidade baseadas em CloudWatch Alarms (ex: CPU Utilization > 70%).
* Garantir a integração do ASG com o ALB através do Target Group.

4.
**Banco de Dados RDS:**

* Provisionar uma instância RDS MySQL ou PostgreSQL com a configuração db.t2.micro (a menor disponível).
* Habilitar backups automáticos e definir uma janela de manutenção.
* Configurar Security Groups para garantir que apenas as instâncias EC2 possam se conectar ao RDS.
* Habilitar o Multi-AZ para alta disponibilidade.

5.
**Aplicação:**

* A aplicação deve ser uma API RESTful ou uma aplicação web simples.
* Deve ser capaz de se conectar ao banco de dados RDS e realizar operações CRUD.
* Implementar métricas e logs utilizando o CloudWatch.

6.
**Análise de Custo com a Calculadora AWS:**

* Utilizar a Calculadora de Custo da AWS para estimar os custos mensais da arquitetura proposta.
* Considerar os custos de todos os recursos utilizados (EC2, ALB, RDS, etc.).
* Elaborar um relatório detalhado com a previsão de custos, destacando os principais gastos e possíveis otimizações.

7.
**Documentação:**

* Criar uma documentação técnica que inclua um diagrama da arquitetura AWS.
* Documentar todas as decisões técnicas tomadas e justificá-las.
* Incluir um guia passo a passo para executar os scripts Terraform e validar a infraestrutura.

Com estes requisitos, os alunos terão uma visão mais completa não apenas da implementação técnica, mas também dos custos associados, o que é crucial em ambientes de produção reais. 

## **Rubricas do projeto para tirar B+**

8.
**Analise de carga:**

* Implementar uma analise de carga e desempenho da arquitetura. (escolher a ferramenta que julgar a mais apropriada para o seu projeto)
* O Locust é uma ferramenta popular para testes de carga e desempenho, permitindo simular milhares de usuários simultâneos para testar a resistência de sistemas. Existem várias outras ferramentas que oferecem funcionalidades semelhantes. Aqui estão algumas das mais conhecidas:

**Apache JMeter:**
Uma das ferramentas de teste de carga mais populares e amplamente utilizadas.
Interface gráfica para configuração de testes.
Suporta vários protocolos, incluindo HTTP, JDBC, FTP e mais.
Extensível através de plugins.
**Gatling:**
Ferramenta de teste de carga de código aberto escrita em Scala.
Focado em testes de carga para aplicações web.
Oferece relatórios detalhados e é conhecido por sua alta performance.
**Artillery:**
Ferramenta moderna, leve e poderosa para testes de carga.
Escrita em Node.js.
Suporta testes de carga para WebSocket, Socket.io, AWS Kinesis e mais.
**LoadRunner:**
Ferramenta comercial da Micro Focus.
Uma das ferramentas de teste de carga mais antigas e estabelecidas do mercado.
Oferece uma ampla variedade de recursos e suporte para vários protocolos.
**Taurus:**
Ferramenta de automação de testes de carga de código aberto.
Permite executar testes escritos em JMeter, Gatling, Locust, Selenium e outras ferramentas sob uma interface comum.
Focado em simplificar a configuração e execução de testes.


9.
**Documentação:**

* Adicionar a documentação anterior a Análise de Custo real com a utilização dos testes de carga na infraestrutura criada na AWS.

## **Rubricas do projeto para tirar A**

10.
**Banco de Dados e VPN:**

* O script (terraform) deve implementar o banco de dados na Nuvem privada do seu Kit (OpenStack) e a aplicação deve ser conectada a ele via VPN. 

