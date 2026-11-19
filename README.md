# prova2simuladosistemasdistribuidos
EVIDENCIA 1 - Primeira execução.

===CENTRAL DE PEDIDOS===
Limite Simultaneo: 3
Estoque inicial: 10
Pedidos confirmados [101, 102, 103]
Replica antes: 10
Replica depois: 10
Consulta apos falha: INDISPONIVEL None

O Código foi copiado com sucesso e executado como requerido

PROBLEMA A
EVIDENCIA 2 - Concorrência.

===CENTRAL DE PEDIDOS===
Limite Simultaneo: 2
Estoque inicial: 10
Pedidos confirmados [101, 102, 103]
Replica antes: 10
Replica depois: 10
Consulta apos falha: INDISPONIVEL None

Realizei uma pequena edição no código:
MAXIMO_SIMULTANEO =
Editando-o de 3 para 2

PROBLEMA B
EVIDENCIA 3 - Sincronização.
===CENTRAL DE PEDIDOS===
Limite Simultaneo: 2
Estoque inicial: 10
Pedidos confirmados [101, 102, 103]
Replica antes: 10
Replica depois: 7
Consulta apos falha: INDISPONIVEL None

Na função sincronizar havia uma pequena imprecisão no código onde ele repetia o mesmo comando 2 vezes para o mesmo servidor.
ANTES:
  def sincronizar():
    replica["estoque"] = REPLICA["estoque"]  

DEPOIS:
def sincronizar():
    replica["estoque"] = principal["estoque"]

PROBLEMA C
EVIDENCIA 4 - Tolerãncia a falhas
===CENTRAL DE PEDIDOS===
Limite Simultaneo: 2
Estoque inicial: 10
Pedidos confirmados [101, 102, 103]
Replica antes: 10
Replica depois: 7
Consulta apos falha: REPLICA 7

Havia uma má construção do código onde ele passava o "if" pelo principal, e passava denovo pelo mesmo servidor. Este erro foi corrigido fazendo o if passar pelo servidor réplica antes do "return INDISPONIVEL"

VALIDAÇÃO DO PROGRAMA
EVIDENCIA 5 - Validação completa.

===CENTRAL DE PEDIDOS===
Limite Simultaneo: 2
Estoque inicial: 10
Pedidos confirmados [101, 102, 103]
Replica antes: 10
Replica depois: 7
Consulta apos falha: REPLICA 7

Por fim o código rodou perfeitamente, cumprindo todas requisições de sincronização, semáforo e tolerância a falhas.

ANÁLISE TÉCNICA
Questão 1: Qual a função do semáforo no procesamento dos pedidos?
O semáforo no processamento tem como função delimitar quantos processos podem ser executados simultaneamente no sistema evitando, assim, problemas de concorrencia.

Questão 2: Por que é necessário sincronizar os dados entre o servidor principal e a réplica?
Os dados nos servidores precisam estar sincronizados para que não haja incongruência entre eles, em caso de que um servidor falha, o segundo precisa estar em conformidade com o primeiro para que não ocorra vendas sem estoque, por exemplo.

Questão 3: O que significa tolerância a falhas e como ela aparece nestre programa?
Tolerância a falhas tem o papel de garantir que o servidor continue em funcionamento mesmo que algum problema ocorra, um servidor saia do ar, ou qualquer coisa do tipo. No caso deste programa ele aparece no servidor backup, intitulado "replica", ele garante que mesmo que, de alguma forma, o principal falhe, o sistema continue em devido funcionamento.

Questão 4: Para que serve o Lock no programa e como o controle de acesso aos recursos ajuda a prevenir problemas de concorrência?
O Lock serve o propósito de fazer com que um processamento ocorra somente quando um anterior terminar. Ele é imprescindivel pois garante que dois processos não sejam executados ao mesmo tempo, causando divergências no estoque.

Questão 5: Considerando a sequência de eventos, a sincronização do estoque deve acontecer antes ou depois do processamento dos pedidos? Explique a relação de causalidade.
A sincronização do estoque deve ser realizada após o processamento dos pedidos. Em sequência o pedido é realizado, a sincronização é feita, atualizando a nova disponibilidade no estoque, e garantindo que o sistema tenha sempre controle de quantos produtos tem á disposição. 
