# 10-jflex-avalia-o-identificador

## Instalação:
`sudo apt update`

`sudo apt install jflex`

# Alguns métodos e variáveis disponíveis:
 * **int yyline**: armazena o número da linha atual.
 * **int yycolumn**: armazena o número da coluna atual na linha atual.
 * **String yytext()**: método que retorna a sequência de caracteres que foi casada com a regra.
 * **int yylength()**: método que retorna o comprimento da sequência de caracteres que foi casada com a regra.

 Para se usar esses métodos e variáveis, é necessário incluir as diretivas abaixo na seção 2:
 * **%line**: permite usar yyline.
 * **%column**: permite usar yycolumn.

 **OBS**: a diretiva "%class" permite alterar o nome padrão da classe Yylex.java.
 
 Exemplo:
 
 * **%class AnalisadorLexico**
 
 ou
 
 * **%class Scanner**

# Exemplo: 

## Arquivo: exemplo.flex

<pre>
/* Alguns métodos e variáveis disponíveis:
 * int yyline: armazena o número da linha atual.
 * int yycolumn: armazena o número da coluna atual na linha atual.
 * String yytext(): método que retorna a sequência de caracteres que foi casada com a regra.
 * int yylength(): método que retorna o comprimento da sequência de caracteres que foi casada com a regra.
 */

/* Definição: seção para código do usuário. */


%%

/* Opções e Declarações: seção para diretivas e macros. */

// Diretivas:
%standalone    // Execução independente do analisador sintático.
%line          // Permite usar yyline.
%column        // Permite usar yycolumn.
%class Scanner // Troca o nome da classe Yylex para Scanner.

%{  // Código que será incluído no analisador léxico:
    public String getLexema() {
        return yytext(); // Apenas retorna o valor de yytext().
    }
%}

// Macros:
letra = [a-zA-Z]
numero = [0-9]
digito = {numero}+
identificador = ( {letra} | \$ )( {letra} | {digito} | \_)*

%%

/* Regras e Ações Associadas: seção de instruções para 
 * o analisador léxico. 
 */

{identificador} {System.out.println("\n -> Encontrei um <Token: IDENTIFICADOR, Lexema: " + getLexema() + ", Tamanho: " + yylength() + ", Linha: " + yyline + ", Coluna: " + yycolumn + ">");}
</pre>

## Arquivo: entrada01.txt:
<pre>
abcde
$abc
$
$_
abc_123
123abcd
456abc
abc$
abc_
7890
_abc
</pre>

## Execução:
`jflex exemplo.flex`

`javac Scanner.java`

`java Scanner entrada01.txt`

## Jogando a saída num arquivo:
`java Scanner entrada01.txt > saida01.txt`


# Git
`git add .`

`git commit -m "Exemplo"`

`git push`