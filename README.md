# COALESCE-LEFT-JOIN
Suponha que você tenha duas tabelas, table1 e table2, e você queira fazer um LEFT JOIN entre elas e aplicar a função COALESCE em uma coluna da table2.

SELECT t1.*,
       COALESCE(t2.column2, 'N/A') AS column2_coalesced
FROM table1 t1
LEFT JOIN table2 t2 ON t1.key = t2.foreign_key;


Neste exemplo:
table1 é a tabela da esquerda no LEFT JOIN.
table2 é a tabela da direita no LEFT JOIN.
t1 e t2 são aliases para table1 e table2, respectivamente.
key é a chave primária na table1.
foreign_key é a chave estrangeira na table2.
COALESCE(t2.column2, 'N/A') retorna o valor da coluna column2 da table2, mas se for nulo, retorna 'N/A'.
Essa consulta retornará todas as linhas da table1, e para cada linha, tentará fazer uma correspondência com a table2 usando as chaves. Se não houver uma correspondência, as colunas de table2 retornarão NULL, mas a função COALESCE garantirá que você obtenha um valor padrão ('N/A' neste caso) em vez de NULL.


SELECT SIMs.*, 
       COALESCE(Usuarios.usu_Nome, 'Sem destinatário') AS Nome_Destinatario,
       COALESCE(sim_Prejuizo, 0) AS sim_Prejuizo,
       Setores.set_Setor,
       COALESCE(Empresas.emp_RazaoSocial, 'MASTER SUL COMEX LTDA - ME') AS Razao_Social_Empresa
FROM tableSIMs AS SIMs
LEFT JOIN tableUsuarios AS Usuarios ON SIMs.usu_IdDestinatario = Usuarios.usu_Id
LEFT JOIN tableSetores AS Setores ON SIMs.set_Id = Setores.set_Id
LEFT JOIN tableEmpresas AS Empresas ON SIMs.emp_CNPJ = Empresas.emp_CNPJ;
