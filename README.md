# analisador-recursivo
Implementação Python de um analisador descendente recursivo para analisar expressões matemáticas.




Anderson Cherubim | Ciência da Computação
Implementar um analisador recursivo descendente para avaliar expressões aritméticas, com as seguintes operações:
Adição +
Subtração -
Multiplicação *
Divisão /
Resto da Divisão Inteira%
Potenciação ^
A linguagem deve respeitar a prioridade natural dos operadores, e deve aceitar a inversão de prioridade mediante o uso de parênteses - "(" e ")".
Gramática final implementada (após aplicação das regras de remoção de recursões à esquerda):
E -> TE '
E '-> + TE' | & | -TE '
T -> PT '
T '-> * PT' | & | / PT '| % PT '
P -> FP '
P '-> ^ F | E
F -> (E) | eu ia
"" "

def  getNumberIndex ( inp ):
    "" "Retorna o índice do fim do valor numérico na string" ""
    índice  =  0
    para  i  no  intervalo ( 0 , len ( inp )):
        se  inp [ i ]. isdigit ():
            índice  =  índice  +  1
        mais :
            pausa 
     índice de retorno

def  skip_spaces ( inp ):
    "" "Ignora espaços em branco no inicio da entrada." ""
    return  inp . lstrip ()

def  E ( inp ):
    inp  =  skip_spaces ( inp )
    imprimir ( "E -> T E '" )
    inp , v1  =  T ( inp )
    inp , v2  =  Eprime ( inp , v1 )
    return ( inp , v2  se  v2  não for  None else v1 )   

def  Eprime ( inp , valor ):
    inp  =  skip_spaces ( inp )
    imprimir ( "E '-> + TE' | & | -T E '" )
    if  inp [ 0 : 1 ] ==  '+' :
        inp , v1  =  T ( inp [ 1 :])
        inp , v2  =  Eprime ( inp , valor  +  v1 )
        return ( inp , v2  se  v2  não for  nenhum outro valor )   
    elif  inp [ 0 : 1 ] ==  '-' :
        inp , v1  =  T ( inp [ 1 :])
        inp , v2  =  Eprime ( inp , valor  -  v1 )
        return ( inp , v2  se  v2  não for  nenhum outro valor )   
    mais :
        retorno ( inp , valor )

def  T ( inp ):
    inp  =  skip_spaces ( inp )
    imprimir ( "T -> P T '" )
    inp , v1  =  P ( inp )
    inp , v2  =  Tprime ( inp , v1 )
    return ( inp , v2  se  v2  não for  None else v1 )   

def  Tprime ( inp , valor ):
    inp  =  skip_spaces ( inp )
    imprimir ( "* PT '| & | / PT' |% P T '" )
    if  inp [ 0 : 1 ] ==  '*' :
        inp , v1  =  P ( inp [ 1 :])
        inp , v2  =  Tprime ( inp , valor  *  v1 )
        return ( inp , v2  se  v2  não for  nenhum outro valor )   
    elif  inp [ 0 : 1 ] ==  '/' :
        inp , v1  =  P ( inp [ 1 :])
        inp , v2  =  Tprime ( inp , valor  /  v1 )
        return ( inp , v2  se  v2  não for  nenhum outro valor )   
    elif  inp [ 0 : 1 ] ==  '%' :
        inp , v1  =  P ( inp [ 1 :])
        inp , v2  =  Tprime ( inp , valor  %  v1 )
        return ( inp , v2  se  v2  não for  nenhum outro valor )   
    mais :
        retorno ( inp , valor )

def  P ( inp ):
    inp  =  skip_spaces ( inp )
    imprimir ( "P -> F P '" )
    inp , v1  =  F ( inp )
    inp , v2  =  Pprime ( inp , v1 )
    return ( inp , v2  se  v2  não for  None else v1 )   

def  Pprime ( inp , valor ):
    inp  =  skip_spaces ( inp )
    imprimir ( "P '-> ^ F | &" )
    if  inp [ 0 : 1 ] ==  '^' :
        inp , v1  =  F ( inp [ 1 :])
        retorno ( inp , valor  **  v1 )
    mais :
        retorno ( inp , nenhum )

def  F ( inp ):
    inp  =  skip_spaces ( inp )
    imprimir ( "F -> (E) | id" )
    if  inp [ 0 : 1 ] ==  '(' :
        inp , valor  =  E ( inp [ 1 :])
        inp  =  skip_spaces ( inp )
        if  inp [ 0 : 1 ] ! =  ')' :
            levantar  Exception ( "Esperado '(', escrever '{}'" . format ( inp [ 0 ]))
        retorno ( inp [ 1 :], valor )
    mais :
        maxIndex  =  getNumberIndex ( inp )
        valor  =  inp [: maxIndex ]
        return ( inp [ maxIndex :], int ( valor ))

if  __name__  ==  "__main__" :
    enquanto  verdadeiro :
        entrada  =  input ( "Digite uma expressao:" )
        se  não  for entrada :
            pausa
        inp , resultado  =  E ( entrada )
        imprimir  inp
        se  inp :
            raise  Exception ( "A entrada nao foi completamente utilizado." )
        imprimir ( "Resultado:" , resultado )
