## **Objetivo**

Criar um banco de dados para gerenciar um sistema de consultas médicas, envolvendo as entidades **Médicos**, **Pacientes** e **Consultas**. Além disso, foi implementada uma consulta SQL para listar médicos e os pacientes que foram atendidos por eles, incluindo médicos que não possuem registros de consultas.

## **Cenário de Modelagem de Dados**

O cenário proposto envolve o seguinte modelo:

1. **Médicos**: A tabela armazena dados dos médicos, como seu nome e especialidade. Relaciona-se com a tabela **Consultas** por meio de um relacionamento 1:N (um para muitos), pois cada médico pode atender vários pacientes em diferentes consultas.

2. **Pacientes**: A tabela armazena informações sobre os pacientes, incluindo nome e idade. Relaciona-se com a tabela **Consultas** por meio de um relacionamento N:N (muitos para muitos), pois um paciente pode ter várias consultas e cada consulta pode envolver diferentes médicos.

3. **Consultas**: A tabela intermediária registra as consultas realizadas, vinculando médicos e pacientes. Esta tabela faz a relação 1:N entre médicos e consultas e a relação N:N entre pacientes e consultas.

### **Relacionamentos**
- **Relação 1:N (Médicos e Consultas)**: Cada médico pode ter várias consultas, mas cada consulta está associada a um único médico.
- **Relação N:N (Consultas e Pacientes)**: Cada consulta pode envolver um ou mais pacientes, e um paciente pode ter várias consultas.

## **Criação das Tabelas**

Para implementar o banco de dados, as tabelas foram criadas com os seguintes comandos SQL:

![image](https://github.com/user-attachments/assets/c72e9b02-dfea-40eb-a3a5-81dbb19fc764)

## **Inserção de Dados**

Após a criação das tabelas, os dados de exemplo foram inseridos para testar o sistema, com médicos, pacientes e consultas, conforme o exemplo abaixo:

![image](https://github.com/user-attachments/assets/495cb75a-1507-442a-93e6-0a13d43107c0)

## **Consulta SQL Complexa**

A consulta SQL foi criada para listar todos os médicos e os pacientes que foram atendidos por eles, incluindo médicos que não possuem registros de consultas. A consulta também lida com a relação 1:N entre médicos e consultas e a relação N:N entre pacientes e consultas.

A consulta SQL utilizada foi a seguinte:

![image](https://github.com/user-attachments/assets/4a5afb62-40ee-4cf5-bd0c-87ff45883e01)

### **Explicação da Consulta**
- **LEFT JOIN** foi usado para garantir que todos os médicos sejam listados, mesmo aqueles que não possuem consultas associadas.
- A tabela **Consultas** faz a junção entre os médicos e os pacientes, permitindo que os resultados exibam os pacientes atendidos por cada médico.
- Caso o médico não tenha pacientes associados, o nome do paciente será exibido como `NULL`.

### **Resultado Esperado**

O resultado esperado da consulta, para os dados inseridos, seria o seguinte:

![image](https://github.com/user-attachments/assets/e2652ced-5035-4171-a3a1-15b700e9951d)

## **Equação da Álgebra Relacional**

A consulta SQL acima pode ser representada na álgebra relacional da seguinte forma:

``` 
π M.Nome do Médico, P.Nome do Paciente (
  (Médicos ⨝ M.ID=Consultas.MedicoID Consultas) ⨝ Consultas.PacienteID=P.ID Pacientes
)
```

### **Explicação da Equação da Álgebra Relacional**
- **π** (projeção) é usada para selecionar as colunas "Nome do Médico" e "Nome do Paciente".
- **⨝** (junção) é usada para combinar as tabelas **Médicos**, **Consultas** e **Pacientes** de acordo com suas chaves de relacionamento.
- O operador de junção garante que a consulta selecione as instâncias onde a relação entre médico e paciente é atendida, com médicos sem pacientes associados sendo incluídos devido ao uso do **LEFT JOIN**.
