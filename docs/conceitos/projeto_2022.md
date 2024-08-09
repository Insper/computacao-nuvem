---
title: Computação em Nuvem
author: Tiago Demay
---

# Projeto Cloud 2022

Infraestrutura como código é o processo de gerenciamento de infraestrutura em um arquivo ou arquivos, em vez de configurar recursos manualmente em uma dashboard. Partindo deste conceito, você deverá:

 **Desenvolver uma aplicação capaz de provisionar uma infraestrutura por meio de uma interface amigável(livre escolha) para gerenciar e administrá-la (construir, alterar e deletar recursos).**

A rubrica abaixo pressupõe que para alcançar o Conceito "B" você tenha feito o Conceito "C" por completo. Assim, para ter "A" precisa que os conceitos anteriores tenham sido alcançados.

Sua aplicação deverá seguir as funções (descrição) abaixo e a tabela completa para alcançar o conceito base.


| Conceito C+ | Descrição                          |
| ----------- | ------------------------------------ |
| `CRIAR`     | :material-check:        *VPC* criação de uma VPC e sub-rede; *instâncias*: esta funcionalidade deverá permitir a escolha de pelo menos 2 tipos de configuração de hosts; ainda deverá ser possível aumentar e diminuir a quantidade de instâncias;  *security group*: criação e a associação de grupos de segurança com instâncias; *Usuário no IAM*. |
| `DELETAR`   | :material-close:        Instâncias, grupos de segurança e usuário. |
| `LISTAR`    | :material-check-all:    Aplicação deverá listar todas instâncias e suas regiões, usuários, grupos de segurança e suas regras. |



| Conceito B  | Descrição                         |
| ----------- | ------------------------------------ |
| `CRIAR`     | :material-check:        Regras em security group; Instância em mais de uma região; Associar algum tipo de restrição de acesso a um usuário; |
| `DELETAR`   | :material-close:        Regras de security group; recursos implantados na Região; |



| Conceito A  | Descrição                          |
| ----------- | ------------------------------------ |
| `CRIAR`     | :material-check:        Criar um HA de servidores web. |



!!! warning
    
    OBS: Será descontado meio conceito na nota do projeto caso algum incidente ou publicação (vazamento) de sua chave AWS for identificada no git hub.


!!! example "ENTREGA"

    * Os projetos deverão ser entregues até às 23h59 do dia 25/11/2022.
    * A entrega será feita via blackboard por meio da associação de seu github.
    * Todos os projetos deverão estar acompanhados de um roteiro (tutorial) de instalação e operação.
    * Serão sorteados/escolhidos 16 projetos para apresentação no dia 01/12/2022.
    * A publicação dos projetos que realizarão a apresentação será no dia 28/11/2022.
    * A apresentação será realizada em um tempo máximo de 15 minutos a partir do roteiro entregue.


:zap::zap::zap: **Falta pouco para terminar o semestre, foquem em terminar os roteiros 3 e 4 em sala e desenvolva o projeto fora do horário de aula.** :zap::zap::zap:

!!! Dica
    Sugerimos que você estude a partir de documentações oficiais e tutoriais técnicos.
        * [terraform.io](https://www.terraform.io/) 
        * [terraform-aws-get-started](https://learn.hashicorp.com/collections/terraform/aws-get-started)