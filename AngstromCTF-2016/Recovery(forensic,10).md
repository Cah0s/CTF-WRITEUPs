Recovery(forensics,10)
HINT: Um editor de texto simples é tudo o que você precisa.

Recebemos esta imagem[https://angstromctf.com/static/problems/forensics/recovery/recovered.img] de disco do No Such Agency há poucos dias. Um hacker escondeu a senha para o computador dele nesta imagem.
você pode encontrá-lo para nós?

[RESOLVING]
Basta abrir a imagem com um editor HEX (hexedit, ghex, online).
procure por "flag" ou no terminal dar o comando: "strings recovered.img | grep flag{".

FLAG: flag{waw_ctrl_f_was_sooper_afective}