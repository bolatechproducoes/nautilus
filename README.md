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
