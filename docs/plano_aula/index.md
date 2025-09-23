# Plano de Aula


## Fluxograma do andamento da disciplina:

<div style="background-color:#f5f5f5; padding: 20px; border-radius: 10px; transform: scale(1.0); transform-origin: top left;">


``` mermaid
---
config:
  layout: dagre
---
flowchart LR
 subgraph subGraph0["Módulo 1"]
        j0["Data de finalização sugerida: 05/09/2025"]
        R1["Roteiro 1 - MAAS"]
        TE1["Teoria 1 - Redes"]
        T1["Tutorial 1 - AWS"]
        i0[" "]
  end
 subgraph subGraph1["Módulo 2"]
        j1["Data de finalização sugerida: 19/09/2025"]
        R2["Roteiro 2 - JUJU"]
        TE2["Teoria 2 - Redes"]
        T2["Tutorial 2 - AWS"]
        i1[" "]
  end
 subgraph subGraph2["Módulo 3"]
        j2["Data de finalização sugerida: 31/10/2025"]
        R3["Roteiro 3 - OpenStack"]
        TE3["Teoria 3 - Redes"]
        T3["Tutorial 3 - AWS"]
        i2[" "]
  end
 subgraph subGraph3["Módulo 4"]
        j3["Data de finalização sugerida: 07/11/2025"]
        R4["Roteiro 4 - OpenStack"]
        TE4["Teoria 4 - Redes"]
        T4["Tutorial 4 - AWS"]
  end
    n10 --> R1
    n11 --> TE1
    n12 --> T1
    i0 L_i0_subGraph1_0@--> subGraph1
    subGraph1 L_subGraph1_i0_0@--> i0
    i1 L_i1_subGraph2_0@--> subGraph2
    subGraph2 L_subGraph2_i1_0@--> i1
    i2 L_i2_subGraph3_0@--> subGraph3
    subGraph3 L_subGraph3_i2_0@--> i2
    R1 -- 100% --> n1["🔒"]
    TE1 -- 70% --> n1
    T1 -- 50% --> n1
    n1 --> EX1[["Exam 1 - QUIZ 1"]]
    EX1 --> n2["🔒"]
    R2 -- 100% --> n2
    TE2 -- 70% --> n2
    T2 -- 50% --> n2
    n2 --> EX2[["Exam 2 - QUIZ 2"]]
    EX2 --> n3["🔒"]
    R3 -- 100%--> n3
    TE3 --70%--> n3
    T3 --50%--> n3
    n3 --> EX3[["Exam 3 - QUIZ 3"]]
    EX3 --> n4["🔒"]
    R4 --100%--> n4
    TE4 -- 70%--> n4
    T4 -- 50%--> n4
    n4 --> EX4[["Exam 4 - QUIZ 4"]]

    n10@{ img: "https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3eo4lq29ys7npyze8vol.jpg", h: 120, w: 250, pos: "c"} 
    n11@{ img: "https://researchpark.illinois.edu/wp-content/uploads/2024/06/3x2-Logo-_PrairieLearn.png", h: 120, w: 200, pos: "b"}
    n12@{ img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRGriEor-iHn4958eGtsWa8qpmxleCqEultLQ&s", h: 120, w: 200, pos: "a"}
     
    
     R1:::modulo1
     TE1:::modulo1
     T1:::modulo1
     i0:::invisible
     R2:::modulo2
     TE2:::modulo2
     T2:::modulo2
     i1:::invisible
     R3:::modulo3
     TE3:::modulo3
     T3:::modulo3
     i2:::invisible
     R4:::modulo4
     TE4:::modulo4
     T4:::modulo4
     n1:::forkjoin
     EX1:::exam
     n2:::forkjoin
     EX2:::exam
     n3:::forkjoin
     EX3:::exam
     n4:::forkjoin
     EX4:::exam
     
  classDef modulo1 fill:#DDEBF7,stroke:#4682B4,stroke-width:2px,color:#000000
  classDef modulo2 fill:#E2EFDA,stroke:#006400,stroke-width:2px,color:#000000
  classDef modulo3 fill:#FFF2CC,stroke:#DAA520,stroke-width:2px,color:#000000
  classDef modulo4 fill:#FCE4D6,stroke:#B22222,stroke-width:2px,color:#000000
  classDef exam fill:#FFEFD5,stroke:#CD853F,stroke-width:2px,color:#000000
  classDef forkjoin fill:#DDFFFF,stroke:#696969,stroke-width:2px,color:#000000
    L_i0_subGraph1_0@{ animation: slow } 
    L_subGraph1_i0_0@{ animation: slow } 
    L_i1_subGraph2_0@{ animation: slow } 
    L_subGraph2_i1_0@{ animation: slow } 
    L_i2_subGraph3_0@{ animation: slow } 
    L_subGraph3_i2_0@{ animation: slow }

```
</div>


A disciplina de Computação em Nuvem do Insper adota uma estrutura baseada no modelo de **Mastery Learning**, com ênfase em progressão por competência. O objetivo é garantir que cada aluno avance somente após demonstrar o domínio considerado básico nos conceitos e habilidades de cada etapa, mantendo um ritmo de aprendizado consistente.

O curso está organizado em quatro módulos sequenciais, cada um com foco em diferentes aspectos da computação em nuvem. Cada módulo é composto por três trilhas paralelas de atividades: Roteiros Práticos de Infraestrutura, Tutoriais sobre Serviços em Nuvem Pública e Teoria sobre Protocolos e Arquiteturas de Rede.

!!! info "Trilhas Parelelas"

    * Roteiros (On-Premise / OpenStack):
    Nesta trilha, os alunos realizam atividades práticas que envolvem a construção de uma nuvem privada utilizando a stack da Canonical: MAAS, Juju e OpenStack. O foco é proporcionar ao aluno um entendimento técnico sobre a infraestrutura que suporta ambientes de nuvem.

    * Tutoriais (AWS / Cloud Pública):
    Aqui os alunos interagem com a plataforma AWS, realizando tarefas como configuração de redes virtuais (VPC), gestão de usuários (IAM), criação de instâncias (EC2), funções serverless (Lambda) e uso de serviços como S3 e bancos de dados gerenciados.

    * Teoria (Redes e Protocolos):
    Baseada no livro de Kurose, esta trilha traz atividades teóricas na plataforma PrairieLearn, com questões autoavaliativas, variações dinâmicas e feedback imediato. Os alunos podem repetir as atividades até alcançarem o domínio de cada conceito.

O progresso do curso só ocorre quando o aluno completa as três trilhas e faz um QUIZ (Exam) na plataforma PrairieLearn correspondente ao módulo. Esses Quiz funcionam como barreiras de progressão, seguindo o modelo **Assessment Locked**, onde a aprovação é condição necessária para liberar o acesso ao próximo QUIZ, porém o aluno pode percorrer as atividades Tutoriais e Teoria como achar mais proveitoso em seus estudos de modo a facilitar como cada individuo trata a disciplina.

# ✅ Regras para liberar o **Exam (Quiz) de cada módulo**

Para ter acesso ao **Exam** do módulo, você precisa cumprir **todas as condições abaixo**:

1. **Roteiro do módulo (100%)**  

   - Concluir o roteiro completo do módulo.  
   - Entregar todas as **evidências (prints)** solicitadas.  

2. **Teoria (70%)**  

   - Realizar pelo menos **70% dos exercícios no PrairieLearn** relacionados à teoria de redes.  

3. **Tutoriais AWS (50%)**  

   - Cada módulo contém **2 laboratórios práticos de AWS**.  
   - Você precisa completar **pelo menos 1 dos 2 (50%)** para desbloquear o Exam.  
---

📌 **Importante:** o **Exam do módulo só será liberado** quando **todas as condições acima forem atendidas**.


Além das trilhas e exames, os alunos desenvolvem um Projeto Final, iniciado desde o primeir mês e conduzido de forma paralela ao restante da disciplina. Este projeto é dividido em duas fases:

- Construção manual de uma infraestrutura escalável, aplicando os conceitos práticos adquiridos.

- Automação da infraestrutura com CI/CD, utilizando Terraform para provisionamento e pipelines de deploy.

Essa abordagem permite ao aluno vivenciar uma experiência educacional que integra teoria, prática e aplicação de conceitos de infraestrutura e desenvolvimento em nuvem de forma progressiva, com acompanhamento e checkpoints claros de aprendizado.

Ao final da disciplina, os alunos terão desenvolvido não apenas competências técnicas, mas também habilidades de organização de aprendizado, autogerenciamento e capacidade de demonstrar conhecimentos de forma prática da área de computação em nuvem.

## Critérios de Avaliação da Disciplina de Computação em Nuvem
A avaliação da disciplina é composta por duas partes principais: **Nota Individual** e **Nota em Grupo**, cada uma representando 50% da nota final.

!!! warning "Atenção"
    Nota Individual (45% da nota final):

    Esta nota será calculada com base na média dos quatro Quiz (Exams) realizadas ao longo do semestre.

    **Critério de Barreira**: a participação no Quiz 4 é **obrigatória**. O aluno que não fizer o último Quiz estará automaticamente reprovado, independentemente do desempenho nos anteriores.

    Nota Individual (5% da nota final):
    Desempenho nos exercícios teóricos: O aluno deve atingir 100% de acerto em todas as atividades teóricas dos quatro módulos.    

!!! warning "Atenção"
    Nota em Grupo (45% da nota final):

    Corresponde ao desempenho no Projeto Final, que será desenvolvido em equipe.

    **Critério de barreira**: a entrega do Projeto Final é obrigatória. A não entrega do projeto resultará em reprovação na disciplina, independentemente das demais notas.

    Nota em Grupo (5% da nota final):
    Conclusão dos tutoriais práticos: O aluno deve concluir todos os tutoriais práticos dos quatro módulos (total de 8 tutoriais), isso dará um acrescimo **individual** a sua nota relacionada ao projeto. 


| Item | Peso na Nota Final | Observações |
|---|---|---|
| **Média dos Quizes Individuais** | **45%** | Média dos 4 Quiz. O **Quiz 4 é obrigatório**: ausência resulta em reprovação independente das demais notas. |
| **Projeto Final (Trabalho em Grupo)** | **45%** | Entrega obrigatória. **A não entrega reprova automaticamente o aluno**. |
|   **Exercícios Teóricos (100%)** | **5%** | Aluno que atingir **100% em todos os exercícios teóricos dos 4 módulos**. |
|  **Conclusão de Todos os Tutoriais** | **5%** | Aluno que concluir **todos os 8 tutoriais práticos dos 4 módulos**. |


## Datas Limite para os Exames
Como parte da estratégia de progressão por domínio adotada pela disciplina, cada aluno pode realizar os Quizzes no momento que se sentir preparado e tiver passado pelos pontos de controle. No entanto, para garantir o ritmo adequado de avanço e evitar atrasos que prejudiquem o andamento geral do aluno, foram estabelecidas datas limite para os Exames "1 e 2" e "3 e 4" e para o projeto final:

Exam 1 e 2 – QUIZ: devem ser realizados até o dia 24/09/2025.

Exam 3 e 4 – QUIZ: devem ser realizados até o dia 26/11/2025.

Projeto Final: deve ser realizado até o dia 26/11/2025.

!!! danger "IMPORTANTE !!!  -->  PRAZOS"
    **TODAS AS ENTREGAS SE ENCERRAM NO DIA 26/11/2025 ÀS 12:00(meio dia), NENHUMA ENTREGA PODE SER FEITA APÓS ESTA DATA**

    Após a data 24/09/2025, o sistema ainda permitirá a realização dos Exam 1 e 2, até a data **FINAL - 26/11/2025**, porém o aluno não poderá obter nota superior a 5,0 nessas avaliações.
    Ou seja, a nota será limitada a 5 caso o Exam seja entregue após o prazo 24/09/2025 estipulado, independentemente da nota do Quiz e não será aceito após a data Final 26/11/2025.
    No caso do projeto final, não existe possibilidade de entrega atrasada, este projeto não será adiado!!!

    Essa medida busca estimular o comprometimento contínuo ao longo do semestre e a responsabilidade com os marcos de entrega, fundamentais para o sucesso no modelo de aprendizagem adotado.


## Observações Gerais

- A disciplina adota o modelo de progressão por domínio (Mastery Learning).
- O Projeto Final e o QUIZ 4 são componentes de critério de barreira.