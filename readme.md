# Nome do Projeto

Descrição concisa do projeto, sua finalidade e funcionalidades.

## Índice


- [Como Usar](#como-usar)
- [Autenticar](#autenticar)
- [Contas Bancárias](#contas-bancárias)
- [Gerando cobrabança](#gerando-cobrança)
- [Obtendo estado cobrança](#obtendo-estado-cobrança)


### URL API

[hom-brazpix](https://hom-brazpix.azurewebsites.net/swagger/index.html)

### Como Usar

O primeiro passo para o consumo da API é a por meio do endpoint autenticar

#### Autenticar

![endoi point da API](https://github.com/Brazpix/Documentacao/assets/7662248/0ebe487f-75fd-41c6-9c93-60cc52bfcb19)

```exemplo
{
  "nomedeusuario": "usuario",
  "senha": "senha"
}
```

Durante o processo de authenticação o sistema irá retornar os seguintes dados

```
{
  "user": "fdc1470e-8342-452a-b875-c4eec48f2654",
  "nome": "nathan",
  "email": "nathan@tes.com",
  "nivel": "Administrador",
  "contas": [
    {
      "id": "918c7d15-37da-4487-bd91-9f23212cea3a",
      "usuarioAdministrativoId": "fdc1470e-8342-452a-b875-c4eec48f2654",
      "instituicaoBancaria": 1,
      "clienteId": "eyJpZCI6ImNjMSIsImNvZGlnb1B1YmxpY2Fkb3IiOjAsImNvZGlnb1NvZnR3YXJlIjozNzU4OCwic2VxdWVuY2lhbEluc3RhbGFjYW8iOjF9",
      "clienteSegredo": "eyJpZCI6Ijc0NmEyMzctYjQ5IiwiY29kaWdvUHVibGljYWRvciI6MCwiY29kaWdvU29mdHdhcmUiOjM3NTg4LCJzZXF1ZW5jaWFsSW5zdGFsYWNhbyI6MSwic2VxdWVuY2lhbENyZWRlbmNpYWwiOjEsImFtYmllbnRlIjoicHJvZHVjYW8iLCJpYXQiOjE2NzExMTkwMTk4MDJ9",
      "chavePix": "9161b0de-32f4-4645-aa5d-474d46315a6e",
      "apelido": "Conta 1",
      "ambiente": 1,
      "favorita": false
    }
  ],
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjZXJ0c2VyaWFsbnVtYmVyIjoiZmRjMTQ3MGUtODM0Mi00NTJhLWI4NzUtYzRlZWM0OGYyNjU0IiwibmFtZSI6Im5hdGhhbiIsInJvbGUiOiJBZG1pbmlzdHJhZG9yIiwiaHR0cDovL3NjaGVtYXMubWljcm9zb2Z0LmNvbS93cy8yMDA4LzA2L2lkZW50aXR5L2NsYWltcy9leHBpcmF0aW9uIjoiMy8xNC8yMDI0IDc6MzI6NDUgUE0iLCJuYmYiOjE3MDk4Mzk5NjUsImV4cCI6MTcxMDQ0NDc2NSwiaWF0IjoxNzA5ODM5OTY1fQ.VAvZdvi-XjuSPNCdgD8C0ir37ipqK7QAS_WaeCuSJD0",
  "expiration": "2024-03-14T19:32:45.9364465Z"
}
```

A partir desse ponto todas as consultas devem ser feitas utilizando o token como Bearer

#### Contas Bancárias

Caso o cliente possua uma conta cadastrada para gerar pix o sistema irá retornar o bloco  na autenticação.

```
"contas": [
  {
    "id": "918c7d15-37da-4487-bd91-9f23212cea3a",
    "usuarioAdministrativoId": "fdc1470e-8342-452a-b875-c4eec48f2654",
    "instituicaoBancaria": 1,
    "clienteId": "eyJpZCI6ImNjMSIsImNvZGlnb1B1YmxpY2Fkb3IiOjAsImNvZGlnb1NvZnR3YXJlIjozNzU4OCwic2VxdWVuY2lhbEluc3RhbGFjYW8iOjF9",
    "clienteSegredo": "eyJpZCI6Ijc0NmEyMzctYjQ5IiwiY29kaWdvUHVibGljYWRvciI6MCwiY29kaWdvU29mdHdhcmUiOjM3NTg4LCJzZXF1ZW5jaWFsSW5zdGFsYWNhbyI6MSwic2VxdWVuY2lhbENyZWRlbmNpYWwiOjEsImFtYmllbnRlIjoicHJvZHVjYW8iLCJpYXQiOjE2NzExMTkwMTk4MDJ9",
    "chavePix": "9161b0de-32f4-4645-aa5d-474d46315a6e",
    "apelido": "Conta 1",
    "ambiente": 1,
    "favorita": false
  }
]
```


Caso o cliente não possua deve ser cadastrado por meio da rota:

```
  https://hom-brazpix.azurewebsites.net/v1/cadastrarcontabancaria
```

Deve ser informado o token da autenticação com o seguinte corpo: 

```
{
  "bancoid": "17fc4118-5ada-49d2-84ff-f70b08e87517",
  "clienteid": "eyJpZCI6IjcwNjM5ZWEtYjBkNS00YzFjLThlYTYtNSIsImNvZGlnb1B1YmxpY2Fkb3IiOjAsImNvZGlnb1NvZnR3YXJlIjo0MTA0Miwic2VxdWVuY2lhbEluc3RhbGFjYW8iOjF9",
  "clientesegredo": "eyJpZCI6IjBkMmQ1NWYtMmQ4NC00MWJjLWJhIiwiY29kaWdvUHVibGljYWRvciI6MCwiY29kaWdvU29mdHdhcmUiOjQxMDQyLCJzZXF1ZW5jaWFsSW5zdGFsYWNhbyI6MSwic2VxdWVuY2lhbENyZWRlbmNpYWwiOjEsImFtYmllbnRlIjoiaG9tb2xvZ2FjYW8iLCJpYXQiOjE2NTk2MjgzNjIxNjh9",
  "chavepix": "28779295827"
}
```

![Cadastro de conta bancária](https://github.com/Brazpix/Documentacao/assets/7662248/f93b4b1d-c9f1-43e4-a9d6-16973eb59de6)


#### Gerando Cobranças

Para gerar deve ser por meio da rotina gerarcobranca

_obs: o campo ContaId é referente ao id da conta informado quando se obtem o usuário_


```
{
    "ContaId": "918c7d15-37da-4487-bd91-9f23212cea3a",
    "Valor": 2.22,
    "Descricao": "testando novo retorno"
}
```
![Gerando cobrança](https://github.com/Brazpix/Documentacao/assets/7662248/dd3d039e-5262-4711-badf-712c47f63723)


#### Obtendo estado cobrança

A consulta de cobranças deve ser por meio do metodo consultarcobranca informando o token que foi gerado no momento da transação.

![Obter estado da cobrança](https://github.com/Brazpix/Documentacao/assets/7662248/40f782bf-9d1c-48cd-8be0-a750425821c4)
