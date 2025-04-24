# Administrando a Instância

---

![51J65TYOZs.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/51J65TYOZs.png)

Após criar uma instância, ela será listada na pagina inicial do lightsail, contendo nela um resumo de suas operações:

![chrome_C3TjibiYOA.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_C3TjibiYOA.png)

- A: Imagem do blueprint selecionado para a Instância
- B: Nome da Instância
- C: Atalhos para rodar o CLI da instância e acessar o menu de opções da instância

- D: Hardware da instância
- E: Estado atual da instância
- F: Dados de Rede da Instância(IPv4 e Ipv6)
- G: Região e Zona da Instância

Vamos agora começar a administrar nossa instância, para isso, vá nas opções da Instância e clique em **Manage**. No topo da página, temos os mesmos dados da página inicial com maiores detalhes (**A**), e logo abaixo as abas para administração da Instância selecionada (**B**).

![chrome_xjEAnRiZTx.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_xjEAnRiZTx.png)

## Conexão

---

Aqui temos de forma detalhada as configurações de conexão SSH para a instância selecionada, podendo realizar a conexão via o CLI no web browser da AWS, e No fim da aba teremos um guia rápido das informações necessárias para realizar a conexão CLI via um browser próprio (Linux Bash, Windows Powershell, etc.):

![Conexão direta via WebBrowser](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_lTiYvJ1br5.png)

Conexão direta via WebBrowser

![Informações para acesso SSH](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_0cgV5V7Ovi.png)

Informações para acesso SSH

- A: IPv4 e IPv6 da sua instância
- B: Nome de usuário da instância criada
- C: Par de Chaves SSH da instância*
    
    

***A Opção de Download do Par de Chaves SSH só existe quando estamos utilizando a chave padrão da Região. Caso você utilize um Par de Chaves Privado, esta opção de download não estará disponível, então guarde suas chaves privadas ao criar as instâncias, e faça isso de forma SEGURA.**

![Instância utilizando um Par de Chaves privado](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_CE5t6Z6zEb.png)

Instância utilizando um Par de Chaves privado

```bash
ssh -i **/path/to/private-key.pem** **username**@**public-ip-address**
```

## Snapshots

---

Como explicado durante a criação da Instância, **Snapshots** são backups da sua instância que podem ser utilizadas caso você tenha um problema. O Lightsail nos dá a opção de criar um Snapshot manualmente aqui nesta aba, que irá criar o backup do momento atual da instância.

![chrome_tsoX9nuDhy.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_tsoX9nuDhy.png)

Ao criar um Snapshot Manual, basta definir um nome para este backup e clicar em **Create**, e seu snapshot será salvo.

Podemos também configurar e editar o Snapshot Automático da mesma. Snapshots Automáticos são realizados diariamente em um horário estabelecido por você, e a AWS armazenará os 7 snapshots mais recentes desta função.

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image.png)

## Armazenamento

---

Quando criamos uma instância, definimos um disco de armazenamento para uso da mesma ao selecionar o plano de pagamento (A). Caso seja necessário aumentar este espaço, podemos alugar discos de armazenamento extras e anexa-los a nossa instância para uso (B).

![chrome_5EIVdCsPGq.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_5EIVdCsPGq.png)

### Criando um novo disco

---

Discos de Armazenamento são separados por Região e Zona para uso, logo caso você precise anexar um novo disco a uma instância, garanta que está criando na mesma Região (**A**).

![chrome_Q7vFvsrFou.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_Q7vFvsrFou.png)

Após ajustar a Região, selecione o armazenamento que seu disco terá dentro das opções. Você pode também utilizar um valor customizado de armazenamento caso deseje, e o preço do aluguel será ajustado de acordo (**B**).

Por fim, defina um nome para este disco de armazenamento, conforme sua preferência.

Tags são opcionais, porém podem ser utilizadas em discos para facilitar a administração das suas instâncias.

No fim da Página, teremos um resumo do valor do aluguel do disco novo, e logo abaixo o botão para finalizar a criação do mesmo.

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%201.png)

### Anexando um novo disco na Instância

---

Assim que criamos um novo disco de armazenamento, o Lightsail irá nos enviar para a página de administração do mesmo, onde ja podemos anexa-lo a uma instância criada.

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%202.png)

Ao selecionar uma instância, teremos um resumo da mesma sendo exibido nesta página, junto com o path do disco dentro dela*

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%203.png)

***A partir deste momento, seu disco será reconhecido pela instância, porém você ainda deverá formatar e montá-lo dentro da instância para uso.**

Alternativamente, podemos selecionar discos já criados dentro do Lightsail na aba de Armazenamento da Instância e anexá-lo na mesma (**A**).

![chrome_9PbvTfdkOu.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_9PbvTfdkOu.png)

![chrome_jP0t22RYGO.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_jP0t22RYGO.png)

Caso queira remover um disco da sua instância, podemos também fazer isso de dentro da aba de Armazenamento, basta encontrar o disco desejado na lista de discos anexados e clicar em **Detach***.

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%204.png)

***Para desanexar um disco, você deverá parar a execução da instância. Lembre de ativá-la novamente do fim do processo.**

### Snapshots de Discos

---

Da mesma forma da instância, você pode criar Snapshots manuais dos seus discos extras, podendo garantir backups importantes de dados.

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%205.png)

## Rede

---

Nesta aba iremos administrar todas as informações de rede, entrada e saída da nossa instância.

### Conexão IPv4

Aqui nós teremos todas nossas informações de rede IPv4 da nossa Instância.

![chrome_2LrWFHtr7c.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_2LrWFHtr7c.png)

- **A:** O IP público da nossa instância é utilizado para realizar todo acesso via a Internet, enquanto o IP privado será utilizado apenas por recursos dentro da sua conta da Lightsail na mesma Região definida.
    
    No exemplo acima, não temos um IP público, isto acontece pois a AWS apenas oferece IPs de forma Dinâmica para instâncias que estão ativas. Enquanto sua instância estiver ativa, você irá ter seu IP público exibido tanto nesta aba, quanto no resumo da instância:
    

![chrome_4Rf6uqD6cX.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_4Rf6uqD6cX.png)

Outro ponto importante, sempre que sua instância parar de executar, um novo IP público será dado a ela em uma próxima execução, o que pode trazer problemas para sua administração e uso. Para eliminar este problema, podemos atribuir um IP público e**stático** para sua Instância, para garantir que mesmo após uma pausa em sua execução, seu endereço IP permaneça o mesmo.

![chrome_CKWsf93Fvf.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_CKWsf93Fvf.png)

![image.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/image%206.png)

Basta definir um nome **único** para seu IP estático e clicar no botão **criar e anexar** para configurar o IP estático da sua Instância. Agora teremos o nosso novo endereço IP público estático exibido no resumo e na Aba de Redes da Instância. Notem que mesmo com a instância **parada**, o nosso IP estático está sendo exibido normalmente.

![chrome_fJzGIhS9jP.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_fJzGIhS9jP.png)

**Importante lembrar que IP estáticos são limitados na sua conta, e a AWS irá cobrar por IPs estáticos criados e não anexados a uma plataforma.**

### Firewall IPv4

---

Agora que configuramos nosso IP público, temos que definir nossas regras de entrada da Instância. Para isso, aqui temos diversas opções de regras ja pré-definidas para conexões HTTP, SSH, de banco de dados, entre outros, porém também podemos configurar uma regra customizada.

![chrome_IV1R5vBBba.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_IV1R5vBBba.png)

Numa regra customizada, temos que definir o **Protocolo** **de comunicação** que será utilizado (TCP ou UDP)(**A**), e as portas que serão utilizadas para a comunicação(**B**). 

Além disso, podemos Restringir o acesso desta regra apenas para um IP ou range de IPs específicos(**C**).

![chrome_WBugIM0k05.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_WBugIM0k05.png)

Após criar a regra, ela irá estar detalhada na lista do Firewall, e poderá ser editada ou removida dentro do mesmo Painel*.

![chrome_ktsq9bDOh5.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_ktsq9bDOh5.png)

***As portas de acesso 22(SSH) e 80(HTTP) são dadas por padrão na criação da instância.**

### Conexão IPv6

A conexão IPv6 segue o mesmo princípio da conexão IPv4, porém ela terá apenas um IPv6 público que será utilizado, e o mesmo não será afetado quando a instância for interrompida.

Como o uso do IPv6 atualmente é limitado, caso você não for utilizar o acesso IPv6, é recomendado desabilitar está função da sua instância. Caso futuramente você mude de ideia, basta reabilita-la neste painel, e um novo IPv6 será atribuido à sua instância.

![chrome_COwr2uJv2x.png](Administrando%20a%20Insta%CC%82ncia%207b02b0ddc4aa42d9b879ae7ce5f1e2a9/chrome_COwr2uJv2x.png)