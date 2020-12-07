# api-gateway
Api Gateway Zuul

# Config
### Build
Buildar o projeto usando o maven:
```
mvn clean install
```

### Run
Após isso execute o comando abaixo para inicializar a aplicaçao na porta 5555:
```
mvn spring-boot:run
```

# Endpoints
### Auth
- Para gerar um token:
```
Post: localhost:8088/oauth/token
Headers: 
    'Authorization: Basic dGVzdGU6cGFzcw==' 
    'Content-Type: multipart/form-data;
Body: 
    'scope=web'
    'grant_type=password'
    'username=vini'
    'password=pass'
```

### Gerenciador Cadastro API
- Para criar um novo automovel:
```
Post: localhost:5555/gerenciador-cadastro/automovel
Headers: 'Authorization: Bearer {access_token gerado no Auth}' 
Body: {
      	"modeloId" : 1,
      	"valor" : 150000.00
      }
```

- Para listar todos os automoveis:
```
Get: localhost:5555/gerenciador-cadastro/automovel
```

- Para buscar um automovel por id:
```
Get: localhost:5555/gerenciador-cadastro/automovel/{id}
```

### Gerenciador Pagamento API
- Para criar um novo boleto:
```
Post: localhost:5555/gerenciador-pagamento/pagamento/boleto
Headers: 'Authorization: Bearer {access_token gerado no Auth}' 
Body: {
      	"automovelId" : 1,
      	"valor" : 150000.00,
      	"vencimento" : "2020-12-10"
      }

Obs.: 
- Caso o valor nao seja enviado, será gerado um boleto com o valor total do automovel
- Caso a data de vencimento nao seja enviada, será gerado um boleto com vencimento D+5 dias
```