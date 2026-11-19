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

No terminal resultado Estoque principal: 10 apos a correção Estoque principal: 7

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
    
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

EVIDENCIA 5

=== CENTRAL DE PEDIDOS ===
Pedidos confirmados: [101, 102, 103]
Estoque principal: 7
Replica antes: 10
Replica depois: 7
Consulta após falha: REPLICA 7

import threading
import time

principal = {"online": True, "estoque": 10}
replica = {"online": True, "estoque": 10}

pedidos_confirmados = []

MAXIMO_SIMULTANEO = 2

semafaro = threading.Semaphore(MAXIMO_SIMULTANEO)
TRAVA = threading.Lock()

def processar_pedido(numero):
    with semafaro:
        time.sleep(0.1)

        with TRAVA:
            if principal["estoque"] > 0:
                principal["estoque"] -= 1
                pedidos_confirmados.append(numero)

def sincronizar():
    replica["estoque"] = principal["estoque"]

def consultar_estoque():
    if principal["online"]:
        return "PRINCIPAL", principal["estoque"]

    if replica["online"]:
        return "REPLICA", replica["estoque"]

    return "INDISPONIVEL", None

print("=== CENTRAL DE PEDIDOS ===")

trabalhadores = [
    threading.Thread(
        target=processar_pedido,
        args=(numero,)
    )
    for numero in [101, 102, 103]
]

for trabalhador in trabalhadores:
    trabalhador.start()

for trabalhador in trabalhadores:
    trabalhador.join()

print("Pedidos confirmados:", sorted(pedidos_confirmados))
print("Estoque principal:", principal["estoque"])

print("Replica antes:", replica["estoque"])

sincronizar()

print("Replica depois:", replica["estoque"])

principal["online"] = False

nome, estoque = consultar_estoque()

print("Consulta após falha:", nome, estoque)


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

ETAPA 5 ANALISE TÉCNICA 

QUESTÃO 1 - Qual é a função do semáforo no processamento dos pedidos?O semáforo controla a quantidade de pedidos processados ao mesmo tempo,evitando sobrecarga no sistema

QUESTÃO 2 -  Por que é necessário sincronizar os dados entre o servidor principal e a réplica?Para garantir que o servidor principal e a réplica tenham as mesmas informações de estoque, evitando dados desactualizados

QUESTÃO 3 - O que significa tolerância a falhas e como ela aparece neste programa?É a capacidade do sistema de continuar funcionando mesmo quando ocorre uma falha. No programa, aparece quando o servidor principal falha e a réplica assume processamento.

QUESTÃO 4 -  Para que serve o "Lock" no programa e como o controle de acessoaos recursos ajuda a prevenir problemas de concorrência?O Lock controla o acesso aos recursos compartilhados, evitando que duas tarefasalterem os mesmos dados ao mesmo tempo e causem erros

QUESTÃO 5 -Considerando a sequência de eventos, a sincronização do estoquedeve acontecer antes ou depois do processamento dos pedidos? Explique arelação de causalidade.A sincronização deve acontecer depois do processamento dos pedidos, poisprimeiro o estoque é atualizado no servidor principal e depois a réplica recebe osnovos valores. Assim, os dois servidores permanecem sincronizados




