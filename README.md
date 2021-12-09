# DesafioBiblioteca

Desenvolva uma API, seguindo as boas práticas de desenvolvimento de APIS com as seguintes especificações:

1. A API deve ser um sistema de gestão de uma pequena biblioteca, onde os usuários devem ter um cadastro para visualizar, reservar e alugar livros do acervo.
1. Deve ser feita uma autenticação com base em roles, assim permitindo que a gestão do acervo seja feita somente por funcionários/administradores da biblioteca.
1. Todos os livros cadastrados devem ter um autor vinculado ao mesmo, não sendo permitido cadastrar um livro sem autor
1. O sistema deve permitir a busca de livros por autor, titulo, descrição e ano de publicação, todas sendo paginadas para melhor performance

## Endpoints

#### Os endpoints disponíveis devem seguir a seguinte especificação:

POST /login - Realiza o login no sistema  

PUT /reset_password - Realiza a troca de senha do usuário

**Author:**

POST /authors - Cadastrar um autor (somente funcionários/administradores cadastrados)  

PUT /authors  - Atualizar um autor (somente funcionários/administradores cadastrados)  

DELETE /authors  - Deletar um autor (somente funcionários/administradores cadastrados)  

GET /authors?Name=&Nationality=&Age=&page=&items=  - Buscar todos os autores (usuários logados)

GET /authors/{id} - Buscar um autor pelo id de cadastro (usuários logados)

**Books:**

POST /books - Cadastrar um livro (somente funcionários/administradores cadastrados)  

PUT /books  - Atualizar um livro (somente funcionários/administradores cadastrados)  

DELETE /books  - Deletar um livro (somente funcionários/administradores cadastrados)  

GET /books?Author=&Name=&releaseYear=&description=&page=&items=  - Buscar todos os livros (filtros vide item 3) (usuários logados)

GET /books/{id} - Buscar um livro pelo id de cadastro  (usuários logados)

**Users:**

POST /users - Cadastrar um usuário  

PUT /users  - Atualizar o cadastro de um usuário (somente usuário logado e funcionários/administradores cadastrados) 

GET /users?Name=&Birthdate=&Document=&page=&items= - Buscar todos os usuários (somente funcionários/administradores cadastrados)  

GET /users/{id} - Buscar o usuário pelo id de cadastro (somente funcionários/administradores cadastrados)  

GET /users - Buscar os dados do usuário que está atualmente logado no sistema (somente usuário logado)  

**Reservation:**

POST /reservations - Cadastrar uma reserva de livro (somente usuário logado)  

PUT  /reservations - Atualizar uma reserva de livro (somente usuário logado)  

GET  /reservations?startDate=&endDate=&author=&bookName=&page&items= - Buscar todas as reservas cadastradas (somente funcionários/administradores cadastrados)  

GET  /reservations - Buscar todas as reservas cadastradas para o usuário logado (somente usuário logado)  

POST /reservations/cancel - Cancelar uma reserva (somente usuário logado)  

POST /reservations/finalize/{id} - Finalizar uma reserva (somente usuário logado)  

**Withdraw:**

POST /withdraw - Cadastra uma retirarada de um ou mais livros (somente usuário logado)  

POST /withdraw/finalize/{id} - Finalizar uma reserva (somente usuário logado)  

GET  /withdraw?open=&startDate=&endDate=&author=&bookName=&page&items= - Buscar todo o histórico de retiradas de livros (somente funcionários/administradores cadastrados)  

GET  /withdraw - Buscar uma retirada que está em andamento para o usuário logado (somente usuário logado)  

#### Regras que devem ser cumpridas:

1. Todo autor deve ser cadastrado anteriormente ao cadastro dos livros do mesmo;
1. Um autor pode ser cadastrado e não possuir nenhum livro;
1. Todo livro cadastrado deve possuir um autor atrelado a ele;
1. Um livro deve ter uma quantidade limitada de cópias;
1. Caso haja uma tentativa de reserva de um livro que não tenha cópias disponíveis para a data desejada, deve ser informado ao usuário;
1. Pode se retirar um livro sem reservas, se existirem cópias disponíveis no momento, e a data do fim do aluguel não conflite com alguma reserva já cadastrada;
1. Uma reserva somente pode ser cancelada até um dia útil anterior a data da reserva;
1. O tempo mínimo para aluguel de um livro é de 5 dias corridos;
1. Um usuário pode realizar reservas e retirar vários livros ao mesmo tempo, porém se um deles estiver indisponível, nenhum deve ser retirado/reservado;
1. Use a API de CEP para preencher os dados de endereço do cliente na hora do cadastro, caso não seja encontrado um endereço para o CEP, informe um erro e indique o usuário a inserir o endereço manualmente no momento do cadastro;
