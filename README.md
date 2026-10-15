# Desafio 1: catálogo de filmes 🎬

Desenvolva sua primeira **API REST usando Java, Spring Boot e PostgreSQL**, permitindo cadastrar, consultar, atualizar e excluir filmes.

O objetivo é aprender o caminho de uma requisição: receber os dados, validar uma regra de negócio e salvar ou consultar as informações no banco.

### 1. Dados do filme

Utilize apenas uma tabela, chamada `filmes`, com os seguintes campos:

| Campo | Tipo em Java | Regra |
| --- | --- | --- |
| `id` | `Long` | Gerado automaticamente |
| `titulo` | `String` | Obrigatório |
| `diretor` | `String` | Obrigatório |
| `anoLancamento` | `Integer` | Obrigatório |
| `genero` | `String` | Obrigatório |

Não é necessário criar tabelas para diretor ou gênero.

### 2. Funcionalidades do CRUD

A API deve oferecer os seguintes endpoints:

| Método | Endpoint | Funcionalidade |
| --- | --- | --- |
| `POST` | `/filmes` | Cadastrar filme |
| `GET` | `/filmes` | Listar todos os filmes |
| `GET` | `/filmes/{id}` | Buscar filme pelo identificador |
| `PUT` | `/filmes/{id}` | Atualizar filme |
| `DELETE` | `/filmes/{id}` | Excluir filme |

Exemplo de JSON para cadastrar ou atualizar:

```json
{
  "titulo": "Interestelar",
  "diretor": "Christopher Nolan",
  "anoLancamento": 2014,
  "genero": "Ficção científica"
}
```

### 3. Regra de negócio

**Não permitir dois filmes com o mesmo título e ano de lançamento.**

Por exemplo:

- Cadastrar `Interestelar`, de `2014`: permitido.
- Cadastrar novamente `Interestelar`, de `2014`: rejeitado.
- Cadastrar `Interestelar`, com outro ano: permitido.

A comparação deve ignorar diferenças entre letras maiúsculas e minúsculas.

**Essa verificação deve ficar na classe `FilmeService`.** Ela deve consultar o banco antes de cadastrar ou atualizar um filme.

Na atualização, o próprio filme não deve ser considerado uma duplicidade. Portanto, atualizar apenas o gênero de um filme deve funcionar normalmente.

### 4. Organização obrigatória

Crie estas quatro classes:

| Classe | Responsabilidade |
| --- | --- |
| `Filme` | Representar o filme e mapear a tabela do banco |
| `FilmeRepository` | Consultar e persistir os dados usando Spring Data JPA |
| `FilmeService` | Executar as operações e validar a regra de duplicidade |
| `FilmeController` | Receber as requisições HTTP e retornar as respostas |

O fluxo deve ser:

**Controller → Service → Repository → PostgreSQL**

O controller deve chamar a service, sem acessar o repository diretamente.

### 5. Banco de dados

- Criar um banco PostgreSQL chamado `catalogo_filmes`.
- Configurar a conexão no `application.properties` ou `application.yml`.
- Utilizar Spring Data JPA para acessar o banco.
- Manter apenas a tabela `filmes`.

**Para este exercício, pode utilizar `spring.jpa.hibernate.ddl-auto=update`**, permitindo que o Hibernate crie a tabela a partir da entidade.

Os filmes devem continuar disponíveis depois de reiniciar a aplicação.
