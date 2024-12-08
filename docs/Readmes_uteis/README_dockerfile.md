
# Explicação do Dockerfile

Este `Dockerfile` cria uma imagem baseada no **Jupyter Notebook com PySpark**, configurada com o **Poetry** para gerenciamento de dependências.

---

## Estrutura do Dockerfile

### 1. `FROM`
```dockerfile
FROM jupyter/pyspark-notebook:spark-3.4.1
```
- Define a imagem base para o container.
  - **`jupyter/pyspark-notebook:spark-3.4.1`**: Imagem oficial do Jupyter Notebook com PySpark, usando a versão 3.4.1 do Spark.

---

### 2. `RUN`
```dockerfile
RUN curl -sSL https://install.python-poetry.org | python3 - --version 1.8.4 && \
    export PATH="$HOME/.local/bin:$PATH" && \
    poetry --version
```
- Instala o **Poetry** no container:
  - **`curl -sSL`**: Baixa o instalador do Poetry.
  - **`python3 - --version 1.8.4`**: Instala a versão 1.8.4 do Poetry.
  - **`export PATH="$HOME/.local/bin:$PATH"`**: Adiciona temporariamente o Poetry ao PATH do sistema.
  - **`poetry --version`**: Verifica a instalação.

---

### 3. `ENV`
```dockerfile
ENV PATH="/home/jovyan/.local/bin:$PATH"
```
- Adiciona o Poetry ao **PATH** do sistema de forma permanente, tornando-o acessível em qualquer sessão.

---

### 4. `WORKDIR`
```dockerfile
WORKDIR /home/jovyan/work
```
- Define o diretório de trabalho padrão no container:
  - Todos os comandos executados no container começarão a partir de **`/home/jovyan/work`**.

---

### 5. `EXPOSE`
```dockerfile
EXPOSE 8888
```
- Expõe a porta **8888**, que é a porta padrão do Jupyter Notebook. Isso permite que o serviço seja acessado de fora do container.

---

## Como Usar

1. **Construir a imagem**
   - Execute o comando para construir a imagem com o Dockerfile:
   ```bash
   docker build -t pyspark-poetry .
   ```

2. **Executar o container**
   - Suba o container usando o comando:
   ```bash
   docker run -p 8888:8888 -v $(pwd):/home/jovyan/work pyspark-poetry
   ```

3. **Acessar o Jupyter Notebook**
   - No navegador, abra o endereço:
   ```
   http://localhost:8888
   ```

---
