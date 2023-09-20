```BNF

inicio ::= "void" "main" "()" "{" lista_instr "}"
            
            |error
            
;

lista_instr ::= lista_instr instruccion
              |instruccion
; 

instruccion ::= impresion ";"
    | declaracion:val ";"                                              
    | list_ifs
    | list_for
    | list_switch
    | list_while
    | error 
    | definirGlobales
    | graficaBarras
    
;

definirGlobales ::= "void" "DefinicionGlobales" "()" "{"listaAsignaciones"}"
    
;

listaAsignaciones ::= listaAsignaciones asignacion
		   | asignacion
;

asignacion ::= "string" "id" "=" valor ";"                                      
            |"double"
;

valor ::= "string":a                             
       | "double":a                              
       | buscar:a                              
;

buscar ::= "$" "{" "," "string":a "," "string":b "}" ";"              ;
;

graficaBarras ::= "string" opciones
                | "string" "[]"  listadoValores ";"
;

opciones ::= "titulo" "=" valor:a                       
          | "titulox" "=" valor:a    
          | "tituloy" "=" valor:a                       
;

listadoValores ::= listadoValores valores
          | valores
;

valores ::= "string"
         | asignacion
;


list_ifs ::= tipo_if lista_instr "}"
;

tipo_if ::= "if":a "(" expresion:val ")" "{"                                     
    | "else":a "if":b "(" expresion:val ")" "{"                                  
    | "else":a "(" expresion:val ")" "{"                                          
;

list_for ::= tipo_for lista_instr "}"
;

tipo_for ::= FOR:a "(" tipo_D "texto":val "=" "numeros":b ";" "texto" relacionales "numeros":c ";" "texto" "++" ")" "{"      
;

list_while ::= tipo_while lista_instr "}"    
    | tipo_do lista_instr:val "}" do_while                                  
;

do_while ::= "while" "(" expresion:a ")" ";"                              
;

tipo_do ::= "do" "{"                                       
;

tipo_while ::="while" "("  expresion:val ")" "{"                             
;

list_switch ::= ini_switch tipo_switch "}" 
;

ini_switch ::= "switch":a "(" expresion:val ")" "{"    
;

tipo_switch ::= tipo_switch ins_case
    | ins_case
;


ins_case ::= impcase lista_instr
    | impcase
    | impdefault lista_instr
;

impcase ::= "case" "numeros":a ":" "texto":val "=" "numeros":val2 ";"    
            | BREAK ";"           

;

impdefault ::= "default" ":" impresion 
;


relacionales ::= ">"
    | "<"
    | ">="
    | "<="
;

impresion ::= "console" "." "write" "(" expresion:a  ")"                         
    | "console" "." "write" "(" """expresion:a """ ")"         
    |error
;

declaracion ::= tipo_D "texto":id "=" expresion:a                            
;

tipo_D ::= "entero"
    | "string"
    | "double"
    | "char"
    | "bool"
    | error
;


expresion ::= expresion:a "+" expresion:b     
    | expresion:a "*"  expresion:b            
    | expresion:a "-"  expresion:b            
    | expresion:a "/"  expresion:b             
    | expresion:a "||"  expresion:b                
    | expresion:a "&&" expresion:b               
    | expresion:a "!" expresion:b              
    | expresion:a "<" expresion:b           
    | expresion:a ">" expresion:b           
    | expresion:a ">=" expresion:b            
    | expresion:a "<=" expresion:b            
    | expresion:a "==" expresion:b        
    | expresion:a "!=" expresion:b          
    
    | "entero":a                                  
    | "string"
    | "double"
    | "char"
    | "bool"                                  
    | "str":a "+" expresion:b                     
    | "true":a                                    
    | "false":a                                   
    | "str":a                                     
    | "strc":a                                    
    | "numeros":a                                
    | "texto":a                                  
    | error
;


```
