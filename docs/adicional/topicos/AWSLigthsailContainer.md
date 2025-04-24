# Container Service

---

Serviço de Containers é outra opção de deployment para suas aplicações dentro da AWS Lightsail. Esse sistema pode ser visto como um ambiente de computação que lhe permite rodar containers na infraestrutura da AWS, utilizando imagens que você cria na sua máquina local, ou imagens de um repositório online(como o docker hub) ou a Amazon ECR Public Gallery.

![amazon-lightsail-container-service-diagram.png](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/amazon-lightsail-container-service-diagram.png)

Para criar seu serviço de containers, devemos considerar dois parâmetros principais:

- **Potência:** Define a quantidade de memória e vCPUs de cada nódulo dentro do seu serviço. Esta potência está dividida dentro do Lightsail entre os modelos:
    
    
    - Nano (Na)
    - Medium (Md)
    
    - Micro (Mi)
    - Large (Lg)
    
    - Small (Sm)
    - XLarge (Xl)
- **Escala:** A quantidade de nódulos de computação que você deseja ter para rodar seus containers. Você pode dedicar até 20 nódulos para um serviço de container.

![image.png](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image.png)

Ao especificar a Escala do serviço para um número maior que 1, seu workload é copiado para todos os nódulos do seu serviço. 

Exemplo: Um serviço de Escala 3 com potência Nano terá três cópias do seu workload rodando em três recursos de computação, cada um com 512mb de RAM e 0.25 vCPU.

Após especificar os dois parâmetros, devemos especificar o deploy inicial dos containers. Você pode utilizar uma imagem exemplo da AWS, ou uma imagem customizada de outro serviço de container.

![image.png](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image%201.png)

![Utilizando uma imagem base com Nginx](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image%202.png)

Utilizando uma imagem base com Nginx

![Imagem de container customizado](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image%203.png)

Imagem de container customizado

Em Containers customizados, podemos definir chaves de ambiente e portas abertas para acesso do mesmo.

![image.png](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image%204.png)

Após concluir as definições da sua imagem dos containers, basta dar um nome ao seu serviço e concluir a criação. 

Lembrando que o custo do serviço será definido pela fórmula: **Potência*Escala**

![image.png](Container%20Service%20eea2bf6a0e1a4d63875a36f178265b14/image%205.png)