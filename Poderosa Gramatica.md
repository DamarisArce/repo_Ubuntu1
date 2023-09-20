```BNF
ini::= entradas
;

entradas ::= "void" "main" "()" "{" sentencias:a "}"
            
            |archivo_json
            
;

sentencias ::= sentencias sentencia
              |sentencias error 
              |sentencia  
              |expresion  
; 

funciones ::= "void" ID "(" <expresion> ")" "{" c "}"
             |"void" ID"()" "{" sentencias "}" 
        
;

funcion_globales ::= "void" "DefinicionGlobales" "()" "{"sentencias "}"
    
;

sentencia ::= sentencia_print
            | sentencia_declaracion
            | sentencia_globales
            | sentenciaIf
            | sentenciaFor
            | sentenciaSwitch
            | sentenciaWhile
            | sentenciaDoWhile
            | funciones
            |funcion_globales
;

sentenciaIf ::= "if" "("expresion ")"{
	<Sentencias>
}[sentenciaElse];

sentenciaElse ::= "else if" "("expresion ")"{
	<Sentencias>
}[sentenciaElse];
		| "else" {
	<Sentencias>
};


sentenciaFor ::="for" (tipo_dato ID "=" expresion; expresion; ID++ ){
<Sentencias>
};

sentenciaSwitch ::= "switch" "(" ID ")"{
sentenciasCase
}

sentenciasCase ::= "case" expresion: 
<Sentencias>
"break;"[sentenciasCase]
	|"default": 
<Sentencias>
"break;"

sentenciaWhile ::="while" "(" expresion ")" {
<Sentencias>
};

sentenciaDoWhile ::="do" {
<Sentencias>
}"while" "(" expresion ")" ";"



sentencia_print ::= "Console" "." "write" "(" expresion ")" ";"
;

sentencia_declaracion ::= tipo_dato ID "=" expresion ";" 
                        |tipo_dato ID ";"    
                        |tipo_dato "[]" "=" lista ";"
;

lista ::= "{" elementos"}"
;

elementos ::= expresion:a   
            | elementos:a "," elementos
;

tipo_dato ::= "int"
            |"double"
            |"string"
            |"bool"
;

expresion ::= expresion "+" expresion
            | expresion "*"  expresion
            | expresion "-"  expresion
            | expresion UMENOS expresion
            | expresion "/" expresion
            | expresion " > " expresion
            | expresion " < " expresion
            | expresion " >= " expresion
            | expresion " <= " expresion
            | expresion " == " expresion
            | expresion " != " expresion
            | expresion " and " expresion
            | expresion "or " expresion
            | "!" expresion
            | "(" expresion ")"
            | ENTERO
            | DECIMAL
            | ID
            | STR
            | BOOLEANO
            | referencia_json
;
referencia_json ::= "${NewValor," STR "," STR "}" 
;
archivo_json ::= "{" miembro "}"
;

miembro ::= STR ":" STR 
        |STR ":" DECIMAL
        | miembro "," miembro
;

BLANCOS ::=[ "\r"	|"\t"]+
ENTERO=[0-9]+
DECIMALES=[0-9]+("."[  |0-9]+)?
ID = [A-Za-z_][A-Za-z0-9_]*
BOOL = "true"| "false"
STR  =   \"([^\"]|"\\\"")+\"
```
