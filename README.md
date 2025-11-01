#  Pipeline de ETL com PySpark e Arquitetura Medalhão

Este projeto de portfólio demonstra a criação de um pipeline básico de Engenharia de Dados, seguindo a famosa Arquitetura Medalhão (Bronze, Silver e Gold).  
O objetivo é transformar dados brutos de vendas em informações prontas para análise, utilizando PySpark e Delta Lake para garantir a qualidade e a organização em um Data Lake.

---

##  Sobre o Projeto (O que foi feito)

Desenvolvi um pipeline de ETL simples, mas que mostra a organização de um bom Data Lake.  
**Fonte de Dados:** Um arquivo CSV de vendas (`data/vendas.csv`).  
**Ferramentas:** PySpark para processamento, Delta Lake para armazenamento confiável e Databricks (ambiente de desenvolvimento) como plataforma.  
**Processo:** O projeto realiza limpeza, normalização e agregações para gerar métricas de negócio.

**Habilidades em Destaque:**
- **Arquitetura Medalhão 🥉🥈🥇:** Implementação das 3 camadas para refinamento e governança dos dados.  
- **PySpark/DataFrames:** Uso do Spark para processamento distribuído.  
- **Transformações ETL:** Aplicação de lógica para garantia de schema, conversão de tipos (ex: datas) e criação de novas colunas calculadas.  
- **Agregação de Dados:** Geração de métricas (Receita Total Diária) na camada Gold, otimizadas para consumo BI/Analítico.

---

##  Estrutura do Repositório

O projeto está organizado com foco em clareza e separação de responsabilidades:

```
etl-databricks-delta-lake/
├── data/                    # Contém o arquivo CSV de origem.
├── images/                  # Contém as capturas de tela usadas na documentação.
├── notebooks/               # Scripts PySpark do pipeline (Bronze, Silver, Gold).
├── .gitignore               # Ignora arquivos de ambiente e cache.
└── requirements.txt         # Dependências necessárias para execução.
```

---

##  O Fluxo de Refinamento (Camada por Camada)

### 1. Camada Bronze (Ingestão/Raw) 🥉
**Função:** Ingerir o CSV e salvá-lo como uma Delta Table.  
**Transformação:** Mínima. Apenas a garantia do schema inicial, como a conversão da coluna `order_date` para o tipo `date`.  
📸 <img width="1455" height="1169" alt="ingestao_bronze" src="https://github.com/user-attachments/assets/eae09e06-c1fe-40cb-8304-49cd59d1909a" />


---

### 2. Camada Silver (Refinamento/Limpeza) 🥈
**Função:** Limpar e enriquecer os dados.  
**Transformação Principal:** Criação da coluna `total_revenue` (preço × quantidade). O dado agora está mais limpo e pronto para a modelagem.  
📸 <img width="1474" height="1186" alt="transformacao_prata" src="https://github.com/user-attachments/assets/793b3e26-d3f7-4da6-8c7a-f60cde55a907" />



---

### 3. Camada Gold (Curadoria/Consumo) 🥇
**Função:** Modelar e agregar o dado para o consumo final.  
**Transformação Principal:** Cálculo da Receita Total Diária (`total_revenue_daily`). Essa tabela é otimizada para ser consultada por ferramentas de Business Intelligence (BI).  
📸 <img width="1464" height="1182" alt="agregacao_ouro" src="https://github.com/user-attachments/assets/ba91f241-76bf-47eb-8e78-c8f01131b126" />


---

##  Execução (Foco em Databricks)

Este projeto foi desenvolvido e testado no ambiente **Databricks Community Edition**.  

Para rodar, o processo mais simples é:

1. **Importar:** Clone este repositório diretamente para um Databricks Workspace usando a integração Git.  
2. **Configurar:** Anexar os notebooks a um Cluster Spark.  
3. **Executar Sequencialmente:** Os scripts em `notebooks/` devem ser executados em ordem para garantir que as tabelas sejam criadas corretamente:

   ```
   ingestao_bronze.py
   transformacao_prata.py
   agregacao_ouro.py
   ```
