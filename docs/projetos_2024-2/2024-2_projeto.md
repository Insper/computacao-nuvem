# Projeto 2024.2

!!! info inline end

    PROJETO: **INDIVIDUAL**

    DEADLINE: **22.nov.2024**

O projeto do semestre trata de uma API [RESTful](https://www.w3.org/2001/sw/wiki/REST){:target="_blank"} que deve ser capaz de cadastrar e autenticar usuários. Logo, para a execução do projeto, é necessário a construção de uma API RESTful para validar a infraestrutura de um aplicativo. Após a construção da API, o projeto deve ser dockerizado e, então, implantado no AWS. A fim de realizar todo o projeto, ele foi dividido em 2 etapas:


1. [Dockerinzing](#dockerinzing)

2. [AWS](#aws)

A base do projeto é a construção da API.

## Construção da API

O aplicativo teve ser uma API RESTful simples, sem interface visual. Sendo que a API deve ser capaz de cadastrar e autenticar usuários, além de permitir a consulta de dados de terceiros.

A API dever ter no mínimo 3 endpoints:

???+ note "Registro de Usuário"
    
    ``` http title="Endpoint"
    POST /registrar
    ```

    Request
    ``` json title="JSON payload"
    {
        "nome": "Disciplina Cloud",
        "email": "cloud@insper.edu.br",
        "senha": "cloud0"
    }
    ```

    Response
    ``` json title="JSON payload"
    {
        "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkRpc2NpcGxpbmEgQ2xvdWQiLCJpYXQiOjE1MTYyMzkwMjJ9.s76o9X4UIANSI-aTF8UhqnBYyIRWw_WH4ut8Xqmo6i0"
    }
    ```

    ``` mermaid
    sequenceDiagram
        autonumber
        actor Alice
        Alice->>+App: POST /registrar
        App->>+Postgres: consulta email
        break se email encontrado
            Postgres-->>Alice: error 409
        end
        App->>Postgres: grava dados e hash da senha no bd
        App->>App: gera JWT Token
        App-->>-Alice: retorna JWT Token
    ```

    !!! failure "Senha"
        
        Nunca guarde a senha do usuário no banco, apenas uma hash da senha.

???+ note "Autenticação de Usuário"

    ``` http title="Endpoint"
    POST /login
    ```

    Request
    ``` json title="JSON payload"
    {
        "email": "cloud@insper.edu.br",
        "senha": "cloud0"
    }
    ```

    Response
    ``` json title="JSON payload"
    {
        "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
                eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkRpc2N
                pcGxpbmEgQ2xvdWQiLCJpYXQiOjE1MTYyMzkwMjJ9.
                s76o9X4UIANSI-aTF8UhqnBYyIRWw_WH4ut8Xqmo6i0"
    }
    ```

    Diagrama de Sequência
    ``` mermaid
    sequenceDiagram
        autonumber
        actor Alice
        Alice->>+App: POST /login
        App->>+Postgres: consulta email e hash no db
        break se email não encontrado
            Postgres-->>Alice: error 401
        end
        break se email e senha não confere
            Postgres-->>Alice: error 401
        end
        App->>App: gera JWT Token
        App-->>-Alice: retorna JWT Token

    ```

???+ note "Aquisição dos Dados"

    ``` http title="Endpoint"
    GET /consultar
    
    ### HEADER
    Authorization: Bearer <JWT>
    ```

    !!! tip "Response"
    
        A resposta pode ser qualquer scrap de uma página de terceiros, no caso aqui, temos um scrap dos dados do índice Bovespa, apenas os últimos 10 dias, partindo da data de consulta. O formato também pode ser qualquer um, aqui temos um exemplo do mesmo dado em CSV e JSON.

        === "Dados"

            |Date|Open|High|Low|Close|Volume|
            |---|---|---|---|---|---|
            |2024-09-05|136112\.0|136656\.0|135959\.0|136502\.0|7528700|
            |2024-09-06|136508\.0|136653\.0|134476\.0|134572\.0|7563300|
            |2024-09-09|134574\.0|135250\.0|134399\.0|134737\.0|6587600|
            |2024-09-10|134738\.0|134738\.0|133754\.0|134320\.0|8253500|
            |2024-09-11|134319\.0|135087\.0|133757\.0|134677\.0|7947300|
            |2024-09-12|134677\.0|134777\.0|133591\.0|134029\.0|7004900|
            |2024-09-13|134031\.0|135879\.0|134031\.0|134882\.0|8866000|
            |2024-09-16|134885\.0|135715\.0|134870\.0|135118\.0|6707000|

        === "CSV"

            ``` csv
            Date,Open,High,Low,Close,Volume
            2024-09-05,136112.0,136656.0,135959.0,136502.0,7528700
            2024-09-06,136508.0,136653.0,134476.0,134572.0,7563300
            2024-09-09,134574.0,135250.0,134399.0,134737.0,6587600
            2024-09-10,134738.0,134738.0,133754.0,134320.0,8253500
            2024-09-11,134319.0,135087.0,133757.0,134677.0,7947300
            2024-09-12,134677.0,134777.0,133591.0,134029.0,7004900
            2024-09-13,134031.0,135879.0,134031.0,134882.0,8866000
            2024-09-16,134885.0,135715.0,134870.0,135118.0,6707000
            ```

        === "JSON"

            ``` json
            [
                {"Date":"2024-09-05","Open":136112.0,"High":136656.0,"Low":135959.0,"Close":136502.0,"Volume":7528700},
                {"Date":"2024-09-06","Open":136508.0,"High":136653.0,"Low":134476.0,"Close":134572.0,"Volume":7563300},
                {"Date":"2024-09-09","Open":134574.0,"High":135250.0,"Low":134399.0,"Close":134737.0,"Volume":6587600},
                {"Date":"2024-09-10","Open":134738.0,"High":134738.0,"Low":133754.0,"Close":134320.0,"Volume":8253500},
                {"Date":"2024-09-11","Open":134319.0,"High":135087.0,"Low":133757.0,"Close":134677.0,"Volume":7947300},
                {"Date":"2024-09-12","Open":134677.0,"High":134777.0,"Low":133591.0,"Close":134029.0,"Volume":7004900},
                {"Date":"2024-09-13","Open":134031.0,"High":135879.0,"Low":134031.0,"Close":134882.0,"Volume":8866000},
                {"Date":"2024-09-16","Open":134885.0,"High":135715.0,"Low":134870.0,"Close":135118.0,"Volume":6707000}
            ]
            ```

    ``` mermaid
    sequenceDiagram
        autonumber
        actor Alice
        Alice->>+App: GET /consultar <br> Token JWT no header
        App-->>App: verifica permissão do JWT
        break se JWT ausente ou inválido
            App-->>Alice: error 403
        end
        App-->>App: web scraping<br>solicita dados de uma base ou página<br>de um 3th party
        Note right of App: Adquire dados da internet, <br>fazendo scraping de quaisquer<br> dados interessantes para o aluno.<br>O conteúdo deve ter atualização frequente.
        App-->>-Alice: retorna dados
    ```

    !!! warning "Aquisição dos Dados"

        Os dados devolvidos pela consulta devem ser de uma página de terceiros, e devem ser atualizados frequentemente. Caso o usuário não tenha um token válido, a API deve retornar um erro 403.

        A escolha dos dados é livre, mas deve ser algo que possa ser atualizado frequentemente, ao menos, diariamente. Claro, respeitando os termos de uso do site.

!!! tip

    O projeto pode ser desenvolvido em qualquer linguagem de programação, mas é recomendado o uso de Python ou Java.

## Dockerinzing

Quando o código da API estiver pronto, ele deve ser dockerizado. Para isso, você deve criar um arquivo `Dockerfile` (de acordo com a linguagem e ambiente de execução escolhidos) e um `compose.yaml` para a execução da aplicação.

O docker compose deve conter pelo menos 2 serviços: a aplicação e o banco de dados. A aplicação deve ser capaz de se conectar ao banco de dados e realizar as operações de CRUD. Conforme ilustrado abaixo:

``` mermaid
flowchart LR
    subgraph api [Docker Compose]
        direction TB
        app e3@==> db@{ shape: cyl, label: "Database" }
    end
    internet e1@==>|request| app
    e1@{ animate: true }
    e3@{ animate: true }
```



A aplicação deve ser autocontida, ou seja, deve ser possível executar a aplicação apenas com o comando `docker compose up` - pois isso é parte essencial da entrega.


<!-- termynal -->

```shell
> docker compose up -d
[+] Running 2/2
 ✔ Container database   Started   0.3s
 ✔ Container app        Started   0.5s

> docker compose ps
NAME           SERVICE       STATUS     PORTS
app            app           Up         0.0.0.0:8080->8080/tcp
database       postgres      Up
```


Para organização, é sugerida a seguinte estrutura de diretórios:

``` tree title="estrutura de diretório sugerida"
app
  Dockerfile
  app.py
  requirements.txt
  ...
compose.yaml
.env
```

### Publicação no Docker Hub

Após a dockerização, o projeto deve ser publicado no Docker Hub. O link do Docker Hub deve ser incluído na documentação do projeto.

!!! warning "Publicação no Docker Hub"
    A publicação no docker hub deve ser feita via linha de comando. E os comandos utilizados devem ser incluídos na documentação do projeto.

### Entrega

A entrega deverá ser um link do projeto no GitHub, contendo o código da API e o Dockerfile.

!!! success "Entrega"
    Deve haver uma documentação básica no README.md do repositório:

    - nome do aluno;
    - explicação do projeto - scrap do que foi feito;
    - explicação de como executar a aplicação;
    - documentação dos endpoints da API;
    - screenshot com os endpoints testados;
    - video de execução da aplicação - de até 1 minuto;
    - link para o docker hub do projeto;
    - referência explícita a localização do arquivo `compose.yaml`;
    - o arquivo `compose.yaml` FINAL (entregue) deve utilizar apenas images do docker hub (inclusive as geradas para a api), ou seja, não deve ter `build` dentro dele.

!!! note "Variáveis de Ambiente"
    As credenciais do banco de dados e JWT devem ser passadas via variáveis de ambiente, por um arquivo `.env`. Todavia, **PARA FACILITAR A CORREÇÃO**, as credenciais podem ser passadas diretamente no `compose.yaml` por valores padrões, para que não tenha que haver um arquivo de variáveis de ambiente. Exemplo:

    ``` { .yaml title="compose.yaml" }
    name: app

        db:
            image: postgres:17
            environment:
                POSTGRES_DB: ${POSTGRES_DB:-projeto} # (1)!
                POSTGRES_USER: ${POSTGRES_USER:-projeto}
                POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-projeto}
            ports:
                - 5432:5432 #(2)!
    ```

    1.  Caso a variável de ambiente `POSTGRES_DB` não exista ou seja nula - não seja definida no arquivo `.env` - o valor padrão será `projeto`. Vide [documentação](https://docs.docker.com/reference/compose-file/interpolation/){target='_blank'}.

    2. Aqui é feito um túnel da porta 5432 do container do banco de dados para a porta 5432 do host (no caso localhost). Em um ambiente de produção, essa porta não deve ser exposta, pois ninguém de fora do compose deveria acessar o banco de dados diretamente.

    ``` { .env title=".env" }
    POSTGRES_DB=superprojeto
    POSTGRES_USER=meuprojeto
    POSTGRES_PASSWORD=S3cr3t
    ```

    Ao executar, o docker compose irá utilizar as variáveis de ambiente do arquivo `.env`, caso existam, senão, utilizará os valores padrões definidos já dentro do arquivo `compose.yaml`.

    !!! warning "Segurança"
        Num ambiente de trabalho, as credenciais do banco de dados e JWT devem ser passadas via variáveis de ambiente, nunca diretamente no código. Essa estratégia viabiliza, até mesmo, que hajam credenciais diferentes para cada ambiente (dev, test, prod).

        **NUNCA** coloque credenciais no repositório, mesmo que seja um repositório privado. Ou seja, NUNCA coloque um arquivo `.env` no repositório (GitHub).

        **NUNCA** deixe portas expostas em produção, a menos que seja estritamente necessário.

!!! tip "Documentação"
    A documentação é um dos pontos mais importantes do projeto. Seja criativo e use imagens, gifs, tabelas, etc. Também, se possível, faça uso de  ferramentas:
    
    - [mkdocs](https://www.mkdocs.org/){target='_blank'} para gerar a documentação e hospedá-la no GitHub Pages.
    - [mermaid](https://mermaid-js.github.io/mermaid/#/){target='_blank'} para gerar diagramas de sequência, fluxogramas, etc.

## AWS

O próximo passo é implantar a aplicação no AWS. A implantação deve ser feita utilizando o Elastic Kubernetes Service (EKS). A aplicação deve ser implantada em um cluster EKS.

O Kubernetes é uma ferramenta de orquestração de contêineres que automatiza a implantação, o dimensionamento e a gestão de aplicações em contêineres. O EKS é um serviço gerenciado que facilita a execução do Kubernetes na AWS.

Você deve subir um cluster EKS e implantar dois PODs, sendo um da aplicação e outro do banco de dados. A aplicação deve ser capaz de se conectar ao banco de dados e realizar as operações de endpoints da API acima descritas.

### Entrega

A entrega deverá ser um link do projeto no GitHub, o mesmo do anterior, mas para uma sessão sobre a publicação na AWS, contendo o uma breve explicação e um link para um vídeo, explicando e executando o trabalho entregue.

!!! success "Entrega"
    O vídeo apresentado deve ter entre 2 e 3 minutos e **DEVE demonstrar TODOS** os seguintes itens:

    - logar na conta e acessar o projeto;
    - explicar o que foi feito e mostrar os componentes do projeto (eks, roles, etc);
    - executar o comando `kubectl get pods` e mostrar os pods rodando;
      ``` shell
      kubectl get pods
      ```
    - mostrar o projeto executando na AWS: chamada da API por um cliente (curl, postman, etc);

    No texto deve haver um link para os arquivos de configuração do Kubernetes (arquivos .yaml: deployment.yaml, service.yaml, etcs), repositório do projeto.

## Rubrica

!!! danger "Rubrica"

    | Etapa | Critério | Nota | Observações |
    |:-:|---|:-:|:-:|
    | 1 | API + Dockerização<br> + Docker Hub + Documentação | C | C+<br>até 25.out |
    | 2 | AWS | + 1 conceito | - 2 conceitos se não entregar a etapa do AWS |
    |   | AWS + Documentação | + 2 conceitos |

!!! tip "Ponto extra"
    Se a primeira etapa for entregue até o dia 25.out, o aluno ganha meio conceito extra na nota final, ou seja, se ele tirar C, fica com C+.


## Anexos

### Docker compose: material de aula

``` tree title="estrutura para dois containers num mesmo compose"
api
  Dockerfile
web
  Dockerfile
  hello.txt
.env
compose.yaml
```


=== "./"

    ``` { .env title='.env' .copy .select linenums='1' }
    --8<-- "https://github.com/hsandmann/insper.cloud.projeto/raw/refs/heads/main/samples/dockercompose/.env"
    ```

    ``` { .yaml title='compose.yaml' .copy .select linenums='1' }
    --8<-- "https://github.com/hsandmann/insper.cloud.projeto/raw/refs/heads/main/samples/dockercompose/compose.yaml"
    ```

=== "./api"

    ``` { .dockerfile title='Dockerfile' .copy .select linenums='1' }
    --8<-- "https://github.com/hsandmann/insper.cloud.projeto/raw/refs/heads/main/samples/dockercompose/api/Dockerfile"
    ```

=== "./web"

    ``` { .dockerfile title='Dockerfile' .copy .select linenums='1' }
    --8<-- "https://github.com/hsandmann/insper.cloud.projeto/raw/refs/heads/main/samples/dockercompose/web/Dockerfile"
    ```

    ``` { .txt title='hello.txt' .copy .select linenums='1' }
    --8<-- "https://github.com/hsandmann/insper.cloud.projeto/raw/refs/heads/main/samples/dockercompose/web/hello.txt"
    ```

#### Executando o docker compose

<!-- termynal -->

``` .shell
> docker compose up -d --build
[+] Running 4/4
 ✔ Container projeto-api-1  Running       0.0s 
 ✔ Container projeto-api-2  Running       0.0s 
 ✔ Container projeto-api-3  Running       0.0s 
 ✔ Container projeto-web-1  Started  
```

#### Parando o docker compose

<!-- termynal -->

``` .shell
> docker compose down         
[+] Running 5/5
 ✔ Container projeto-web-1  Removed     0.2s 
 ✔ Container projeto-api-1  Removed    10.5s 
 ✔ Container projeto-api-2  Removed    10.4s 
 ✔ Container projeto-api-3  Removed    10.5s 
 ✔ Network projeto_default  Removed 
```

## Referências

[^1]: [Introduction to JSON Web Tokens](https://jwt.io/introduction){target='_blank'}

[^2]: [How to containerize different types of services](https://docs.docker.com/samples/){target='_blank'}

[^3]: :fontawesome-brands-youtube:{ .youtube } [Como criar um cluster Kubernetes na AWS com EKS](https://youtu.be/JrT5YV1KMeY){:target="_blank"} por [Fabricio Veronez](https://github.com/fabricioveronez){:target="_blank"}