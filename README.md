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

| Campo      | Descrição                    |
| ---------- | ---------------------------- |
| id         | Identificador da transação   |
| cliente_id | Identificador do cliente     |
| data       | Data da transação            |
| tipo       | credito ou debito            |
| valor      | Valor monetário da transação |

### Exemplo

```csv
id,cliente_id,data,tipo,valor
1,CLI001,2026-01-10,credito,1500.00
2,CLI001,2026-01-15,debito,200.00
3,CLI002,2026-02-05,credito,5000.00
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
