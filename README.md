
# **ATIVIDADES PRATICAS DE POWER BI**

Estes projetos foram desenvolvidos atraves de um curso externo de Power BI + SQL, no qual estou aprendendo algus dos conceitos dessas ferramentas.


# **Projeto 1**
O objetivo principal deste primeiro projeto é construir uma dashboard inicial no Power BI, explorando conceitos básicos de formatação e customização.

### 💻**Funcionalidades desejadas**
Para este projeto, foram designadas as seguintes funcionalidades, além de toda a customização e padronização necessárias para garantir uma visualização clara e eficaz dos dados:

- **Gráfico de Barras Vertical**: Exibe os salários dos funcionários.
- **Gráfico de Linhas**: Avalia os salários por departamento ao longo do tempo.
- **Gráficos de Barras Horizontais**:
  - Mostra a quantidade de faltas por filial.
  - Exibe os salários gastos por filial.
- **Segmentação de Dados**: Permite uma análise mais detalhada dos dados por **departamento**.
- **6 Segmentações de Dados** para filtros adicionais:
  - Nomes dos funcionários.
  - Filiais.
  - Contratações realizadas.
  - Demissões realizadas.
  - Quantidade de faltas.
  - Sexo dos funcionários.
- **Gráficos de Rosca**:
  - Quantidade de funcionários por gênero (valor tota e em porcentagem).
  - Média de idade por gênero (valor tota e em porcentagem).
- **Card**: Mostra a quantidade total de funcionários.
##  📊**Resultado Final**
![image](https://github.com/Dyest/AtividadesPowerBi/blob/main/Projeto-1/Images/dashboard.jpg)

## **Funções DAX**  

As funções **DAX (Data Analysis Expressions)** são utilizadas para realizar cálculos avançados e operações dinâmicas no Power BI. Elas permitem a criação de colunas calculadas e medidas personalizadas, possibilitando uma análise de dados mais eficiente e flexível.  

Com DAX, é possível não apenas gerar novos insights, mas também otimizar o desempenho dos cálculos, tornando as análises mais dinâmicas e robustas.  

### 📌**Medidas Criadas**  

Neste projeto, foram criadas quatro medidas iniciais utilizando funções DAX básicas, como **`SUM`**, **`AVERAGE`** e **`COUNT`**.  

```javascript
TOTAL DE SALARIOS = SUM(tb_rh[SALARIO]) 
```

```javascript
QTDE TOTAL DE FALTAS = SUM(tb_rh[QTDE FALTA]) 
```

```javascript
IDADE POR GENERO = AVERAGE(tb_rh[IDADE]) 
```

```javascript
GENERO = COUNT(tb_rh[NOME])
```

### 📌**Colunas Calculadas**  
Além das medidas, foram criadas três colunas calculadas, cada uma utilizando diferentes funcionalidades do DAX.

**`ANO`** → Extrai o ano de admissão do funcionário.
```javascript
ANO = YEAR(tb_rh[DATA ADIMISSAO]) 
```

**`FUNCIONARIO`** → Classifica o funcionário como "CARO" ou "COMUM" com base no salário.
```javascript
FUNCIONARIO = IF(tb_rh[SALARIO] >= 5000, "FUNCIONARIO CARO", "FUNCIONARIO COMUM")
```

**`ESTADOS`** → Converte as siglas dos estados para seus nomes completos.

```javascript
ESTADOS = IF(tb_rh[FILIAL] = "RJ", "RIO DE JANEIRO", 
          IF(tb_rh[FILIAL] = "SP", "SÂO PAULO",
          IF(tb_rh[FILIAL] = "MG", "MINAS GERAIS")))
```

