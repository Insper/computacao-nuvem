# Infraestrutura por Código

Aplicação em Python para gerenciar infraestrutura construída com Terraform.

- **Aluno:** Francisco Pinheiro Janela
- **Curso:** Engenharia da Computação
- **Semestre:** 6
- **Contato:** franciscopj@al.insper.edu.br
- **Ano:** 2022
- **GitHub Page**: https://fran-janela.github.io/roteiro-proj-CompNuvem/

## Como Operar com o meu programa:

!!! Warning
O programa foi desenvolvido por uma única pessoa, e existem algumas falhas na robustez da utilização, ou seja, é da responsabilidade do usuário configurar adequadamente os campos durante a utilização para que a montagem não falhe. Ademais, aproveito para lembrar a **importância da proteção de suas chaves de acesso**, utilize-as apenas em variáveis de ambiente. Esta aplicação utiliza a criação de um arquivo `.env` para armazená-las. Mais sobre isso na aba de Pré-Requisitos.

## Pré-requisitos

Para começar a operar com o meu programa, sigam o passo a passo indicado no readme do [meu repositório](https://github.com/fran-janela/projeto-comp-nuvem) no github.

## Como usar

Ao iniciar o programa pela primeira vez, o usuário se depara com a escolha entre a configuração das regiões, podendo, nesse caminho, gerenciar instâncias, gerenciar security groups e levantar aplicações em **HA** (High Availability), e a configuração do ambiente do IAM, onde o usuário pode gerenciar usuários e políticas(restrições).

Para facilitar, a árvore de navegação abaixo, pode trazer mais facilidade para o usuário se encontrar pelo programa:

```
├── Configuração de Regiões
│   ├── Criar, deletar ou escolher uma região
│   ├── Gerenciar Instâncias
│   │   ├── Listar Instâncias
│   │   ├── Criar Instância
│   │   ├── Deletar Instância
│   │   ├── Atualizar Configuração de uma Instância
│   │   └── Voltar
│   ├── Gerenciar Security Groups
│   │   ├── Listar Security Groups
│   │   ├── Criar Security Group
│   │   ├── Deletar Security Group
│   │   ├── Adicionar Regras a um Security Group
│   │   ├── Deletar Regras de um Security Group
│   │   └── Voltar
│   └── Gerenciar Aplicação em HA
│       ├── Listar Aplicação em HA
│       ├── Criar Aplicação em HA
│       ├── Deletar Aplicação em HA
│       └── Voltar
├── Configuração do IAM
│   ├── Limpar ou Restaurar a Infraestrutura do IAM
│   ├── Gerenciar Usuários
│   │   ├── Listar Usuários
│   │   ├── Criar Usuário
│   │   ├── Deletar Usuário
│   │   ├── Adicionar Políticas a um Usuário
│   │   ├── Deletar Políticas de um Usuário
│   │   └── Voltar
│   └── Gerenciar Políticas
│       ├── Listar Políticas
│       ├── Importar Política
│       └── Voltar
├── Listar todas as Instâncias
└── Sair
```

Em sua maioria, as instruções de uso de cada uma das funcionalidades está autocontida no próprio programa, mas existem algumas considerações que podem ser feitas:

### Configuração de Regiões

#### Criar, deletar ou escolher uma região

- Ao criar uma região em um uma daquelas disponíveis no programa, garanta que a sua conta possua permissões para fazê-lo, pois isso pode gerar um problema para o bom funcionamento da aplicação. Ao criar uma nova região, automáticamente a infraestrutura básica é copiada da pasta de `sample` para uma com o nome da região, com a adição do prefixo `tf-`.

- Ao escolher a opção de deletar uma região, não existe confirmação necessária, e se o comando for executado, a região será deletada, ou seja, irá perder todos os recursos criados naquela região de uma vez. Portanto, é importante que o usuário tenha certeza de que deseja deletar a região.

#### Gerenciar Instâncias

- Ao Listar as Instâncias, o usuário deve escolher pelo número mostrado na tela aquela que quer visualizar mais informações.

- Ao Criar uma Instância, o usuário deve escolher o tipo de instância que deseja criar, e o nome da instância que deseja criar. O nome da instância deve ser único, ou seja, não pode haver duas instâncias com o mesmo nome na mesma região. Além disso, o número de instâncias olocado é a quantidade de réplicas aquelas configurações que irão ser criadas. Por fim, o Sistema Operacional pré definido é o `Ubuntu Server 18.04 LTS`.

??? Warning
O usuário deve ter criado previamente seu `par de chaves` na AWS para poder indicá-lo na criação de uma instância e, por sua vez, poder acessá-lo via ssh posteriormente.

- Ao atualizar a configuração de uma instância estará mudando todas as réplicas criadas. Quando for feita a mudança de número de instâncias, será sempre a com índice maior que será deletada. Ao mudar os _ids_ dos security groups, deverá passar novamente todos aqueles que desejar aplicar à instância, configurações antigas serão perdidas.

#### Gerenciar Security Groups

- Ao Listar os Security Groups, o usuário deve escolher pelo número mostrado na tela aquele que quer visualizar mais informações.

- Ao Criar um Security Group, o usuário deve escolher o nome do Security Group que deseja criar. O nome do Security Group deve ser único, ou seja, não pode haver dois Security Groups com o mesmo nome na mesma região. Além disso, poderá ser criado quantas regras de Ingress e Egress que o usuário desejar, se atentando somente à liberação de todas as portas para não correr riscos de segurança.

- Só será possível deletar um Security Group se ele não estiver sendo usado, ou seja, se quiser deletá-lo, deve remover todas as dependências dele nas instâncias da região.

#### Gerenciar Aplicação em HA

Em primeiro lugar, a Aplicação em HA é uma demo com funcionamento limitado, que permite a criação de uma aplicação predefinida e utiliza sistemas de _Auto Scalling_ e _Load Balancing_ disponíveis na AWS. Só é possível criar em duas regiões: `us-east-1` e `us-east-2`.

- Só pode ser criada uma aplicação em HA por região, ou seja, se já houver uma aplicação em HA criada na região, não será possível criar outra.

- Para pegar a URL da aplicação e poder acessá-la, basta listar a aplicação no programa.

### Configuração do IAM

#### Limpar ou Restaurar a Infraestrutura do IAM

- Limpar a infraestrutura do IAM significa apagar todas as configurações pré criadas para usuários, mas todos as políticas importadas continuarão sendo criadas quando for restaurada a infraestrutura.

- A Infraestrutura vem configurada com 4 políticas de teste: _AdministratorAccess_, _AdminNorthVirginia_, _AdminOregon_ e _AdminOhio_. Essas políticas são criadas automaticamente quando a infraestrutura é restaurada, e não podem ser deletadas.

#### Gerenciar Usuários

- Ao Listar os Usuários, desta vez o usuário não precisa escolher pelo número mostrado na tela, pois o programa já irá mostrar as informações de todos os usuários e todas as políticas atreladas a eles.

- Ao Criar um Usuário, o usuário deve escolher o nome do Usuário que deseja criar. O nome do Usuário deve ser único, ou seja, não pode haver dois Usuários com o mesmo nome na mesma região. Além disso, a senha aparecerá somente na criação deste, então guarde-a em um local seguro antes de continuar. Atrelar uma política (restrição) ao usuário, deve ser feita posteriormente com a função de adicionar políticas.

- Ao deletar um Usuário, o usuário não poderá ser recuperado, e todas as configurações de políticas atreladas também serão descartadas, mas as políticas em si ainda continuarão existindo.

#### Gerenciar Políticas

- Ao Listar as Políticas, o usuário deve escolher pelo número mostrado na tela aquela que quer visualizar mais informações.

- Para importar uma política, o usuário deve passar o _path_ completo do arquivo `.json`. Caso seja um arquivo válido, a regra será criada e permanentemente adicionada ao seu repositório de políticas. Para deletá-la, deve apagar o arquivo .json criado em `iam/policies/`. O nome da política será o nome do arquivo, sem a extensão.

- Para facilitar a criação, construa a política pela dashboard da AWS e copie o conteúdo do arquivo `.json` gerado.

---

## Roteiro DIY

## Começando

Para seguir esse tutorial é necessário:

- **Tecnologias:** Terraform, Python
- **Documentos:** [Terraform AWS Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- **Pré-Requisitos:** aqueles anteriormente destacados para o funcionamento do programa e uma conta na AWS com permissões de administrador e suas credenciais.

!!! Danger
**ATENÇÃO:** Estas próximas etapas serão feitas para vias de estudo, não é recomendado que sejam feitas em um ambiente de produção. Além disso, as chaves que serão utilizadas são extremamente sensíveis, então não as compartilhe com ninguém, muito menos disponibilize-as no _GitHub_ ou similares. **Daqui em diante é por sua conta e risco.**

## O que é Terraform?

**Terraform** é uma ferramenta de infraestrutura por código, desenvolvida pela _HashiCorp_, que te permite definir, tanto para _Cloud Pública_, quanto para _Cloud Privada_, recursos de infraestrutura em código possível de ser lido pelo ser humano e pelo computador, podendo ser versionado, reutilizádo e compartilhado.

### Terraform e AWS

A HashiCorp disponibiliza uma série de módulos para os recursos na aws que podem ser copiados e reconfigurados para construir a sua infraestrutura. Para facilitar a sua pesquisa, a documentação no link acima é de grande utilidade.

Existem 4 grandes tipos de módulos que serão explorados neste roteiro, são eles:

- **Provider:** é o módulo que permite a comunicação com a AWS, e é o primeiro módulo que deve ser importado. Ele é responsável por definir a região que será utilizada, e também as credenciais de acesso.

- **Resource:** é o módulo que define os recursos que serão utilizados na AWS. Por exemplo, se você deseja criar uma instância EC2, você deve importar o módulo `aws_instance` e configurar os parâmetros necessários para a criação da instância.

- **Data:** é o módulo que permite a consulta de informações de recursos já existentes na AWS. Por exemplo, se você deseja consultar o ID de uma instância EC2, você deve importar o módulo `aws_instance` e configurar os parâmetros necessários para a consulta da instância.

- **Output:** é o módulo que permite a visualização de informações de recursos já existentes na AWS. Por exemplo, se você deseja visualizar o ID de uma instância EC2, você deve importar o módulo `aws_instance` e configurar os parâmetros necessários para a visualização da instância.

## Criando a Infraestrutura Básica para o roteiro

Em primeiro lugar, defina um diretório(pasta) para o seu projeto. Isso vai ser importante para posteriormente replicar o que foi feito e poder escalar para a construção de uma infraestrutura maior com o auxílio de uma aplicação em `python`. Dê o nome de `sample` para o diretório, pois ele será a amostra replicada para cada região. Para este tutorial iremos utilizar somente a região `us-east-1` (Norte da Virgínia).

Dentro deste diretório, crie um arquivo chamado `main.tf` e outro chamado `variables.tf`. O primeiro será responsável por definir os providers necessários e iniciar a estrutura do terraform, e o segundo será responsável por definir as variáveis que serão utilizadas para a criação dos recursos.

- Dentro do arquivo `main.tf`, insira o seguinte código:

```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}
```

Este _Snipet_ de código é responsável, então, por definir a versão do terraform que será utilizada e também a versão do provider `aws` que será necessário.

Além disso, é necessário definir, em si, a região do provider e passar a ele as credenciais para poder acessar a sua AWS.

- Em um novo arquivo `provider.tf`, insira o seguinte código:

```terraform
provider "aws" {
  region = var.region
  access_key = var.AWS_ACCESS_KEY_ID
  secret_key = var.AWS_SECRET_ACCESS_KEY
}
```

- E no arquivo já criado `variables.tf`, insira o seguinte código:

```terraform
variable "region" {
  type = string
  default = "us-east-1"
}

variable "AWS_ACCESS_KEY_ID" {
  type = string
  sensitive = true
}

variable "AWS_SECRET_ACCESS_KEY" {
  type = string
  sensitive = true
}
```

!!! Info
O arquivo `variables.tf` é responsável por definir as variáveis que serão utilizadas na infraestrutura do Terraform. O parâmetro `sensitive = true` é responsável por ocultar a variável quando for executado o comando `terraform plan` ou `terraform apply`.

- Agora, execute o comando `terraform init` para que o terraform baixe os providers necessários para a criação da infraestrutura.

```cmd
terraform init
```

### Definindo as variáveis para o código:

Anteriormente foi falado da importância de manter o sigilo quanto **às chaves de acesso à AWS**, e, portanto, iremos precisar de um arquivo que as contenha, e ao mesmo tempo, não seja enviado para nenhum repositório aberto.

O Terraform consegue ler um arquivo e dele extrair as variáveis que serão utilizadas na infraestrutura. Para isso, crie um arquivo chamado `config.tfvars.json` dentro de uma pasta `config`. É importante que estes estejam descritos no seu arquivo `.gitignore` ou similares.

- Adicione o conteúdo a esse arquivo:

```json
{
  "region": "us-east-1",
  "AWS_ACCESS_KEY_ID": ["SEU_ID_CHAVE"],
  "AWS_SECRET_ACCESS_KEY": ["SUA_SECRET_KEY"]
}
```

O arquivo `variables.tf` será responsável por informar ao terraform quais as variáveis que serão necessárias e quais os seus tipos. O arquivo `config.tfvars.json` será responsável por informar ao terraform quais os valores que serão utilizados para as variáveis.

Agora, podemos aplicar a nossa infraestrutura. Para isso, execute o comando `terraform apply` e informe o arquivo `config.tfvars.json` como variável de entrada.

```cmd
terraform apply -var-file=config/config.tfvars.json
```

## Criando a Infraestrutura de Rede

Agora que já temos a infraestrutura básica criada, podemos começar a criar a infraestrutura de rede. Para isso, iremos criar um arquivo chamado `network.tf` e nele iremos definir os recursos que serão utilizados para a criação da infraestrutura de rede.

Para a criação de rede, vamos começar a exercitar a pesquisa na documentação do terraform. Crie um recurso para cada uma das seguintes funcionalidades e adicione os parâmetros também descritos:

- **VPC:** cidr_block, instance_tenancy, enable_dns_support, enable_dns_hostnames e tags={Name}
- **Subnet:** vpc_id, cidr_block, map_public_ip_on_launch e tags={Name}
- **Internet Gateway:** vpc_id e tags={Name}
- **Route Table:** vpc_id e tags={Name}
- **Route:** route_table_id, destination_cidr_block e gateway_id
- **Route Table Association:** subnet_id e route_table_id

Para as configurações de rede, adicione ao arquivo `variables.tf` as seguintes variáveis:

```terraform
variable "network_configurations" {
  type = object({
    vpcCIDRblock = string
    instanceTenancy = string
    dnsSupport = bool
    dnsHostNames = bool
    publicsCIDRblock = string
    mapPublicIP = bool
    publicdestCIDRblock = string
  })
}
```

E como exemplo, adicione ao arquivo `config.tfvars.json` as seguintes configurações:

```json
"network_configurations": {
        "vpcCIDRblock": "172.16.0.0/16",
        "instanceTenancy": "default",
        "dnsSupport": true,
        "dnsHostNames": true,
        "publicsCIDRblock": "172.16.10.0/24",
        "mapPublicIP": true,
        "publicdestCIDRblock": "0.0.0.0/0"
}
```

O restante das variáveis, associe diretamente no arquivo `network.tf`, utilizando a seguinte estrutura:

```terraform
variavel = [recurso].[nome_do_recurso].[variável_desejada]

# Exemplo:
vpc_id = aws_vpc.VPC.id
```

## Criando Instâncias EC2

A criação de instâncias vai nos trazer alguns conceitos extremamente interessantes para a escalabilidade da nossa aplicação no terraform, são estes: `count`, `for_each`, e `locals`. Vamos começar pelo básico.

- Crie uma instância usando o recurso `aws_instance` no arquivo `instances.tf`.

- Realize o Apply da infraestrutura e veja sua instância sendo criada.

- Utilizando a módulo de `output` do terraform, crie um output para a instância criada. O output deve conter o id da instância e o DNS público e estará localizado no arquivo gerado automáticamente `terraform.tfstate`.

### Escalando com o count

- Com o argumento `count` dentro da definição do recurso, crie 3 instâncias EC2.

- Execute o `terraform apply` e veja as 3 instâncias sendo criadas.

O **count** é um sistema de criação em massa de instâncias com as mesmas configurações, e deve ser usado para rapidamente construir um grupo de máquinas com as mesmas configurações para provavelmente a mesma aplicação. Para possuir maior controle sobre o múltiplo deploy de instâncias, é mais recomendado usar o `for_each`.

### Escalando com o for_each

Em primeiro lugar, o for_each irá utilizar da configuração de variáveis no formato de `list` ou `map` para criar múltiplas instâncias com configurações diferentes. Para isso, vamos criar uma variável no arquivo `variables.tf`:

```terraform
variable "instances_configuration" {
  type = list(object({
    instance_name = string
    instance_type = string
    ami           = string
    key_name      = string
  }))
}
```

O tipo `list` indica ao terraform que a variável é uma lista e deve ser percorrida pelo **for_each**. Já o tipo `object` indica que a variável é um objeto, ou seja, um conjunto de variáveis definidas, que podem ser acessadas pela sua chave. No arquivo de variàveis **.json**, deve ser construido os valores da forma descrita acima.

- O recurso da instância com a construção do for_each deve ser similar a:

```terraform
resource "aws_instance" "web" {
  for_each = {for instance in var.instances_configuration: instance.instance_name =>  instance}
  ami           = each.value.ami
  instance_type = each.value.instance_type
  subnet_id     = aws_subnet.Subnet.id
  key_name      = each.value.key_name

  tags = {
    Name = "${each.value.instance_name}"
  }
}
```

**OBS.:** Note que para indicar o valor de cada instância é usado o complemento `each.value`

- Crie 3 instâncias diferentes com este método.

### Escalando com o for_each e count

É de certo que não é possível usar ambas as configurações for_each e count no mesmo recurso, mas podemos contornar essa situação. Para isso, adicione uma variàvel ao conjunto de variáveis de configuração das instâncias que indicará a quantidade delas a serem criadas.

Em seguida vamos utilizar as variáveis **locais**, com o argumento `locals`. Construindo baseado na ideia de replicar a configuração definida para a quantidade de instâncias, basta criar um for que atenda a essa quantidade e adicione várias vezes a mesma configuração mudando apenas o nome, com o acréscimo de um número que indique indíce, por exemplo. Além disso, para aplicar tais configurações locais, as informações devem ser passadas pela função de `flatten`.

No final, a sua instância deve possuir o seguinte formato:

```terraform
locals {
  serverconfig = [
    for srv in var.instances_configuration : [
      for i in range(1, srv.no_of_instances+1) : {
        instance_name = "${srv.instance_name}-${i}"
        instance_type = srv.instance_type
        ami = srv.ami
        security_groups_ids = srv.security_groups_ids
        key_name = srv.key_name
      }
    ]
  ]
}

locals {
  instances = flatten(local.serverconfig)
}

resource "aws_instance" "web" {
  for_each = {for server in local.instances: server.instance_name =>  server}
  ami           = each.value.ami
  instance_type = each.value.instance_type
  subnet_id = aws_subnet.Subnet.id
  vpc_security_group_ids = each.value.security_groups_ids
  key_name = each.value.key_name

  tags = {
    Name = "${each.value.instance_name}"
  }
}

output "instances" {
  value       = [for instance in aws_instance.web : instance]
  description = "All Machine details"
}
```

## Criando Security Groups

Para a criação dos security groups, vamos utilizar o método do **for_each** pensando na escalabilidade da solução. Além disso, na AWS é possível adicionar várias regras tanto de `Ingress` (Inbound) quanto de `Egress` (Outbound) ao mesmo tempo, portanto, nossa aplicação também deve conseguir fazê-lo.

- Crie o arquivo `security_groups.tf` e construa as suas configurações.

??? Dica
Para criar múltiplas regras de _Ingress_ e _Egress_, utilize variáveis do tipo `dynamic`.

- Teste criando 2 grupos de segurança, um com uma regra de _Ingress_ e duas regras de _Egress_ e outro com duas regras de _Ingress_ e uma regra de _Egress_.

### Aplicando o security group nas instâncias

Utilizando a função de `output`, é possível coletar o ID do _Security Group_ definido automáticamente pela AWS.

Para atrelá-lo a uma instância use a variável do recurso `aws_instance` chamada `vpc_security_group_ids` e passe uma lista de IDs de _Security Groups_ como valor.

- Crie um Security Group que libere a conexão SSH e associe-o a uma instância

- Junto com o par de chaves criado e associado a `key_name`, teste o acesso à instância.

## Criando Infraestrutura para o IAM

Para a criação da estrutura no IAM, serão necessários 2 recursos principais: o `usuário` em si e as `policies`(políticas ou restrições) de acesso. Além disso, são necessários recursos que criem o usuário e atrelem a ele uma senha automática (que pode ser exportada como `output`), um recurso que crie o documento da política, para facilitar a implementação, e recursos que criem a conexão entre o usuário e a política.

- Crie o arquivo `policies.tf` e construa as suas configurações.

??? Dica
Para atrelar um documento a uma política, use a seguinte variável e sua configuração:
`terraform
    policy = data.aws_iam_policy_document.ec2_policy[each.value.name].json
    `

- Crie o arquivo `users.tf` e construa as suas configurações.

- Associe uma política criada a um usuário através do recurso `aws_iam_user_policy_attachment`.

??? Dica
Crie uma variàvel para cada uma das configurações acima, ou seja, uma variável para a configuração de políticas, outra para a configuração de usuários e outra para a configuração de atrelamento de políticas a usuários.

- Teste a criação de um usuário com a restrição de acesso à região da North Virginia. A política criada para isso está abaixo:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "us-east-1"
        }
      }
    }
  ]
}
```

## Criando múltiplas Regiões

Como os usuários são globais, não vamos nos preocupar com suas configurações para cada instância, eles podem receber sua pasta separada para gerenciamento de infraestrutura. Pensando, então, nos outros arquivos, ou seja,`main.tf`, `provider.tf`, `network.tf`, `instances.tf`, `security_groups.tf`, para criar uma nova região, basta replicar todo o diretório, mudando apenas no arquivo de configurações `.json` a região do _provider_.

- Crie duas pastas com essa infraestrutura, uma para a região da North Virginia e outra para a região de Ohio.

- Teste a criação de uma instância em cada região.

**OBS.:** Aplique o comando de `init` e `apply` em cada uma das pastas criadas.

## Criando um HA de servidores web

### Configurando uma Imagem Base

Para a criação de um HA de servidores web, é necessário primeiro criar uma imagem(`ami`) que funcionará como template para a criação de instâncias caso as máquinas base estejam ficando sobre-lotadas.

- Crie uma instância com o sistema operacional Ubuntu Server 18.04 LTS.

- Aplique:

```cmd
sudo apt update; sudo apt install nodejs build-essential -y
```

- Edite um arquivo server.js:

```js
#!/usr/bin/env nodejs
var http = require("http");
var os = require("os");
var crypto = require("crypto");

http
  .createServer(function (req, res) {
    res.writeHead(200, { "Content-Type": "text/plain" });
    var nonce = 1;
    var seed = Math.random();
    var h = crypto.createHash("sha256");

    h.update(new Buffer(nonce + " Hello World " + seed));
    while (h.digest("hex").substr(0, 3) != "000") {
      h = crypto.createHash("sha256");
      nonce++;
      h.update(new Buffer(nonce + " Hello World " + seed));
    }

    res.end('{ "host": ' + os.hostname() + ', "nonce": ' + nonce + "}");
  })
  .listen(8080, "");
console.log("Server running at http://localhost:8080/");
```

- Torne o arquivo executável:

```cmd
chmod +x ./server.js
```

- Execute e teste o servidor(lembre-se de liberar a porta no security group):

- Configure a máquina para iniciar o servidor automaticamente após `reboot`:

```cmd
crontab -e\ @reboot /home/ubuntu/server.js
```

- Dê `reboot` e teste o acesso ao servidor novamente.

??? Copywright
O procedimento foi retirado do [site oficial da matéria](https://insper.github.io/computacao-nuvem/projetos/0.Cloud_Intro/#escalabilidade).

Com o template de instância criado, gere uma imagem dele pela **dashboard da AWS** e salve a `ami` gerada para uso no próximos passos.

### Criando os recursos para o HA

Para construir o HA, vamos utilizar o recurso `aws_autoscaling_group`, emparelhado com `aws_launch_configuration` e também `aws_lb` (_Load Balence_). Para isso, construa a infraestrutura baseada neste tutorial: [Tutorial de HA](https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg). Ele foi produzido pela Hashicorp, empresa que desenvolve o Terraform, mas em caso de dúvida, o resultado esperado se encontra dentro da pasta `sample-HA` no repositório do meu programa.

??? Dicas - Crie _Security Groups_ diferentes para o _Load Balencer_ e para configuração das instâncias.

    - São necessárias 3 *Subnets* para a criação do *Load Balencer*.

## Crie seu Próprio Programa.

Com toda a experiência adquirida na formatação, construção e manipulação da infraestrutura por meio do terraform, agora você é capaz de criar o seu prórpio programa.

Eu criei, utilizando `Python`, uma ferramenta que roda no terminal e executa as operações descritas acima, de forma automatizada. Para isso, a aplicação copia os arquivos de base, armazenados na pasta `sample` para uma nova pasta com o nome da região, configura o arquivo `.tvars.json` com as informações descritas pelo usuário e executa o terraform para a criação da infraestrutura.

O seu programa pode ser criado via `Python` ou qualquer outra linguagem que você se sinta confortável para manipulação de arquivos e execução de comandos. É possível, também, que essas configurações sejam feitas via **backend** e toda a interface de usuário seja feita via **frontend** em outra linguagem, uma vez que toda a configuração da infraestrutura pode ser enviada via `.json` para o backend.

**Aqui o céu é o limite!** Use a sua criatividade!

## Motivação

Minha motivação para a criação desta aplicação e, consequentemente, este tutorial veio da crescente vontade de aprender sobre infraestrutura e Computação Nuvem, o que me motivou a tentar produzir algo robusto e confiável, que pudesse ser utilizado por pessoas com algum conhecimento em infraestrutura, assim como eu, mas com a vontade de aprender.
