# Relembrando: Métodos HTTP

- **GET** → Busca de dados  
- **POST** → Inserção de dados  

---

## Curl

### Comandos para GET

**Comandos comuns no `curl`:**

    curl URL -I
    curl URL -Iv
    curl URL -L
    curl URL -LI

**Outros comandos GET bastante utilizados:**

    curl URL
    curl -v URL
    curl -H "Authorization: Bearer TOKEN" URL
    curl -H "Accept: application/json" URL

---

## Inserção de dados através do Curl (POST)

### Exemplo de envio de JSON via linha de comando

    curl -X POST -H "Content-Type: application/json" -d '{
      "name": "Leonardo",
      "last_name": "Vidal",
      "cpf": "516.925.785-41",
      "email": "example@teste",
      "birth_data": "1996-10-29"
    }' http://localhost:5000/register

Caso o **CPF seja inválido**, a API retorna automaticamente uma mensagem de erro indicando a falha na validação.

---

## Envio de dados via arquivo

Em APIs maiores, é comum importar um arquivo contendo os dados necessários.  
Assim, o `curl` lê o conteúdo do arquivo em vez de você precisar passar todas as strings diretamente pela linha de comando.

    curl -X POST -H "Content-Type: application/json" -d @arquivo.json http://localhost:5000/register

### Explicação do comando acima

- A flag `-d @arquivo.json` instrui o `curl` a ler o conteúdo do arquivo localizado no seu computador (neste caso, `arquivo.json`) e enviá-lo no corpo da requisição.
- O símbolo `@` é essencial: sem ele, o `curl` enviaria apenas o texto literal `arquivo.json` em vez do conteúdo do arquivo.
- Essa abordagem facilita o envio de **payloads grandes e complexos**, além de tornar os testes mais organizados e reutilizáveis.
