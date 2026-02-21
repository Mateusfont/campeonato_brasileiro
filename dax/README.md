# Dax do projeto
## % POS_BOLA	
''AVERAGE(f_Estatistica[posse_de_bola])''
Cartões amarelo	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[cartao] = "Amarelo"
) + 0
Cartões na prorrogação	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Prorrogacao] = "Prorrogação P.T" ||
    f_Cartoes[Prorrogacao] = "Prorrogação S.T"
) + 0
Cartões no primeiro tempo	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Etapa] = "Primeiro Tempo"
) + 0
Cartões no segundo tempo	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[Etapa] = "Segundo Tempo"
) + 0
Cartões vermelho	
CALCULATE(
    COUNTROWS(f_Cartoes),
    f_Cartoes[cartao] = "Vermelho"
) + 0
CHUTES_GOL	
SUM(f_Estatistica[chutes_no_alvo])
Clube com maior quantidade de vitorias	
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

Média de cartões por jogo	
VAR Quantidade_jogos_disputados = 
    DISTINCTCOUNT(f_Cartoes[partida_id])
VAR Quantidade_cartoes = 
    [Cartões amarelo] + [Cartões vermelho]
RETURN
Quantidade_cartoes / Quantidade_jogos_disputados
Partidas	
DISTINCTCOUNT(f_Cartoes[partida_id]) + 0
POS_BOLA	
SUM(f_Estatistica[posse_de_bola])
PREC_PASSES	
AVERAGE(f_Estatistica[precisao_passes])
QTD_ESCANTEIOS	
 SUM(f_Estatistica[escanteios])
QTD_FALTAS	
SUM(f_Estatistica[faltas])
QTD_GOLS	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Gol Normal"
)
QTD_GOLS_CONTRA	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Gol Contra"
)
QTD_GOLS_PENALTY	
CALCULATE(
    COUNTROWS(f_Gols),
    f_Gols[tipo_de_gol] = "Pênalti"
)
QTD_IMPEDIMENTOS	
SUM(f_Estatistica[impedimentos])
QTD_PARTIDAS	
DISTINCTCOUNT(f_Gols[partida_id])
QTD_VITORIAS	
COUNT(f_Base_Dados[vencedor])
Total de cartões	
[Cartões amarelo] + [Cartões vermelho] + 0
