  
   Realizzare la funzione contalettere(s) seguente. La funzione
   accetta come parametro una stringa s (che puo' anche essere
   vuota). La funzione deve restituire il numero di lettere minuscole
   che sono presenti in s almeno una volta. Si garantisce che in s non
   saranno mai presenti lettere maiuscole e numeri; potranno pero'
   essere presenti spazi e altri caratteri di punteggiatura, che
   devono essere ignorati.

   Ad esempio, se s = "abcdefabcdef" la funzione deve restituire 6, in
   quanto nella stringa compaiono in tutto 6 lettere dell'alfabeto (in
   particolare, 'a', 'b', 'c', 'd', 'e', 'f').

   Si noti che, in base alla specifica sopra, la funzione restituisce
   sempre un valore compreso tra 0 e 26 (estremi inclusi): la funzione
   restituisce 0 se e solo se in s non e' presente alcuna lettera
   minuscola dell'alfabeto, mentre restituisce 26 se e solo se in s
   compare ognuna delle 26 lettere dell'alfabeto almeno una volta.


     /* contalettere.c */
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    
    int contalettere( char *s )
    {
        return -1;
    }
    
    void test( char *s, int expect )
    {
        int r = contalettere(s);
        if ( r == expect ) {
            printf("Test OK\n");
        } else {
            printf("test FALLITO: s=\"%s\", risultato atteso=%d, risultato ottenuto=%d\n",
                   s, expect, r);
        }
    }
    
    int main( void )
    {
        test("a", 1);
        test("xyz", 3);
        test("abcdefabcdef", 6);
        test("una mela al giorno leva il medico di torno", 14);
        test("supercalifragilistichespiralidoso", 15);
        test("pranzo d'acqua fa volti sghembi", 21);
        test("the quick brown fox jumps over the lazy dog", 26);
        test("abcdefghijklmnopqrstuvwxyz", 26);
        test("abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz", 26);
        test("", 0); /* stringa vuota */
        test("...", 0); /* non ci sono lettere, solo punteggiatura */
        test("   ", 0); /* non ci sono lettere, solo punteggiatura */
        return 0;
    }


**Passo 1**

Scorro la stringa 

    **int**  contalettere( **char** *s){ 
       int i
       for (i=0; s[i]; i++) {
       }
    } 
In questo caso `s[i]` rappresenta il singolo carattere
ex: "cane"
s[0]=c
s[1]=a
s[2]=n
s[3] =e

**Passo 2**

Creo una seconda lista dove salvo le lettere minuscole che ho trovate in maniera tele che se trovo un doppione lo salto

    **int**  contalettere( **char** *s){ 
       int occ[26] = {0}; 
       int i
       for (i=0; s[i]; i++) {
       }
    }


int occ[26] = {0}; è uguale a [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]

Quindi ora l'idea è di mettere un "1" al posto di "0" nelle lettere che compaiono.


*Attenzione!!* 
*Questo metodo si può usare sono con un numero di iterazioni di cui si conosce il numero(in questo caso 26). Altrimenti si rischia di saturare la memoria* 

**Passo 3**

    **int**  contalettere( **char** *s){ 
       int occ[26] = {0}; 
       int i
       for (i=0; s[i]; i++) {
	       occ[s[i] - 'a'] += 1;
       }
    }
Selezione le lettere di mio interesse e gli sostituisco un uno...
esempio:
anna->[1,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0 ecc...]

**Passo 4**

    **int**  contalettere( **char** *s){ 
       int occ[26] = {0}; 
       int i
       for (i=0; s[i]; i++) {
	       occ[s[i] - 'a'] += 1;
       }
	    for (j=0; j<26; j++) {
	        if (occ[j] > 0) result++;
	    }
	    return result;
    }

Ho sommato tutti gli uno all'interno della lista e il risultato è il numero delle lettere minuscole!


