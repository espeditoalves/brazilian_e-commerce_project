- [1. O que é docker-compose.yml?](#1-o-que-é-docker-composeyml)
- [2. Como o docker-compose.yml se relaciona com o dockerfile?](#2-como-o-docker-composeyml-se-relaciona-com-o-dockerfile)
- [3. Comandos uteis](#3-comandos-uteis)
  - [3.2. Como sair do shell](#32-como-sair-do-shell)
  - [3.3. Como parar o Container:](#33-como-parar-o-container)
  - [3.4. Como voltar a usar o Container:](#34-como-voltar-a-usar-o-container)
  - [3.5. Como remover um container:](#35-como-remover-um-container)
- [4. Principais Comandos do Docker Compose](#4-principais-comandos-do-docker-compose)
  - [4.6. Verificar o status dos serviços](#46-verificar-o-status-dos-serviços)
  - [4.7. Executar um comando em um container rodando](#47-executar-um-comando-em-um-container-rodando)
  - [4.8. Ver os logs de todos os serviços](#48-ver-os-logs-de-todos-os-serviços)
  - [4.9. Ver os logs de um serviço específico](#49-ver-os-logs-de-um-serviço-específico)
  - [4.10. Recriar os serviços (sem cache)](#410-recriar-os-serviços-sem-cache)
  - [4.11. Escalar o número de containers de um serviço](#411-escalar-o-número-de-containers-de-um-serviço)
  - [4.12. Parar e remover containers, redes e volumes temporários criados pelo `up`](#412-parar-e-remover-containers-redes-e-volumes-temporários-criados-pelo-up)
  - [4.13. Ver as redes criadas pelo Docker Compose](#413-ver-as-redes-criadas-pelo-docker-compose)
  - [4.14. Listar volumes gerados](#414-listar-volumes-gerados)
  - [4.15. Executar um container sem precisar iniciar todos os serviços](#415-executar-um-container-sem-precisar-iniciar-todos-os-serviços)


## 1. O que é docker-compose.yml?
O arquivo **`docker-compose.yml`** é usado pelo **Docker Compose** para definir e gerenciar aplicativos que utilizam múltiplos containers de forma declarativa. Com ele, você pode descrever a infraestrutura do seu aplicativo, especificando os serviços, redes e volumes necessários para a execução do mesmo.

## 2. Como o docker-compose.yml se relaciona com o dockerfile?
Você pode criar uma **imagem personalizada** usando um **`Dockerfile`** e, em seguida, usar o **`Docker Compose`** para orquestrar containers que utilizam essa **imagem personalizada** junto com outras imagens disponíveis na internet.

## 3. Comandos uteis

- **Como acessar o shell do Container:** `docker exec -it <nome-container> bash`

### 3.2. Como sair do shell

```bash
exit
```

### 3.3. Como parar o Container:
```bash
docker stop <nome-container>
```

### 3.4. Como voltar a usar o Container:
```bash
docker start <nome-container>
```

### 3.5. Como remover um container:
```bash
docker rm <nome-container>
```


## 4. Principais Comandos do Docker Compose

1. **Iniciar serviços definidos no arquivo `docker-compose.yml`:** `docker-compose up`

2. **Iniciar os serviços em modo "detached" (em segundo plano):**
`docker-compose up -d`

3. **Iniciar os container\serviços já existentes definidos no arquivo `docker-compose.yml`:**  `docker-compose start`

4. **Para todos os containers\serviços já definidos no arquivo `docker-compose.yml`:**  `docker-compose stop`

5. **Remover containers, redes e volumes criados pelo `docker-compose.yml`: ** `docker-compose down`

6. **Remover containers, redes e volumes (incluindo volumes persistentes):** `docker-compose down -v`

### 4.6. Verificar o status dos serviços
```bash
docker-compose ps
```

### 4.7. Executar um comando em um container rodando
```bash
docker-compose exec <nome_servico> <comando>
```

### 4.8. Ver os logs de todos os serviços
```bash
docker-compose logs
```

### 4.9. Ver os logs de um serviço específico
```bash
docker-compose logs <nome_servico>
```

### 4.10. Recriar os serviços (sem cache)
```bash
docker-compose up --build --no-cache
```

### 4.11. Escalar o número de containers de um serviço
```bash
docker-compose up --scale <nome_servico>=<número>
```

### 4.12. Parar e remover containers, redes e volumes temporários criados pelo `up`
```bash
docker-compose down --rmi all
```

### 4.13. Ver as redes criadas pelo Docker Compose
```bash
docker network ls
```

### 4.14. Listar volumes gerados
```bash
docker volume ls
```

### 4.15. Executar um container sem precisar iniciar todos os serviços
```bash
docker-compose run <nome_servico> <comando>
```
