# Boas vindas ao repositório do projeto Cookmaster!

## Desenvolvimento

Foi desenvolvido todas as camadas da aplicação (Models, Service e Controllers). Através dessa aplicação, será possível realizar as operações básicas que se pode fazer em um determinado banco de dados: Criação, Leitura, Atualização e Exclusão (ou `CRUD`, para as pessoas mais íntimas 😜).

Para realizar qualquer tipo de alteração no banco de dados (como cadastro, edição ou exclusão de receitas) será necessário autenticar-se. Além disso, as pessoas usuárias devem poder ser clientes ou administradores. Pessoas clientes apenas poderão disparar ações nas receitas que ele mesmo criou. Já uma pessoa administradora pode disparar qualquer ação em qualquer receita.

A autenticação foi feita via `JWT`.

É possível adicionar uma imagem à uma receita, utilizando o upload de arquivos fornecido pelo `multer`.



### 1 - Endpoint para o cadastro de usuários

- Rota (`/users`).

- No banco um usuário precisa ter os campos Email, Senha, Nome e Role.

- Para criar um usuário através da API, todos os campos são obrigatórios, com exceção do Role.

- O campo Email é único.

- Usuários criados através desse endpoint não são administradores.

- O body da requisição deve conter o seguinte formato:

  ```json
  {
    "name": "string",
    "email": "string",
    "password": "string"
  }
  ```

Se o usuário for cadastrado com sucesso o resultado retornado deverá ser conforme exibido abaixo, com um status http `201`:

![Usuário Cadastrado](./public/usuariocriadocomsucesso.png)

### 2 - Endpoint para o login de usuários

- Rota (`/login`).

- A rota deve receber os campos Email e Senha e esses campos são validados no banco de dados.

- Um token `JWT` é gerado e retornado caso haja sucesso no login.

- O body da requisição deve conter o seguinte formato:

  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
Se foi feito login com sucesso o resultado retornado deverá ser conforme exibido abaixo, com um status http `200`:

![Login com Sucesso](./public/logincomsucesso.png)

### 3 - Endpoint para o cadastro de receitas

- Rota (`/recipes`).

- A receita só pode ser criada caso o usuário esteja logado e o token `JWT` validado.

- No banco, a receita tem os campos Nome, Ingredientes, Modo de preparo, URL da imagem e Id do Autor.

- Nome, ingredientes e modo de preparo devem ser recebidos no corpo da requisição, com o seguinte formato:

  ```json
  {
    "name": "string",
    "ingredients": "string",
    "preparation": "string"
  }
  ```

- O campo dos ingredientes pode ser um campo de texto aberto.

- O campo ID do autor, é preenchido automaticamente com o ID do usuário logado, que é extraído do token JWT.

O resultado retornado para cadastrar a receita com sucesso deverá ser conforme exibido abaixo, com um status http `201`:

![Receita com Sucesso](./public/receitacomsucesso.png)

### 4 - Endpoint para a listagem de receitas

- Rota (`/recipes`).

- A rota pode ser acessada por usuários logados ou não

O resultado retornado para listar receitas com sucesso deverá ser conforme exibido abaixo, com um status http `200`:

![Receita com Sucesso](./public/listarreceitas.png)

### 5 - Endpoint para visualizar uma receita específica

- Rota (`/recipes/:id`).

- A rota pode ser acessada por usuários logados ou não

O resultado retornado para listar uma receita com sucesso deverá ser conforme exibido abaixo, com um status http `200`:

![Listar uma Receita](./public/listarumareceita.png)

### 6 - Endpoint para a edição de uma receita

- Rota (`/recipes/:id`).

- A receita só pode ser atualizada caso o usuário esteja logado e o token `JWT` validado.

- A receita só pode ser atualizada caso pertença ao usuário logado, ou caso esse usuário seja um admin.

- O corpo da requisição deve receber o seguinte formato:

  ```json
  {
    "name": "string",
    "ingredients": "string",
    "preparation": "string"
  }
  ```

O resultado retornado para editar uma receita com sucesso deverá ser conforme exibido abaixo, com um status http `200`:

![Editar uma Receita](./public/editarcomsucesso.png)

### 7 - Endpoint para a exclusão de uma receita

- Rota (`/recipes/:id`).

- A receita só pode ser excluída caso o usuário esteja logado e o token `JWT` validado.

- A receita só pode ser excluída caso pertença ao usuário logado, ou caso o usuário logado seja um admin.

O resultado retornado para excluir uma receita com sucesso deverá ser conforme exibido abaixo, com um status http `204`:

![Excluir uma Receita](./public/excluircomsucesso.png)

### 8 - Endpoint para a adição de uma imagem a uma receita

- Rota (`/recipes/:id/image/`).

- A imagem é lida do campo `image`.

- O endpoint aceita requisições no formato `multipart/form-data`.

- A receita só pode ser atualizada caso o usuário esteja logado e o token `JWT` validado.

- A receita só pode ser atualizada caso pertença ao usuário logado ou caso o usuário logado seja admin.

- A URL completa para acessar a imagem através da API é gravada no banco de dados, junto com os dados da receita.

O resultado retornado para adicionar uma foto na receita com sucesso deverá ser conforme exibido abaixo, com um status http `200`:

![Foto Autenticada](./public/fotocomsucesso.png)

### 9 - Endpoint para acessar a imagem de uma receita

- As imagens estão disponíveis através da rota `/images/<id-da-receita>.jpeg` na API.

O resultado retornado deverá ser do tipo imagem, com um status http `200`:

![Foto Autenticada](./public/imagemrecetornada.png)


