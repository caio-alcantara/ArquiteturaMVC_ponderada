# Caio de Alcantara Santos - Turma 11 Grupo 03


## Ponderada de programação semana 01 - Arquitetura MVC
&nbsp;&nbsp;&nbsp;&nbsp;Ponderada de programação da semana 01 do módulo 02. Desenvolver e apresentar uma proposta de arquitetura detalhada em esboço do padrão MVC (Model-View-Controller) para projeto Sails.js proposto para o módulo.

## Informações sobre o projeto

* Nome do Projeto: VTM - Voluntariado Transformador Massivo <br>
* Descrição: Uma plataforma Web que integre organizações sociais e voluntários em um só lugar. Permitindo que essas organizações possam encontrar pessoas disponíveis para trabalhos voluntários. <br>
* Arquitetura: MVC (Model-View-Controller)
* Ferramenta de Diagramação: <a href="https://app.diagrams.net/"> draw.io </a>

## Sobre o framework Sails.js
&nbsp;&nbsp;&nbsp;&nbsp;O framework utilizado para o backend da aplicação é o Sails,js, um framework já baseado na arquitetura MVC e que tem como base a ideia de desenvolver em semanas softwares que levariam meses para estares funcionais. Além disso, o Sails.js facilita em grande parte a integração com API's

## Funcionalidades propostas para a aplicação
&nbsp;&nbsp;&nbsp;&nbsp;Um usuário deve poder se cadastrar como voluntário na plataforma e possuir um perfil de voluntário ou organização. Então, ele poderá se mostrar disponível para trabalhos voluntários ou encontrar organizações que já estejam o oferecendo. Além disso, o voluntário pode, de maneira individual, ou representando uma organização, cadastrar alguma ação que ele esteja realizando. Por fim, o usuário terá um perfil que mostre suas estatísticas relacionadas a trabalho voluntário e a plataforma também contará com um contabilizador de todas as horas que foram trabalhadas por intermédio dela.
* Cadastro de usuário
* Se disponibilizar para trabalho voluntário
* Encontrar trabalhos voluntários disponíveis
* Cadastrar uma ação
* Perfil que mostre estatísticas
* Estatísticas gerais da plataforma

## Sobre o padrão de arquitetura MVC
&nbsp;&nbsp;&nbsp;&nbsp;O padrão MVC consiste em separar a aplicação em 3 camadas.
* A camada de Views: Páginas HTML. É aquilo com o que de fato o usuário interage
* Controllers: Responsável por intermediar as comunicações entre cliente e servidor. É aqui que se encontra a lógica de negócios da aplicação, o que o usuário pode ou não fazer, quais funcionalidades o site possui.
* Model: Responsável por se comunicar com o banco de dados da aplicação. O usuário não interage com essa camada do software.

<br>

## Arquitetura MVC do projeto proposto
<img src="MVC - Caio de Alcantara Santos.png">
<div align='center'> Fonte: <a href="https://drive.google.com/file/d/1kwGsNteJ-KwynH3I2WWWJB9TxPbww7Tk/view?usp=sharing"> Material produzido pelo autor (2024) </a> </div>

### Models:
&nbsp;&nbsp;&nbsp;&nbsp;Neste projeto, possuímos duas entidades (tabelas no banco de dados): usuários e ações cadastradas. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Para a tabela de usuários, os atributos considerados indispensáveis são: Id, nome, email, senha, CEP, idade, horas voluntariadas, ações criadas, ações em que trabalha. Essa tabela se refere a qualquer pessoa que utiliza a plataforma, seja um voluntário único ou uma organização. A ideia, na verdade, é que todos que se cadastrem na plataforma façam isso como voluntário. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Para a tabela de ações, as coisas ficam mais simples. Uma ação apenas possui um id como *primary key*, uma *foreign key* que aponta para o id de seu criador, o local de atuação, uma descrição, a quantidade de horas de trabalho e os usuários cadastrados nela.
&nbsp;&nbsp;&nbsp;&nbsp;No que se trata das relações entre as entidades, podemos dizer que é uma relação *many-to-many*, uma vez que um usuário pode estar em várias ações e uma ação pode ter vários usuários. 

### Views:
&nbsp;&nbsp;&nbsp;&nbsp; Para o projeto, até o momento pensamos em 5 telas:
* Landing Page: Captar a atenção do usuário e introduzí-lo à finalidade da plataforma
* Cadastro: Colher informações necessárias para cadastrar o usuário na plataforma e criar o seu perfil
* Homepage: Mostrar as oportunidades de trabalho disponíveis, os voluntários disponíveis e possibilitar o cadastro de novas ações.
* Perfil: Mostrar informações (nome, foto, bio) do usuário e estatísticas sobre o mesmo.
* Ação: Página de uma determinada ação, mostra sua descrição, o tempo de trabalho, imagens e a possibilidade de alguém se candidatar.

### Controllers:
&nbsp;&nbsp;&nbsp;&nbsp; Os controladores responsáveis por medias as interações do usuário na plataforma são os seguintes: <br>
* Para os usuários:
    * Cadastrar na plataforma - feito por meio do envio de um formulário
    * Se tornar disponível para trabalho - A partir de um botão toggle, que o torna visível para organizações em busca de voluntários
    * Candidatar em vaga - um botão para enviar seus dados para a organização
    * Cadastrar ação própria - um botão para enviar os dados da ação 
    * Cadastrar ação de organização - um botão para enviar os dados da ação + organização
    * Atualizar informações no perfil + alterar dados do perfil
    * Convidar membros para suas ações - um botão no perfil de outra pessoa para chamá-la para uma ação sua
* Para as ações:
    * Criar - criação de ações
    * Atualizar - atualização de parâmetros de uma ação
    * Procurar - procura por ações específicas

&nbsp;&nbsp;&nbsp;&nbsp;"View" é o nome que damos à camada de informações que aparece para o usuário. Sejam issos textos, imagens, botões, formulários, etc. Ao interagir com qualquer um desses elementos, o "Controller" é o responsável por colher o dado da interações e realizar alguma funcionalidade da plataforma. Por exemplo, ao preencher os dados do formulário de cadastro e clicar no botão de se cadastrar, o *controller* pega as informações que foram enviadas pelo usuário e as mandam para o banco de dados (Model), cadastrando, efetivamente, o usuário na plataforma. 

### Infraestrutura:
&nbsp;&nbsp;&nbsp;&nbsp;O projeto possui, até o momento, como componente de infraestrutura um banco de dados relacional gerenciado pelo sistema PostgreSQL, responsável por armazenar em entidades (tabelas) todos os dados necessários de usuários e cadastrados na plataforma. No padrão MVC, o banco de dados está presente da camada de Model, nunca podendo ser visível ou interagido pelo usuário. O Model será responsável por fazer consultas e alterar valores no banco de dados por meio de operações de CRUD (Create, Read, Update, Delete).

## Justificativa das escolhas:
### Implicações da Arquitetura:
&nbsp;&nbsp;&nbsp;&nbsp;A escolha da arquitetura MVC e do framework Sails.js (baseado em MVC) implica em uma separação de camadas de software muito explícita, o que facilita o entendimento do que cada parte do software faz, podendo fazer, por exemplo, a separação do que é visível para o usuário e o que é regra de negócio.<br>
&nbsp;&nbsp;&nbsp;Em relação a escalabilidade, a separação do software em camadas permite uma maior modularização e reaproveitamento de código, de forma que cada camada pode ser escalada individualmente.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Sobre a questão da manutenção, a arquitetura MVC, também por conta da modularidade citada anteriormente, permite que cada parte do código possa ser isolada e testada individualmente.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Por fim, no que se diz respeito a testabilidade, o MVC permite o desenvolvimento de testes unitários para cada camada do software, o que facilita a testagem da aplicação como um todo.

