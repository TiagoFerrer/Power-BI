# **DESAFIO DE PROJETO**
### COLETA E PROCESSAMENTO DE DADOS COM POWER BII
#### Objetivo Geral
1. Configurar o setup de Banco de Dados na Azure
2. Popupar o servidor com script
3. Integrar o MySQL com Power BI
4. Realizar as transformações necessárias

#### Setup do Banco de Dados na Azure
Nesta primeira etapa foi criada uma conta gratuita na Azure e nessa conta foi criado um Servidor flexível do Banco de Dados do Azure para MySQL, só foram realizadas as configurações básicas, para os testes do projeto.
Também foi criada uma conexão no Workbench do MySQL com o Banco de Dados da Azure para isso foi necessário alguns dados da Azure:
* Nome do servidor
* Nome de logon do administrador
* Fazer o download do arquivo do CA SSL

#### Arquivos para popular o Banco de Dados
[Arquivo para a  criação das tabelas](https://github.com/TiagoFerrer/Power-BI/blob/main/DIO/Desafio/script_bd_company.sql)
[Arquivo para a inserção dos dados](https://github.com/TiagoFerrer/Power-BI/blob/main/DIO/Desafio/insercao_de_dados_e_queries_sql.sql)

#### Integração do Power BI co MySQL
Para fazer a conexão do Banco de Dados MySQL e o Power BI basta selecionar "Obter dados > Mais... > Banco de Dados MySQL", clicar em conectar. Na próxima tela, preencher os dados com Servidor e o nome do Banco de Dados, não sendo necessário preencher os outros campos. Com isso os dados serão carregados no Power BI.

#### Realizar as transformações necessárias
Ao carregar os dados foi verificado que os cabeçalhos foram carregados corretamente, mas alguns dados foram carregados de forma incorreta:
a) Alterado para o tipo texto
| **Tabela** | **Coluna** |
|---|---|
| Departamento | Dnumber |
| Depart_Local | Dnumber |
| Funcionario | Dno |
| Projeto | Dnum |
| Works_On | Pno |

b) Alterado para o tipo número decimal fixo
| **Tabela** | **Coluna** |
|---|---|
| Funcionario | Salary |

Após as alteração dos tipos de dados, foram verificados os dados quanto a valores null, foi encontrado um único valor nulo na coluna **Super_ssn** da tabela **Funcionario**, foi verificado que não é necessária a remoção da linha, o dado é nulo pois o mesmo é o gerente não tendo um superior.

Também na tabela **Funcionario** foi feita a divisão da coluna **Address** em 4 colunas Number, Street, City e State, para melhorar a análise dos dados.

Foi feita a mescla das consultas employee e departament e foi criada uma outra tabela employees com os dados dessa mescla, as colunas desnecessárias foram eliminadas.

No SQL foi feita a junção dos dados dos colaboradores e dos seus respectivos gerentes. A querry abaixo foi executada no MySQL e gerou os dados requeridos.  

```sh
use azure_company;  

SELECT  
    G.Fname AS manager_Fname,
    G.Minit AS manager_Minit,
    G.Lname AS manager_Lname,
    F.Fname,
    F.Minit,
    F.Lname
FROM
    Funcionario AS F
LEFT JOIN Funcionario AS G
    ON F.super_ssn = G.ssn
ORDER BY G.Fname;
```
Também foi escrita uma consulta em SQL para agrupar os dados e saber quantos colaboradores existem por gerente
```sh
use azure_company;

SELECT
    manager_first_name,
    COUNT(*) AS colaboradores
FROM (
    SELECT
        F.Fname,
        F.Lname,
        G.Fname AS manager_first_name,
        G.Lname AS manager_last_name,
        G.ssn AS manager_ssn
    FROM
        Funcionario AS F
    INNER JOIN Funcionario AS G
        ON F.super_ssn = G.ssn
    ) AS Funcionario
GROUP BY
    manager_ssn
HAVING
    COUNT(*) > 0;
```
Após fazer todas as transformações no Power Query do Power BI, foi confeccionado um [Relatório no Power BI.](https://github.com/TiagoFerrer/Power-BI/blob/main/DIO/Desafio/Desafio%20de%20Projeto.pbix)
