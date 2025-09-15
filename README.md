# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:15-09-2025
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
cdex3.l
```
%{
#include "y.tab.h"
%}

digit   [0-9]
%%
[ \t\n]+        ; // Ignore whitespace
{digit}+        { yylval = atoi(yytext); return NUMBER; }
[\+\-\*/]       { return *yytext; }
\(              { return '('; }
\)              { return ')'; }
.               { return 0; }
%%
int yywrap() { return 1; }
```
cdex3.y
```
%{
#include <stdio.h>
#include <stdlib.h>
void yyerror(const char *s);
int yylex(void);
%}

%token NUMBER

%%
expr:   expr '+' term
        | expr '-' term
        | term
        ;

term:   term '*' factor
        | term '/' factor
        | factor
        ;

factor: '(' expr ')'
        | NUMBER
        ;

%%

void yyerror(const char *s) {
    printf("Invalid arithmetic expression.\n");
}

int main() {
    printf("Enter an arithmetic expression: ");
    if (yyparse() == 0)
        printf("Valid arithmetic expression.\n");
    return 0;
}
```
# OUTPUT
name.l
<img width="1401" height="760" alt="Screenshot 2025-09-13 110056" src="https://github.com/user-attachments/assets/4a383789-5de7-42ed-b017-166c375ad5e0" />
cdex3.l
<img width="957" height="408" alt="image" src="https://github.com/user-attachments/assets/33670763-705c-42a1-9275-03106c4ad954" />
<img width="955" height="412" alt="image" src="https://github.com/user-attachments/assets/1f67948f-e4da-45ef-bd27-75f3c2c38a7d" />

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
