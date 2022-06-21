# Nautilus
Aplicação com backend e frontend em JavaScript e banco de dados MySQL para treino de CRUD

## Sobre o projeto:
O Nautilus foi desenvolvido como um exercício para o treino de CRUD em JavaScript, utilizando o modelo de desenvolvimento com frontend, backend e banco de dados separados.
O projeto aqui apresentado é apenas um exercício e disponibilizo ele aqui para quem tiver interesse em utiliza-lo para treinar aplicando seus conhecimentos em JavaScript, Node e MySQL, esse projeto já esta funcional e dockeirizado para rodar utiizando bind mount, ele não esta pronto e tem possibilidades de estudo desde procurar e corrigir bugs, até ampliar e alterar o projeto, deixarei algumas sugestões neste readme.

### O que o Nautilos se propõe a fazer?
A premissa do sistema é cadastrar estaleiros, modelos de embarcações, embarcações, clubes, marinas, marinheiros e proprietários, fazendo a relação entre os dados, como qual é o proprietário da embarcação, a qual clube ou marina esta vinculada, qual o marinheiro responsável e qual seu modelo e estaleiro de fabricação.
A aplicação tem um sistema de login com senha salva utilizando hash jwt e token de validação de login. No entanto, o sistema não diferencia usuários e todos que criarem uma conta acessarão e editarão os mesmos dados.

![Tela Principal](/telaprincipal.png)
tela principal

![Tela de barcos](/telabarcos.png)
tela de visualização dos barcos cadastrados

![Tela Cadastro](/cadastro.png)
tela de cadastro de estaleiros

### Como esta organizado o projeto?
O projeto esta divido em 4 repositórios, sendo este o elo de ligação entre eles através do uso de submodule do git, você pode acessa-los pelos links:
* Repositório Principal: https://github.com/bolatechproducoes/nautilus
* Repositório do Banco de Dados: https://github.com/bolatechproducoes/mySQLNaval
* Repositório do Backend: https://github.com/bolatechproducoes/backendNaval
* Repositório do Frontend: https://github.com/bolatechproducoes/frontendNaval

### Como baixar e rodar o projeto?
**É necessário ter o Git, o Docker e o MySQL Workbench instalados no seu pc para rodar esse projeto**
1. Crie uma pasta para o projeto e acesse ela pelo terminal.
2. Execute o comando: git clone https://github.com/bolatechproducoes/nautilus.git .
3. Execute o comando: git clone https://github.com/bolatechproducoes/mySQLNaval.git mysql
4. Execute o comando: git clone https://github.com/bolatechproducoes/backendNaval.git Backend
5. Execute o comando: git clone https://github.com/bolatechproducoes/frontendNaval.git Frontend
6. Acesse a pasta Backend pelo VsCode e crie um arquivo .env com as seguintes configurações:
```env
DATABASE=dbnaval
DATABASE_HOST=192.168.0.17    ===> Trocar pelo ip do seu computador na rede 
DATABASE_PORT=3306
DATABASE_USERNAME=root
DATABASE_PASSWORD=278315

TOKEN_SECRET=FGJVGvvjvgvkHVJVJV67546474674hvuHMVJHV
TOKEN_EXPIRATION=7d

APP_URL=http://localhost:3001
APP_PORT=3001
```
7. Acesse a pasta principal do projeto com o VsCode e altere o arquivo docker-compose.yaml mudando o endereço para o do seu computador como no exemplo abaixo:
```yaml
version: '3.3'

services:
  db:
    build: ./mysql/
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 278315
      MYSQL_DATABASE: dbnaval
    ports:
      - "3306:3306"
    networks:
      - dockercompose

  backend:
    depends_on:
      - db
    build: ./Backend/
    ports:
      - "3001:3001"
    restart: always
    volumes:
      - COLOCAR-AQUI-O-ENDEREÇO-DA-PASTA-BACKEND-NO-SEU-PC-AQUI:/dist
    networks:
      - dockercompose
  frontend:
    depends_on:
      - backend
    build: ./Frontend/
    ports:
      - "3000:3000"
    restart: always
    volumes:
      - COLOCAR-AQUI-O-ENDEREÇO-DA-PASTA-FRONTEND-NO-SEU-PC-AQUI:/dist
    networks:
      - dockercompose
networks:
  dockercompose:
volumes:
  db_data: {}
```
Você pode encontrar o endereço das pastas no seu computador abrindo o projeto com o VsCode e clicando com o botão da direita do mouse em cima da pasta e selecionando a opção "Copiar o Caminho" como na imagem abaixo:
![caminho do arquivo](/caminho-do-arquivo.png)
Obs. no Windows as barras são invertidas, pode deixar como esta que irá funcionar

Obs.2 no linux o Backend e Frontend funcionaram com bind mount com as alterações aplicadas no código sendo aplicadas no container rodando, no windows você tera que desligar (down) e religar (up) o docker compose para as alterações serem aplicadas

8. Vá na pasta do projeto pelo terminal e execute o comando: docker-compose up
9. Espere até o Docker criar as imagens e subir os containers e a aplicação estará rodando em http://localhost:3000, mas ainda será necessário configurar o banco de dados para que a aplicação funcione.
10. Rode o MySQL Workbench e acesse o banco de dados que estará rodando em http://localhost:3000, utilize a senha 278315 para acessar o usuario root

![banco de dados](/bdworkbench.png)
- Coloque a senha 278315 e aperte ok

![senha](/senhabd.png)

11. Crie um banco de dados chamado bdnaval clicando com o botão da direita do mouse na aba lateral esquerda e escolhendo a opção create schema.
12. Configure o banco de dados como na imagem abaixo

![config db](/configdb.png)

Clique no botão aplicar na primeira tela e apply na segunda tela

![config db2](/configdb2.png)

13. Abra a pasta backend no terminal e digite o comando: npx sequelize db:migrate
14. Volte no terminal que você deixou rodando o docker-compose up e pare o processo apertando ctrl+c ou caso tenha fechado o terminal abra uma nova janela do terminal na pasta do projeto e execute o comando: docker-compose down
15. Na pasta do projeto execute o comando docker-compose up e pronto, a aplicação estará rodando, o frontend na porta 3000, o backend na porta 3001 e o banco de dados na porta 3306, você também pode dar o build do container do banco de dados, rodar só ele e rodar o backend pelo VsCode com o comando npm run dev no terminal e o frontend com o comando npm start.

### Como foi pensado o banco de dados e as tabelas?
As tabelas e sua relações estão descritas na imagem abaixo:

![banco de dados](/tabelas.jpg)

Na pasta "planilhas" deste projeto tem um .xls com todos seus campos e atributos

As tabelas e campos são criados atraves de migrations, as quais você pode acessar em Backend/src/database/migrations e o ORM utilizado na aplicação é Sequelize

### Como foi pensada a estrutura de pastas do projeto?
A estrutura de pastas foi feita com base no último projeto em JavaScript do Curso de TypeScript e JavaScript do Professor Luiz Otávio Miranda na Udemy. Esse projeto surgiu como um autodesafio de aplicação dos conhecimentos adquiridos durante o curso.

### Quais frameworks e tecnologias foram utilizadas neste projeto?
Neste projeto foi utilizado o ambiente Node com o instalador de pacotes npm, o banco de dados é o MySQL sendo utilizado o Sequelize como ORM para a comunicação com o backend. As rotas do backend foram construídas utilizando o Express, a parte de criptografia e segurança foi configurada com bcryptjs, cors, dotenv, helmet, e jsonwebtoken e para poder fazer o upload de imagens o multer. Para construir o frontend o framework utilizado foi o React, utilizando o axios para a comunicação com o backend, o Redux e o Saga para controlar os estados globais e as ações,o Toastify para gerar mensagens instantâneas, o Styled-component para criação de componentes entre outras tecnologias, como linters foram utilizados o eslint e o prettier.

### Este projeto esta pronto?
Não, e isto é proposital, este é um projeto de treino, consegui atingir o objetivo que me atribui com ele e deixo agora para quem quiser treinar seus conhecimentos em JavaScript, segue uma lista de correção de bug e features que podem ser implementadas a partir deste código, se você está fazendo o curso do Otávio Miranda na Udemy e já terminou as sessões sobre JavaScript conseguirá sem problemas rodar e implentar este código.

### O que tem para fazer/treinar neste projeto?
* Fazer a verificação da tipagem de dado dos telefones, no backend e frontend.
* Fazer o responsivo do Frontend, ele foi desenvolvido somente para 1080x1920.
* Acrescentar foto ao usuário e exibir o avatar no header.
* Criar campo de usuario nas tabelas e um middleware de verificação de usuário nas consultas para que cada usuário acesse somente seus dados.
* Modificar e alterar o frontend, fique a vontade, seja criativo!
* Criar tabelas de regras de usuários, obrigar o usuario a escolher um perfil (proprietario, marinheiro, funcionário de clube ou marina, ou funcionário de estaleiro. Sendo que proprietários só podem acessar suas embarcaçãos, podem escolher um clube e acessar seus marinheiros, pode acessar também o estaleiro que fabricou sua embracação. Marinheiros só podem acessar as embarcações que foram designados e funcionários de clubes, marinas ou estaleiros só podem acessar as informações respectivas ao seu negócio e as embarcações vinculadas a eles.
* Criar funções de pesquisa utilizando expressões regulares.
* Aprimorar o funcionamento das caixas de seleção com valores vindos de tabelas.
* Implementar serviço de envios de e-mail.

Essas são apenas algumas idéias, fiquem a vontade para clonar, fazer forks e se quiserem pull requests, divirtam-se aplicando JavaScript neste projeto!
