- [1. Brazilian E-Commerce Project](#1-brazilian-e-commerce-project)
  - [1.1. Conjunto de Dados](#11-conjunto-de-dados)
    - [1.1.1. Esquema de dados](#111-esquema-de-dados)
  - [1.2. Construção do Ambiente Exploratório](#12-construção-do-ambiente-exploratório)
    - [1.2.1. Dockerfile e Docker Compose](#121-dockerfile-e-docker-compose)
    - [1.2.2. Passo a Passo](#122-passo-a-passo)
    - [1.2.3. Configurando o Poetry](#123-configurando-o-poetry)
    - [1.2.4. Passo a Passo para Obter o Token do Jupyter e Usar no VSCode](#124-passo-a-passo-para-obter-o-token-do-jupyter-e-usar-no-vscode)
      - [1.2.4.1. Use o link e token](#1241-use-o-link-e-token)
  - [1.3. Estrutura do Projeto](#13-estrutura-do-projeto)
    - [1.3.1. Principais notebooks](#131-principais-notebooks)


# 1. Brazilian E-Commerce Project

Este projeto tem o objetivo de realizar uma análise exploratório com esse conjunto de dados públicos de E-commerce Brasileiro.
Espera-se realizar essa análise utilizando bibliotecas como `Pandas` e `Matplotilib`.
Também seram realizada análise com a utilização de `SQL` e `Pyspark`.
Por fim desejo investigar essas bases para ver a possíbilidade de construir um **`Modelo Machine Learning`** de classificação.

Para desenvolvimento desse projeto foi realizado o download do conjunto de dados no formato CSV no Link: [Kaggle - Brazilian E-commerce Data](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data).

Os dados foram lidos e salvos em um banco de dados `PostgreSql` com o intuito de de desenvolver habilidades com SQL e Pyspark, para isso foi realizada a construção de um ambiente de desenvolvimento isolado por meio de ``Containers`` do ``Docker``.


## 1.1. Conjunto de Dados

Este é um conjunto de dados públicos de comércio eletrônico brasileiro de pedidos feitos na [Olist Store](https://www.olist.com/). O conjunto de dados conta com informações de 100 mil pedidos de 2016 a 2018 feitos em vários marketplaces no Brasil. Seus recursos permitem visualizar um pedido em várias dimensões: desde o status do pedido, preço, desempenho de pagamento e frete até a localização do cliente, atributos do produto e, finalmente, avaliações escritas pelos clientes.

O Olist conecta pequenas empresas de todo o Brasil aos canais sem complicações e com um único contrato. Esses comerciantes podem vender seus produtos por meio da Olist Store e enviá-los diretamente aos clientes usando os parceiros logísticos do Olist.

Depois que um cliente compra o produto na Olist Store, um vendedor é notificado para atender a esse pedido. Assim que o cliente recebe o produto, ou a data estimada de entrega é devida, o cliente recebe uma pesquisa de satisfação por e-mail onde pode dar uma nota para a experiência de compra e anotar alguns comentários.

**Ponto de atenção:** Um pedido pode ter vários itens.
Cada item pode ser atendido por um vendedor distinto.
Todos os textos que identificam lojas e parceiros foram substituídos pelos nomes das grandes casas de Game of Thrones.

### 1.1.1. Esquema de dados

Os dados são divididos em vários conjuntos de dados para melhor compreensão e organização.
Esquema dos dados:
![Esquema de Dados](data\archive\Esquema_dados.png)

## 1.2. Construção do Ambiente Exploratório


### 1.2.1. Dockerfile e Docker Compose

### 1.2.2. Passo a Passo

1. **Iniciar o Docker Compose:** `docker-compose up`
2. **Verificar os containers em execução:** `docker ps`
3. **Acessar o bash do container:** `docker exec -it <container> bash`

    ```bash
    # Após pegar o nome do container com docker ps
    docker exec -it brazilian_e-commerce_project-ambiente_exploratorio-1 bash
    ```

4. **Iniciar os container\serviços já existentes definidos no arquivo `docker-compose.yml`:** `docker-compose start`
5. **Para todos os containers\serviços já definidos no arquivo `docker-compose.yml`:** `docker-compose stop`

Para mais comandos acessar: 

### 1.2.3. Configurando o Poetry

1. **Instalar dependências com Poetry:** `poetry install`
2. **Configurar o Kernel do Jupyter:** ```python -m ipykernel install --user --name=<container> --display-name "Python (nome_que_desejar)"```

    ```bash
    # Use esse para uma organização melhor
    python -m ipykernel install --user --name=brazilian_e-commerce_project-ambiente_exploratorio-1 --display-name "ambiente_brazilian"
    ```

### 1.2.4. Passo a Passo para Obter o Token do Jupyter e Usar no VSCode

#### 1.2.4.1. Use o link e token

- Use o link com token completo fornecido pelo docker, basta copiar o link com o token (**`http://127.0.0.1:9090/lab/?token=abc123def456`**) e colar na caixa `Existent Jupyter Server`.

- Clique em `Select Kernel` > `Select Another Kernel` > `Existent Jupyter Server`.

- O link comentado é o mesmo link utilizado para acessar o jupyter notebook via navegador

- Pode ser acesso também com os comandos:
  
    ```bash
    docker-compose logs <service_name>
    docker-compose logs
    docker logs <container_id>
    ```

## 1.3. Estrutura do Projeto

```bash
.
├── config                      
│   ├── main.yaml                   # Main configuration file
│   ├── model                       # Configurations for training model
│   │   ├── model1.yaml             # First variation of parameters to train model
│   │   └── model2.yaml             # Second variation of parameters to train model
│   └── process                     # Configurations for processing data
│       ├── process1.yaml           # First variation of parameters to process data
│       └── process2.yaml           # Second variation of parameters to process data
├── data            
│   ├── final                       # data after training the model
│   ├── processed                   # data after processing
│   └── raw                         # raw data
├── docs                            # documentation for your project
├── .gitignore                      # ignore files that cannot commit to Git
├── Makefile                        # store useful commands to set up the environment
├── models                          # store models
├── notebooks                       # store notebooks
│   ├── exploration
│   │   └── .gitkeep
│   ├── modeling
│   │   └── .gitkeep
│   ├── preprocessing
│   │   └── .gitkeep
│   └── reporting
│       └── .gitkeep
├── output                          # store outputs
│   ├── figures
│   │   └── .gitkeep
│   ├── predictions
│   │   └── .gitkeep
│   └── reports
│       └── .gitkeep
├── .pre-commit-config.yaml         # configurations for pre-commit
├── pyproject.toml                  # dependencies for poetry
├── README.md                       # describe your project
├── src                             # store source code
│   ├── __init__.py                 # make src a Python module 
│   ├── process.py                  # process data before training model
│   ├── train_model.py              # train model
│   └── utils.py                    # store helper functions
└── tests                           # store tests
    ├── __init__.py                 # make tests a Python module 
    ├── test_process.py             # test functions for process.py
    └── test_train_model.py         # test functions for train_model.py
```

### 1.3.1. Principais notebooks

