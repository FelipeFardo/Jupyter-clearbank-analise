# Análise de Transações Financeiras

## Sobre o Projeto

Este projeto foi desenvolvido em Python com o objetivo de realizar a leitura, validação, análise e visualização de dados de transações financeiras armazenadas em um arquivo CSV.

O sistema processa os dados, identifica registros inválidos, gera estatísticas mensais, detecta transações suspeitas e exporta os resultados para um arquivo JSON. Além disso, produz gráficos para facilitar a interpretação das informações.

O desenvolvimento e a execução foram realizados em ambiente Docker utilizando Jupyter Notebook.

---

## Objetivos

* Ler dados de transações financeiras a partir de um arquivo CSV.
* Validar e limpar registros inconsistentes.
* Gerar estatísticas mensais.
* Identificar transações suspeitas.
* Exportar resultados em formato JSON.
* Exibir relatórios formatados na saída do notebook.
* Gerar visualizações gráficas dos dados.

---

## Tecnologias Utilizadas

* Python 3
* Jupyter Notebook
* Docker
* Pandas
* Matplotlib
* CSV (biblioteca padrão)
* JSON (biblioteca padrão)
* Datetime

---

## Estrutura dos Dados

O arquivo CSV deve conter as seguintes colunas:

| Coluna     | Tipo esperado | Descrição                                                          |
| ---------- | ------------- | ------------------------------------------------------------------ |
| id         | inteiro       | Identificador único da transação                                   |
| data       | texto         | Data da transação no formato `AAAA-MM-DD`                          |
| cliente_id | texto         | Código do cliente (não pode ser vazio)                             |
| tipo       | texto         | Tipo da transação: `credito` ou `debito`                           |
| valor      | decimal       | Valor da transação (deve ser maior que `0`)                        |
| descricao  | texto         | Descrição livre da operação                                        |
| categoria  | texto         | Categoria da transação (ex.: `salario`, `compra`, `transferencia`) |

### Exemplo

```csv
id,data,cliente_id,tipo,valor,descricao,categoria
1,2026-01-05,CLI001,credito,3500.00,Salário mensal,salario
2,2026-01-10,CLI001,debito,250.50,Compra supermercado,compra
3,2026-01-15,CLI002,debito,1200.00,Pagamento aluguel,moradia
```

---

## Regras de Validação

Uma transação é considerada válida quando:

* O campo `id` é numérico e não está vazio.
* O campo `cliente_id` não está vazio.
* A data está no formato `YYYY-MM-DD`.
* O campo `tipo` possui valor `credito` ou `debito`.
* O valor é numérico e maior que zero.

Registros que não atendem a essas regras são classificados como inválidos.

---

## Estatísticas Geradas

Para cada mês são calculados:

* Quantidade de transações
* Total de créditos
* Total de débitos
* Saldo mensal
* Valor médio das transações
* Maior valor registrado
* Menor valor registrado

Exemplo de estrutura:

```python
resumo_mensal[mes] = {
    "quantidade": 10,
    "total_credito": 15000.00,
    "total_debito": 4200.00,
    "saldo": 10800.00,
    "media": 1920.00,
    "maior_valor": 5000.00,
    "menor_valor": 100.00
}
```

---

## Identificação de Transações Suspeitas

O sistema considera suspeitas as transações com valor superior a:

```python
LIMITE_SUSPEITO = 10000.00
```

Essas transações são listadas separadamente no relatório final.

---

## Relatório JSON

Ao final da execução é gerado um arquivo JSON contendo:

```json
{
  "gerado_em": "2026-05-14",
  "total_transacoes_validas": 6,
  "total_transacoes_invalidas": 2,
  "resumo_mensal": {},
  "transacoes_suspeitas": []
}
```

---

## Visualização de Dados

O projeto gera gráficos utilizando Matplotlib.

### Gráfico de Barras Empilhadas

Compara os valores de créditos e débitos por mês.

Características:

* Título
* Rótulo do eixo X
* Rótulo do eixo Y
* Legenda

Exemplo:

```python
plt.bar(meses, creditos, label="Crédito")
plt.bar(meses, debitos, bottom=creditos, label="Débito")
```

---

## Relatório no Notebook

Após a execução, o sistema exibe um relatório formatado contendo:

* Quantidade de registros válidos e inválidos.
* Estatísticas mensais.
* Lista de transações suspeitas.
* Resumo geral dos dados processados.

Exemplo:

```text
==================================================
RELATÓRIO DE ANÁLISE DE TRANSAÇÕES
==================================================

Total de transações válidas: 6
Total de transações inválidas: 2

Mês: 2026-01
Quantidade de transações: 2
Total de créditos: R$ 1500.00
Total de débitos: R$ 200.00
Saldo: R$ 1300.00
```

---

## Como Executar

### Iniciar o ambiente Docker

```bash
docker compose up -d
```

### Acessar o Jupyter Notebook

Abra o navegador:

```text
http://localhost:8888/lab?token=desafio-analise-financeira
```

### Executar o Projeto

1. Abra o notebook do projeto.
2. Execute as células na sequência.
3. Verifique:

   * Relatório gerado na saída do notebook.
   * Arquivo JSON exportado.
   * Gráficos gerados durante a análise.

---

## Estrutura do Projeto

```text
project-data/
│
├── work/
│   ├── documents/
│   │   └── transactions.csv
│   │
│   └── notebooks/
│       └── desafio_final.ipynb
        └── analise_pandas.ipynb
        └── relatorio.json
        └── grafico.png
│
└── docker-compose.yaml
└── README.md
```

---

## Autor

Projeto desenvolvido para fins acadêmicos com o objetivo de praticar:

* Manipulação de arquivos CSV
* Validação de dados
* Estruturas de dados em Python
* Análise estatística
* Exportação para JSON
* Visualização de dados com Matplotlib
* Utilização de Docker e Jupyter Notebook
* Biblioteca Pandas para análise de dados
