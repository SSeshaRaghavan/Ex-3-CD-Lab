# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
name.l
```
%{
    #include "y.tab.h"
%}

%%
[a-zA-Z]+  { yylval = strdup(yytext); return NAME; }
[ \t\n]    { /* Ignore whitespace */ }
.          { printf("Invalid character: %s\n", yytext); }

%%

int yywrap() { return 1; }
```
name.y
```
%{
    #include <stdio.h>
    #include <stdlib.h>
    extern int yylex();
    void yyerror(const char *s);
%}

%token NAME

%%
start: NAME { printf("Hello, %s!\n", $1); }
     ;

%%
void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

int main() {
    printf("Enter your name: ");
    yyparse();
    return 0;
}
```
CDEXPR3.l
```

```
# OUTPUT

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
