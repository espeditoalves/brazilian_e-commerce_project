# Configuração de Ambiente com Docker Compose

Este projeto utiliza **Docker Compose** para configurar dois serviços principais: um ambiente de exploração de dados com Jupyter Notebook e um banco de dados PostgreSQL.

## Estrutura do `docker-compose.yml`

### Versão
```yaml
version: '3.8'
```
Define a versão do Docker Compose utilizada. A versão **3.8** é compatível com recursos modernos do Docker.

---

### Serviços

#### 1. Serviço: `ambiente_exploratorio`
Configura um ambiente para exploração de dados com **Jupyter Notebook**.

- **`build`**  
  Configura a construção do container com base no arquivo `Dockerfile` localizado no mesmo diretório.

- **`ports`**  
  Mapeia portas entre o host (máquina local) e o container:
  - `8888:8888`: A porta 8888 do host será usada para acessar o serviço Jupyter Notebook.

- **`volumes`**  
  Mapeia diretórios entre o host e o container, permitindo persistência de dados:
  - `.:/home/jovyan/work`: O diretório atual do host é mapeado para `/home/jovyan/work` no container.

- **`environment`**  
  Define variáveis de ambiente:
  - `JUPYTER_ENABLE_LAB=yes`: Ativa o modo JupyterLab, uma interface moderna do Jupyter.

#### 2. Serviço: `postgres_db`
Configura um banco de dados PostgreSQL.

- **`image`**  
  Define a imagem Docker do PostgreSQL:
  - `postgres:13`: Utiliza a versão 13 do PostgreSQL.

- **`ports`**  
  Mapeia portas entre o host e o container:
  - `5432:5432`: A porta 5432 do host será usada para acessar o banco de dados PostgreSQL.

- **`environment`**  
  Configura variáveis de ambiente para o banco de dados:
  - `POSTGRES_USER=pyspark`: Define o nome do usuário administrador.
  - `POSTGRES_PASSWORD=123456`: Define a senha para o usuário.
  - `POSTGRES_DB=mydatabase`: Define o nome do banco de dados inicial.

- **`volumes`**  
  Configura persistência dos dados do PostgreSQL:
  - `pgdata:/var/lib/postgresql/data`: Salva os dados no volume nomeado `pgdata`, garantindo persistência mesmo que o container seja removido.

---

### Volumes

```yaml
volumes:
  pgdata:
```
- **`pgdata`**: Volume nomeado para armazenar os dados do PostgreSQL, garantindo que os dados sejam preservados mesmo após a exclusão do container.

---

## Resumo dos Serviços

1. **`ambiente_exploratorio`**  
   - Ambiente para análise e desenvolvimento com Jupyter Notebook.

2. **`postgres_db`**  
   - Banco de dados PostgreSQL com dados persistentes.

3. **Volumes**  
   - Garante que os dados do PostgreSQL não sejam perdidos.

---

## Como Usar

1. **Subir os containers**  
   Execute o comando abaixo para iniciar os serviços:
   ```bash
   docker-compose up
   ```

2. **Acessar o Jupyter Notebook**  
   - Abra o navegador e acesse: `http://localhost:8888`.

3. **Conectar ao PostgreSQL**  
   - Utilize a porta `5432`, o usuário `pyspark`, a senha `123456` e o banco `mydatabase`.

---

