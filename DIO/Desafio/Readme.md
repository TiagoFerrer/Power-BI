# **DESAFIO DE PROJETO**
### COLETA E PROCESSAMENTO DE DADOS COM POWER BII
#### Objetivo Geral
1. Configurar o setup de banco de dados na Azure
2. Popupar o servidor com script
3. Integrar o MySQL com Power BI
4. Realizar as transformações necessárias

#### Realizar as transformações necessárias
Ao carregar os dados foi verificado que os cabeçalhos foram carregados corretamente, mas alguns dados foram carregados de forma incorreta:
a) Alterado para o tipo texto
| **Tabela** | **Coluna** |
|---|---|
| Departament | Dnumber |
| dept_locations | Dnumber |
| employee | Dno |
| project | Dnum |
| works_on | Pno |
b) Alterado para o tipo número decimal fixo
| **Tabela** | **Coluna** |
|---|---|
| employee | Salary |

Após as alteração dos tipos de dados, foram verificados os dados quanto a valores null, foi encontrado um único valor nulo na coluna **Super_ssn** da tabela **employee**, foi verificado que não é necessária a remoção da linha, o dado é nulo pois o mesmo é o gerente não tendo um superior.

Também na tabela **employee** foi feita a divisão da coluna **Address** em 4 colunas Number, Street, City e State, para melhorar a análise dos dados.

Foi feita a mescla das consultas employee e departament e foi criada uma outra tabela employees com os dados dessa mescla, as colunas desnecessárias foram eliminadas.

No SQL foi feita a junção dos dados dos colaboradores e dos seus respectivos gerentes. A querry abaixo foi executada no MySQL e gerou os dados requeridos.

> use azure_company;
> SELECT
>    m.Fname AS manager_Fname,
>    m.Minit AS manager_Minit,
>  m.Lname AS manager_Lname,
>  e.Fname,
>  e.Minit,
>  e.Lname
> FROM
>  employee AS e
>  LEFT JOIN employee AS m
>    ON e.super_ssn = m.ssn
> ORDER BY m.Fname;

Também foi escrita uma consulta em SQL para agrupar os dados e saber quantos colaboradores existem por gerente
> use azure_company;
SELECT
  manager_first_name,
  COUNT(*) AS colaboradores
FROM
  (
    SELECT
      e.Fname,
      e.Lname,
      m.Fname AS manager_first_name,
      m.Lname AS manager_last_name,
      m.ssn AS manager_ssn
    FROM
      employee AS e
    INNER JOIN employee AS m
      ON e.super_ssn = m.ssn
  ) AS employee
GROUP BY
  manager_ssn
HAVING
>  COUNT(*) > 0
