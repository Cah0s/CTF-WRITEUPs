Java is the Best (re, 50)
HINT: JD-GUI is a great Java decompiler.

What kind of input makes this program[https://angstromctf.com/static/problems/re/java_is_the_best/SuperSecure.class] happy?

[RESOLVING]
Aqui teremos um arquivo .class(SuperSecure.class) e devemos primeiro verificar se é realmente isso, vamos dar um file SuperSecure.class
para ver o tipo de arquivo ... sabendo então que realmente é um arquivo java, poderiamos tentar executa-lo usando java SuperSecure.class
porém resultará em erro e não podemos ler o arquivo porque está compactado... vamos descompilar o mesmo para ver o que teremos.

use o Decompilador online[http://www.javadecompilers.com/] ou então podemos usar o JAD[http://varaneckas.com/jad/]... eu usei o JAD mesmo
./jad SuperSecure.class -> ele resultará em u arquivo SuperSecure.jad no qual podemos dar um cat ou strings ou usar um hexeditor, enfim

nós teremos:
if(args[0].charAt(0) == 'd' && args[0].charAt(1) == 'o' && args[0].charAt(2) == 'n' && args[0].charAt(3) == 't' && args[0].charAt(4) == '_' && args[0].charAt(5) == 'u' && args[0].charAt(6) == 's' && args[0].charAt(7) == 'e' && args[0].charAt(8) == '_' && args[0].charAt(9) == 'j' && args[0].charAt(10) == 'a' && args[0].charAt(11) == 'v' && args[0].charAt(12) == 'a' && args[0].charAt(13) == '_' && args[0].charAt(14) == 'i' && args[0].charAt(15) == 'f' && args[0].charAt(16) == '_' && args[0].charAt(17) == 'y' && args[0].charAt(18) == 'o' && args[0].charAt(19) == 'u' && args[0].charAt(20) == '_' && args[0].charAt(21) == 'w' && args[0].charAt(22) == 'a' && args[0].charAt(23) == 'n' && args[0].charAt(24) == 'n' && args[0].charAt(25) == 'a' && args[0].charAt(26) == '_' && args[0].charAt(27) == 'h' && args[0].charAt(28) == 'i' && args[0].charAt(29) == 'd' && args[0].charAt(30) == 'e' && args[0].charAt(31) == '_' && args[0].charAt(32) == 'c' && args[0].charAt(33) == 'o' && args[0].charAt(34) == 'd' && args[0].charAt(35) == 'e')

basta anotar caractere por caractere e achamos a flag o/ -> dont_use_java_if_you_wanna_hide_code