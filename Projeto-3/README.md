
# **Projeto 3**

O objetivo principal deste terceiro projeto é desenvolver um dashboard mais robusto no Power BI, focado na análise de faturamento, utilizando dados consolidados dos anos de 2017 a 2019. O projeto explora conceitos de modelagem de dados, criação de medidas em DAX e visualizações com tooltips personalizadas.

### 📈 **Gráficos e Visualizações**  
- **Gráficos de Meta por Ano (Gauge)**: Visualização das metas anuais de faturamento com comparação do valor atingido.  
- **Gráfico de Linhas (Crescimento Percentual)**: Comparativo entre os faturamentos diários de 2018 e 2019, com destaque para a linha de crescimento percentual.  
- **Gráfico de Colunas (Faturamento por Ano)**: Exibe o total faturado em cada ano (2017, 2018 e 2019).  
- **Gráfico de Barras (Faturamento x Cancelado por Vendedor)**: Comparação entre o total faturado e o valor cancelado por vendedor.  
- **Gráfico de Colunas (Faturamento por Tipo de Pagamento)**: Apresenta os valores de faturamento divididos por método de pagamento (crédito, débito, presente, dinheiro).  
- **Tabela Resumo de Vendas**: Detalhamento completo por número fiscal, data, vendedor, forma de pagamento e valores.  
- **Segmentações**: Filtros por vendedor e valor da venda.

### 🎛️ **Filtros (Segmentações de Dados)**  
Foram implementados filtros interativos com base na Tabela Calendário:  
- **Ano**  
- **Mês**  
- **Dia**  
- **Vendedor**  
- **Valor da Venda**

### 📊 **Indicadores Chave (KPI's)**  
Foram criados cards informativos para destacar os principais indicadores:  
- **Lucro Total**  
- **Lucro por Forma de Pagamento**  
- **Lucro nos Últimos 10 Dias**  
- **Variação Percentual de Lucro**

### 📋 **Unificação e Modelagem de Dados**  
- Consolidação das tabelas de faturamento de **2017, 2018 e 2019** em uma única tabela unificada.
- Criação de uma **tabela calendário** automática para análises temporais avançadas.

### 📊 **Resultado Final da Tela Principal**
![Dashboard Projeto 3](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-3/imgs/dashboard.png)  


## 📊 **Relacionamento entre Tabelas**

As tabelas de faturamento foram unificadas e relacionadas à Tabela Calendário por meio do campo de data, permitindo a aplicação de filtros e medidas temporais. 

![Relacionamento Projeto 3](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-3/imagem-dashboard.png)  

