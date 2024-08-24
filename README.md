# Conjuntos de Prescrições

Analise dos dados.

- Tipo de dados analisados, csv
- Usando Python e seu modulo pandas, matplotlib e time


## Caracteristicas

- Importe dos dados analisados
- importe e salve do aqrquivo para GitHub
- Exporte do documento csv

## Instalação

Instalando os dependentes e devdependentes e inciando a analise dos dados.

```sh
Install jupter notebook
```

Para Produção de ambiente...

```sh
py -m venv venv
venv\scripts\activate
```

## Desenvolvimento

Abrindo seu jupter notebook and executando os comandos.

Modulos:

```sh
import pandas
import matplotlib
import time
```

Importando dados com limite 100 e indexadoando a coluna ano e mês:

```sh
dados_df = pd.read_csv("EPD_202204.csv", nrows=100, index_col=0)
```

```sh
def df_dados():

    if dados_df is not None:         
        return dados_df
    return 'Dados não confirmados.'

display(df_dados())
```
#### Trabalho para origem

Para produção de analise:

```sh
def produtos_regiao():
    """
        Analise de produtos por região
    """
    
    produtos_por_regiao = dados_df[['REGIONAL_OFFICE_NAME', 'CHEMICAL_SUBSTANCE_BNF_DESCR', 'TOTAL_QUANTITY']].groupby(['REGIONAL_OFFICE_NAME', 'CHEMICAL_SUBSTANCE_BNF_DESCR']).sum()
    return produtos_por_regiao

display(produtos_regiao())
```

```sh
def grafi_produtos():
    """
        Amostragem dos produtos por região
    
    """
    produtos_regiao().plot(kind='bar', figsize=(15,5))
    return plt.show()

grafi_produtos()
```

```sh
def somatoria():
    """
        Produtos com maior somatoria de custo por meês
    
    Metodos:
    
    groupby = agrupamento
    sum() = somatoria
    sort_values = ordernar 
    head(10) = 10 primeiras linhas
    
    
    """
    somatoria_custos = dados_df[['CHEMICAL_SUBSTANCE_BNF_DESCR', 'ACTUAL_COST']].groupby('CHEMICAL_SUBSTANCE_BNF_DESCR')
    return somatoria_custos

display((somatoria()).sum().sort_values('ACTUAL_COST', ascending=False).head(10))
```

```sh
def grafi_soma():
"""
    Amostragem da somatoria
"""
    somatoria().sum().plot(kind='bar', figsize=(12, 5))
    plt.title('Grafico da somatoria de custos')
    return plt.show()

grafi_soma()
```

```sh
def comuns():
    """
        Os produtos mais comuns
        
    Metodos:
    
    groupby = agrupa
    sum() = soma 
    
    """
    
    prescricoes_comuns = dados_df[['BNF_DESCRIPTION','TOTAL_QUANTITY']].groupby('BNF_DESCRIPTION').sum()
    return prescricoes_comuns

display(comuns().sort_values(by='TOTAL_QUANTITY', ascending=False))
```

```sh
def grafi_comuns():
"""
    Amostragem dos produtos mais comuns
"""
    comuns().plot(kind='bar', figsize=(12, 5))
    plt.title('Grafico de prescrições mais comuns')
    return plt.show()

grafi_comuns()
```

```sh
def mais_prescrito():
    """
        Os produtos que é mais prescritos por cada prescriber
    
    """
    produto_mais_prescrito = dados_df[['CHEMICAL_SUBSTANCE_BNF_DESCR', 
        'BNF_DESCRIPTION','TOTAL_QUANTITY']].groupby('CHEMICAL_SUBSTANCE_BNF_DESCR').sum()
    return produto_mais_prescrito

display(mais_prescrito().sort_values(by='TOTAL_QUANTITY', ascending=False))
```

```sh
def grafi_prescrito():
"""
    Produtos mais prescritos por prescribers
"""
    mais_prescrito().plot(kind='bar', figsize=(12, 5))
    plt.title('Grafico dos produtos mais prescritos')
    ylabel
    return plt.show()

grafi_prescrito()
```

```sh
def qtd_prescribers():
    """
        Quantidade de prescriber adicionados no ultimo mês
    
    """
    
    prescribers_qtd = dados_df.groupby('BNF_DESCRIPTION').BNF_DESCRIPTION.count()
    return prescribers_qtd

print(qtd_prescribers().sum())
```

```sh
def mais_regiao():
    """
        Precribers que atuam em mais de uma regiao
    
    """
    atuam_regiao = dados_df[['REGIONAL_OFFICE_NAME', 'CHEMICAL_SUBSTANCE_BNF_DESCR', 'QUANTITY']].groupby(['REGIONAL_OFFICE_NAME', 'QUANTITY'])
    return atuam_regiao

display(mais_regiao().sum().sort_values(by='QUANTITY', ascending=False))
```

```sh
def preco():
    """
        Preço médio dos produtos coletados no ultimo mês
        
    Metodos:
    
    mean() = média
    
    """
    preco_medio = dados_df['ACTUAL_COST'].mean()
    return preco_medio

print(preco())
```

```sh
def valor_maior():
    """
        Tabela com a prescrição de maior valor do usuario
    
    """
    maior_valor = dados_df[['BNF_DESCRIPTION', 'ACTUAL_COST']].groupby('BNF_DESCRIPTION').sum().max()
    return maior_valor

print(valor_maior())
```

```sh
def rotina_mensal():
    """
        Rorina mensal de coleta de dados do ultimo mês
    
    """
    
    while True:
        dados_df.to_csv('atual.csv')
        time.sleep(5)

display(rotina_mensal())
```
