# Criando Uma Instância

Assim que acessar a área do Lightsail, você já é levado para a criação de uma nova instância:

![chrome_TKkRGxQdl7.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_TKkRGxQdl7.png)

Vamos olhar para cada detalhe da Criação da nossa nova instância:

## Região e Zona

O Lightsail irá selecionar automaticamente a região e zona de acordo com o seu acesso padrão da AWS, porém você pode modificar para qualquer outra caso queira. Cada região possui uma quantidade fixas de zonas onde podemos alocar nossas instâncias.

![chrome_JiDg4xMlQR.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_JiDg4xMlQR.png)

![chrome_HTl7k2pyKE.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_HTl7k2pyKE.png)

## Selecionando a imagem da sua instância

O Lightsail oferece diversas imagens prontas para serem utilizadas de acordo com as necessidades do seu projeto, em duas versões: **OS** e **APPS + OS**. Se você, por exemplo, vai lançar um webapp criado em Django, você ja pode selecionar a opção **DJANGO** da lista e sua instância ja virá com um OS contendo toda a infraestrutura dele já pronta para uso, precisando apenas adicionar seu projeto na mesma.

![Untitled](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/Untitled.png)

Você também pode também instalar apenas um Sistema Operacional na sua instância, tendo ela limpa e pronta para receber as customizações necessárias para rodar seu projeto.

![chrome_XsNQQOPjwA.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_XsNQQOPjwA.png)

## Campos Opcionais

### Script

Caso você queria inserir um script customizado para a criação da sua instância, basta inseri-lo nesta area e o Lightsail irá executá-lo ao cria-la

![chrome_oq6J348iah.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_oq6J348iah.png)

### Par de Chaves SSH

Embora opcional, esta é uma parte importante da criação de sua instância. Para acessar sua instância via SSH, você deverá ter um par de chaves criado e armazenado de forma segura, pois o download do mesmo só pode ser feito uma vez. Caso você venha a perder este par de chaves, um novo terá de ser criado em seu lugar. Uma chave com nome *default* é dado a sua instância automaticamente, porém é recomendado dar um nome mais específico ao uso dela para não confundir e ter uma melhor administração dos seus pares de chaves.

![chrome_dvPFAak73b.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_dvPFAak73b.png)

![chrome_SYNWArQTgt.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_SYNWArQTgt.png)

### Snapshots Automáticos

*Snapshots* são backups da sua instância e discos de armazenamento anexados a ela, criados e armazenado pela AWS. Nesta etapa podemos definir a criação de um snapshot diário para ela, o que pode ser de grande ajude caso nossa instância tenha um erro ou falhe futuramente. Para programar o snapshot diário apenas selecione o horário e fuso desejado para tal.

![Untitled](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/Untitled%201.png)

## Plano da Instância

Após realizar todas as customizações da sua instância, precisamos nos atentar ao plano de pagamento dela, que irá definir toda a arquitetura por trás dela. A AWS costuma oferecer os planos mais básicos de forma gratuita por alguns meses, o que é ótimo para testes e projetos de pequena duração. Seleciona a que for mais apropriado ao seu projeto

![Untitled](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/Untitled%202.png)

## Identificação da Instância

Por fim, dê um nome apropriado para sua instância, e, caso necessário, adicione tags que possam facilitar no controle e manutenção delas dentro da AWS futuramente. Para concluir, basta clicar em **criar instância**.

![chrome_NJCAetHA8A.png](Criando%20Uma%20Insta%CC%82ncia%20f5b1feb21a664d8890349bdeedb82930/chrome_NJCAetHA8A.png)