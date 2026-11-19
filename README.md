# Prova2-Sistemas-Distribu-dos

EVIDENCIA 2

PS C:\Users\aluno\AppData\Local\Programs\Microsoft VS Code> & 'C:\Program Files\Python313\python.exe' 'c:/Users/aluno/Desktop/Simulado_Dsitribuidos/central_pedidos.py'
=== CENTRAL DE PEDIDOS ===
Pedidos confirmados: [101, 102, 103]
Estoque principal: 7
Replica antes: 10
Replica depois: 7
Consulta após falha: REPLICA 7
PS C:\Users\aluno\AppData\Local\Programs\Microsoft VS Code> 
////////////////////////////////////////////////////////////////////////////////////////////////////////////////

EVIDENCIA 2

FOI ALTERADO DE 3 PARA 2 A MAXIMO_SIMULTANEO 
<img width="228" height="70" alt="image" src="https://github.com/user-attachments/assets/a56950d0-8739-4660-8c11-e90ec24eb064" />

MAXIMO_SIMULTANEO = 3 FOI ALTERADO PARA 2 = MAXIMO_SIMULTANEO = 2

////////////////////////////////////////////////////////////////////////////////////////////////////////////////

EVIDENCIA 3 

FOI ALTERADO A FUNÇÃO SINCRONIZAR ONDE ESTAVA ERRADO A  replica["estoque"] = replica["estoque"] 
<img width="366" height="69" alt="image" src="https://github.com/user-attachments/assets/3e6efadd-1565-473b-8aac-c3ec948cbb7b" />

Foi alterado 
def sincronizar():
    replica["estoque"] = replica["estoque"]

para def sincronizar():
    replica["estoque"] = estoque["estoque"]
    
////////////////////////////////////////////////////////////////////////////////////////////////////////////////

EVIDENCIA 5 






////////////////////////////////////////////////////////////////////////////////////////////////////////////////
ETAPA 5 ANALISE TÉCNICA 

QUESTÃO 1 - O SEMAFARO TEM A FUNÇÃO DE DE DAR A SEQUENCIA NA ORDEM DE PROCESSAMENTO DOS PEDIDOS 

QUESTÃO 2 - 

QUESTÃO 3 -

QUESTÃO 4 -

QUESTÃO 5 -




