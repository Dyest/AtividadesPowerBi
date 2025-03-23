
# **Projeto 2**
O objetivo principal deste segundo projeto é construir uma dashboard no Power BI, explorando conceitos intermediarios de formatação e customização, alem de uma maior utilziação de formulas DAX basicas. Para esse projeto foi definido uma dashboard para uma concecionaria, utilizando uma tabela voltado a modelos e placas de carros alem de km rodados e situaçoes cadastral de clientes.

### 📈 **Gráficos e Visualizações**  
- **Gráfico de Barras Horizontal**: Exibe o faturamento geral por dia da semana.  
- **Gráficos de Barras Verticais**:  
  - Exibe o faturamento por Ano, Trimestre, Mês e Dia.  
  - Apresenta a **% de faturamento** por Ano e Mês.  

### 🎛️ **Filtros (Segmentações de Dados)**  
Foram implementados **4 filtros interativos**, permitindo uma análise mais dinâmica:  
- **Situação**  
- **Ano**  
- **Modelo**  
- **Dia**  

### 📊 **Indicadores Chave (KPI's)**  
Três **cards informativos** para destacar métricas essenciais:  
- **Total de Clientes**  
- **Média de KM Rodados**  
- **Faturamento Total**  

### 📋 **Tabela de Resumo de Consumo**  
A tabela exibe informações detalhadas sobre cada transação, incluindo:  
- **ID do Cliente**  
- **Marca e Modelo dos veículos**  
- **Placa do veículo**  
- **Data da Transação e Dia da Semana**  
- **Cadastro e Status do Cliente** (com ícones personalizados)  
- **Faturamento da Transação**  
###  📊**Resultado Final tela de veiculos**
![image](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-2/images/pag_1.jpg)

### 📌 **Fórmulas DAX Utilizadas**  

#### 📅 **Colunas Calculadas**  
**Obter o Dia da Semana** - Esta função extrai o dia da semana a partir da data da transação.  

```DAX
DIA_DA_SEMANA = FORMAT('tb_km'[DATA], "dddd")
```
**Icone dos status** - Define valores numéricos para representar status com ícones.
```DAX
STATUS_ICONE = IF('tb_km'[SITUAÇÃO CADASTRAL] = "ATIVO", 1, 2)
```

#### 📊 **Medidas Calculadas**

Calcula a média dos quilômetros percorridos pelos veículos.

```DAX
MEDIA_KM = AVERAGE('tb_km'[KILOMETRO_PERCORRIDO])
```

Calcula o total de clientes registrados na tabela por meio de seus IDs. 
```DAX
TT CLIENTES = DISTINCTCOUNT(tb_km[ID_CLIENTE])

Calcula o total de cidades registrados na tabela. 
```
```DAX
TOTAL_CIDADES = DISTINCTCOUNT(tb_cli[CIDADE])
```
Calcula o valor total de salarios dos usuarios cadastrados atraves de seus IDs. 
```DAX
SLARIO_CLI = SUM(tb_cli[SALARIO]) / DISTINCTCOUNT(tb_cli[ID])
```

calcula o Faturamento total
```DAX
FATURAMENTO = SUMX(tb_km, [KILOMETRO_PERCORRIDO]* [VALOR POR KM])
```
## 📊 **TB_CLI e Relações entre Tabelas**

#### 🗂 **Tabela `tb_cli`**  
Foi adicionada uma nova tabela chamada `tb_cli`, que contém informações sobre os clientes cadastrados no sistema. Não foi necessário realizar processos iniciais de ETL, pois não havia dados faltantes.

#### 🔗 **Relacionamento entre Tabelas**  
Foi criada a primeira relação entre as tabelas `tb_km` e `tb_cli`. Inicialmente, foi feito um **Inner Join** com base nos IDs dos clientes, já que a tabela `tb_km` contém múltiplos registros para cada cliente (tabela fato de muitos para um), e a tabela `tb_cli` é a tabela de dimensão, com um único registro para cada cliente.

Como a tabela `tb_km` possui dados adicionais e é a tabela de fato, foi necessário realizar um **Left Join** entre `tb_km` e `tb_cli`, garantindo que todos os dados de quilômetros percorridos fossem preservados, enquanto relacionamos os registros de clientes.

 
Foi realizado também um **Anti Left Join** para identificar os clientes que estão registrados na tabela `tb_km`, mas que não estão registrados oficialmente na tabela `tb_cli`.

A estrutura de relacionamento entre as tabelas ficou assim:
- `tb_km` (muitos) → `tb_cli` (um)


###  📊**Resultado dos relacionamentos**
![image](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-2/images/relacionamento.jpg)

###  📊**Resultado final tela de clientes**
![image](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-2/images/pag_2.jpg)
## **DUVIDAS**

📌 **Diferença entre SUM e SUMX**

✅ SUM → Faz a soma direta de uma coluna específica. \
✅ SUMX → Faz a soma iterando linha por linha e aplicando um cálculo antes da soma.

🔍 **Quando usar SUM?**\

Quando você quer somar diretamente os valores de uma coluna.
É mais rápido e mais eficiente em termos de desempenho.

```DAX
TOTAL_VENDAS = SUM(Tabela[Vendas])
```
👉Dessa forma ele simplesmente soma todos os valores da coluna [Vendas].

🔍 **Quando usar SUMX?**

Quando o cálculo depende de outras colunas ou precisa ser feito linha por linha antes da soma ou quando a soma envolve uma expressão calculada, como multiplicação de colunas.

```DAX
TOTAL_VENDAS_COM_DESCONTO = SUMX(Tabela, Tabela[Quantidade] * Tabela[Preco_Unitario])
```
👉Dessa forma o SUMX multiplica Quantidade * Preco_Unitario para cada linha e só depois soma os resultados.

✅ Vantagem: Evita a criação de uma coluna extra apenas para armazenar os valores da multiplicação antes da soma, tornando o modelo mais leve e eficiente.

