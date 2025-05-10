
# 📊 Projeto 5 - Integração SQL Server com Power BI

Este projeto demonstra a **integração entre SQL Server e Power BI**, utilizando uma modelagem de dados que facilita a análise e visualização de informações sobre eventos. Alem disso esse projeto tem como função relembrar, estudar e praticar comandos e funçoes SQL.

---

## 🔍 Estrutura do Banco de Dados

Inicialmente, o banco de dados era composto por:
- **Tabela Fato:** `tb_eventos`
- **Tabelas Dimensão:** `dim_empresa` e `dim_categoria`

Com base na tabela fato `tb_eventos`, foram criadas **novas tabelas dimensão**, permitindo maior flexibilidade na análise dos dados:

### ✅ **Novas Tabelas Dimensão Criadas**
1. **dim_tipo_evento** → Tipos de eventos registrados.
2. **dim_cobertura** → Coberturas oferecidas nos eventos.
3. **dim_coordenador** → Coordenadores responsáveis pelos eventos.
4. **dim_contratante** → Empresas contratantes dos eventos.

\
Cada tabela foi criada visando a **eliminação de valores duplicados**  alem de incrementar os estudos (apesar de não ser realmente necessaria criar as tabelas dim nesse caso). 

```sql
-- Criando a tabela dimensão de Tipos de Eventos
SELECT DISTINCT (tipo_evento) INTO dim_tipo_evento FROM tb_eventos;
``` 
```sql
-- Criando a tabela dimensão de Cobertura
SELECT DISTINCT (cobertura) INTO dim_cobertura FROM tb_eventos;
```
```sql
-- Criando a tabela dimensão de Coordenador
SELECT DISTINCT (coordenador_resp) INTO dim_coordenador FROM tb_eventos;
```
```sql
-- Criando a tabela dimensão de Contratante
SELECT DISTINCT (contratante) INTO dim_contratante FROM tb_eventos;
```

## 🛠 Criação da View para o Power BI

Após a normalização dos dados, foi criada uma View chamada eventos_tratado, visando obter uma melhor visualização geral dos dados, garantindo uma estrutura mais organizada e sem valores nulos para o carregamento no Power BI.

```
CREATE VIEW eventos_tratado AS
SELECT 
    data_evento AS data,
    id_empresa AS id,
    tipo_evento AS [tipo de evento], 
    
    CASE WHEN pgto = '50% PAGO' 
        THEN 'PARCIALMENTE' 
        ELSE pgto END AS pago,

    total_participantes_evento AS [total de participantes],
    cobertura,
    coordenador_resp AS coordenador,
    
    CASE WHEN valor_faturado_dia IS NULL
        THEN '0,00' 
        ELSE valor_faturado_dia END AS faturamento,

    CASE WHEN royalties_holding IS NULL 
        THEN '0,00' 
        ELSE royalties_holding END AS [royalties pagos],

    CASE WHEN desconto_contratante IS NULL 
        THEN '0,00' 
        ELSE desconto_contratante END AS [desconto contratantes],

    contratante AS contratantes,
    categoria AS categoria
FROM tb_eventos;

```

## 📅 Criação da Tabela Calendário

Após o tratamento da View, foi criada uma **tabela dimensão calendário** para melhor análise temporal dentro do **Power BI**. (Uma breve introdução sobre PL SQL)

```sql
CREATE TABLE dim_calendario (
    data DATE PRIMARY KEY,
    ano INT,
    mes INT,
    dia INT,
    dia_semana VARCHAR(50)
);

DECLARE @DataInicial DATE = '2017-01-02';
DECLARE @DataFinal DATE = '2017-05-16';

DECLARE @DataAtual DATE = @DataInicial;

WHILE @DataAtual <= @DataFinal
BEGIN 
    INSERT INTO dim_calendario (data, ano, mes, dia, dia_semana)
    VALUES (@DataAtual, YEAR(@DataAtual), MONTH(@DataAtual), DAY(@DataAtual), DATENAME(WEEKDAY, @DataAtual));

    SET @DataAtual = DATEADD(DAY, 1 , @DataAtual);
END;
```


## 📊 Integração no Power BI

Após as modificações realizadas no banco de dados, as tabelas foram consumidas no Power BI, onde foram estabelecidos os relacionamentos necessários entre as tabelas, garantindo a correta estruturação dos dados.

![Modelo Relacional](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-5/Imagens/Relacionamentos.png?raw=true)

---

## 📈 Criação das Visualizações

Com os dados devidamente estruturados, foram iniciadas as visualizações dentro do Power BI.

📌 **Observação:** Como o foco era apenas na integração e estudo do SQL, não foi realizada uma estilização avançada, apenas a construção de uma Dashboard simples contendo alguns dados considerados por mim relevantes para análise.

---

## 🖥️ Tela 1 - Análise Financeira

A primeira tela apresenta um **dashboard financeiro**, destacando informações sobre faturamento e pagamentos de eventos.

### 🔹 Elementos Visuais

- **Gráficos de Rosca**  
  - O primeiro representa a **distribuição dos pagamentos**, separando eventos pagos, parcialmente pagos e não pagos.  
  - O segundo apresenta a percentagem do faturamento atual**, com base nos pagamentos já efetuados e parcialmente efetuados.

- **Gráfico de Barras**  
  - Exibe a evolução do faturamento ao longo dos dias, meses e anos.

- **Cards Indicadores**  
  - Apresentam métricas como faturamento atual, faturamento pendente, quantidade de pagamentos parcialmente pendentes e pendentes.

- **Tabela de Eventos**  
  - Exibe os tipos de eventos e seus respectivos faturamentos, juntamente com seus tipos (custo alto/baixo) e a quantidade total de realizações.


![Tela 1](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-5/Imagens/Pagina1.png?raw=true)

---

## 📊 Tela 2 - Eventos e Contratantes

A **segunda tela** do dashboard apresenta análises detalhadas sobre **quantidade de eventos, participantes e contratantes**.

### 🔹 **Elementos Visuais**
- **Gráfico de Barras:** Compara os pagamentos entre eventos de **custo alto** e **custo baixo**.  
- **Gráfico de Barras Horizontal:** Exibe os **cinco principais contratantes** por faturamento.  
- **Gráfico de Barras Horizontal:** Exibe os contratantes que realizaram **mais eventos**.  

![Tela 2](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-5/Imagens/Pagina2.png?raw=true)

---

É isso rapaziada vlw por chegar até aqui

