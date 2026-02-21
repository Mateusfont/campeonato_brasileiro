# Dax do projeto
## % POS_BOLA	
```DAX
AVERAGE(f_Estatistica[posse_de_bola])
```
## CARTÕES AMARELO
```DAX	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[cartao] = "Amarelo"
) + 0
```
## CARTÕES NA PRORROGAÇÃO
```DAX	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Prorrogacao] = "Prorrogação P.T" ||
    f_Cartoes[Prorrogacao] = "Prorrogação S.T"
) + 0
```
## CARTÕES NO PRIMEIRO TEMPO
```DAX	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Etapa] = "Primeiro Tempo"
) + 0
```
## CARTÕES NO SEGUNDO TEMPO
```DAX	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Etapa] = "Segundo Tempo"
) + 0
```
## CARTÕES VERMELHO
```DAX	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[cartao] = "Vermelho"
) + 0
```
## CHUTES_GOL
```DAX	
SUM(f_Estatistica[chutes_no_alvo])
```
## CLUBE COM A MAIOR QUANTIDADE DE VITÓRIAS
```DAX	
var Tabela_Vitorias = 
    SUMMARIZE(
        FILTER(f_Base_Dados, f_Base_Dados[vencedor] <> "Empate"),
        f_Base_Dados[vencedor],
        "Total Partidas Ganhas",
        COUNT(f_Base_Dados[vencedor])
    )
var Clube_Maior_Quantidade_Vitorias = 
    TOPN(
        1,
        Tabela_Vitorias,
        [Total Partidas Ganhas],
        DESC
    )
return
    SELECTCOLUMNS(
        Clube_Maior_Quantidade_Vitorias,
        "Clube",
        f_Base_Dados[vencedor]
    )
```
## MÉDIA DE CARTÕES POR JOGO
```DAX
VAR Quantidade_jogos_disputados = 
    DISTINCTCOUNT(f_Cartoes[partida_id])
VAR Quantidade_cartoes = 
    [Cartões amarelo] + [Cartões vermelho]
RETURN
Quantidade_cartoes / Quantidade_jogos_disputados
```
## PARTIDAS
```DAX	
DISTINCTCOUNT(f_Cartoes[partida_id]) + 0
```
## POS_BOLA
```DAX	
SUM(f_Estatistica[posse_de_bola])
```
## PREC_PASSES
```DAX	
AVERAGE(f_Estatistica[precisao_passes])
```
## QTD_ESCANTEIOS
```DAX	
 SUM(f_Estatistica[escanteios])
```
## QTD_FALTAS
```DAX	
SUM(f_Estatistica[faltas])
```
## QTD_GOLS
```DAX	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Gol Normal"
)
```
## QTD_GOLS_CONTRA
```DAX	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Gol Contra"
)
```
## QTD_GOLS_PENALTY
```DAX	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Pênalti"
)
```
## QTD_IMPEDIMENTOS
```DAX	
SUM(f_Estatistica[impedimentos])
```
## QTD_PARTIDAS
```DAX	
DISTINCTCOUNT(f_Gols[partida_id])
```
## QTD_VITORIAS
```DAX	
COUNT(f_Base_Dados[vencedor])
```
## TOTAL DE CARTÕES
```DAX	
[Cartões amarelo] + [Cartões vermelho] + 0
```