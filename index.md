## NOFLASH - Documentation

Neste projeto será desenvolvido uma página web cujo objetivo permite na atualização rápida de artigos, postagens ou publicações entre utilizadores.

![noflash_logo](https://user-images.githubusercontent.com/72763555/145847448-df5d9ded-b330-405f-a468-cfd8b54b4230.jpeg)

```

Realizado por: Pedro Gomes & Diogo Rocha

Politécnico: Instituto Politécnico Cávado e do Ave

Curso: Desenvolvimento Web e Multimédia

Disciplina: Desenvolvimento Colaborativo de Sofware & Computação Distribuída
```


# Especificação da API


## Users

**Endpoint - HTTP Action - Business Operation**

/Users - GET - getAllUsers

/Users/{user_id} - GET - getUserId

/Users/{user_id} - PUT - updateUserId

/Users/{user_id} - DELETE - deleteUser

## Tests
```
test('Test #1 - Listar os Utilizadores', () => {
return request(app).get('/users')
  .set('authorization', bearer ${user.token})
  .then((res) => {
  expect(res.status).toBe(200);
  expect(res.body.length).toBeGreaterThan(0);
  });
});
                                      
test('Test #2 - Inserir Utilizadores', () => {
return request(app).post('/users')
  .set('authorization', bearer ${user.token})
  .send({ name: 'Pedro Gomes', password: 'admin', email: mail })
  .then((res) => {
  expect(res.status).toBe(201);
  expect(res.body.name).toBe('Pedro Gomes');
  });
});
                                      
test('Test #3 - Inserir utilizadores sem nome', () => {
return request(app).post('/users')
  .set('authorization', bearer ${user.token})
  .send({ password: 'admin', email: mail })
  .then((res) => {
  expect(res.status).toBe(400);
  expect(res.body.error).toBe('Nome é um atributo obrigatório');
  });
 });
                                      
test('Test #4 - Inserir utilizador sem email', async () => {
const result = await request(app).post('/users')
  .set('authorization', bearer ${user.token})
  .send({ name: 'Pedro Gomes', password: 'admin' });
  expect(result.status).toBe(400);
  expect(result.body.error).toBe('O email é um atributo obrigatório');
  });
                                      
test('Test #5 - Inserir utilizador sem password', (done) => {
request(app).post('/users')
  .set('authorization', bearer ${user.token})
  .send({ name: 'Pedro Gomes', email: mail })
  .then((res) => {
  expect(res.status).toBe(400);
  expect(res.body.error).toBe('A palavra-passe é um atributo obrigatório');
  done();
  });
 });
                                      
test('Test #6 - Inserir utilizador com email duplicado', () => {
request(app).post('/users')
  .set('authorization', bearer ${user.token})
  .send({ name: 'Pedro Gomes', password: 'admin', email: mail })
  .then((res) => {
  expect(res.status).toBe(400);
  expect(res.body.error).toBe('Email duplicado na BD');
  });
 });
                                      
test('Test #9 - Listar utilizador por ID', () => {
return app.db('users')
  .insert({ Dados do Utilizador }, ['id'])
  .then((user) => request(app).get(`${MAIN_ROUTE}/${user[0].id}`))
  .set('authorization', bearer ${user.token})
  .then((res) => {
  expect(res.status).toBe(200);
  expect(res.body.name).toBe(Nome do Utilizador);
  });
 });
                                      
test('Test #10 - Atualizar utilizador', () => {
return app.db('users')
  .insert({ Dados do Utilizador }, ['id'])
  .then((user) => request(app).put(`${MAIN_ROUTE}/${user[0].id}`)
  .send({ Nome do utilizador atualizado }))
  .set('authorization', bearer ${user.token})
  .then((res) => {
  expect(res.status).toBe(200);
  expect(res.body.name).toBe(Utilizador atualizado);
  });
 });
                                      
test('Test #11 - Remover Utilizador', () => {
return app.db('users')
  .insert({ Dados do Utilizador }, ['id'])
  .then((user) => request(app).delete(`${MAIN_ROUTE}/${user[0].id}`)
  .send({ Utilizador Removido }))
  .set('authorization', bearer ${user.token})
  .then((res) => {
  expect(res.status).toBe(204);
  });
  });
  ```

## Posts

**Endpoint - HTTP Action - Business Operation**

/Posts - GET - getAllposts

/Posts/{posts_id} - GET - getPostId

/Posts - POST - createPosts

/Posts/{posts_id} - PUT - updatePostId

/Posts/{posts_id} - DELETE - deletePostId



