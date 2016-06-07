SuperSecure™(web,30)
HINT: Gostaria de saber onde o seu browser vai atrás de você clique em Login ...

Jason fez um novo site SuperSeguro™[http://web.angstromctf.com:1338/], mas perdeu a senha. É exibido na página de administração. você pode fazer o login?
Bom no código fonte da página tem a seguinte linha (12)

if(username == "admin" && CryptoJS.SHA256(password).toString() == "7de7b2fed84fd29656dff73bc98daef391b0480efdb0f2e3034e7598b5a412ce") {
[and the in the line]e na linha (15) window.location.href = "admin_" + CryptoJS.SHA256(password).toString() + ".html";

(12) se o username for (admin) e a senha for igual a sha256 você seria redirecionado (12) para a (admin_7de7b2fed84fd29656dff73bc98daef391b0480efdb0f2e3034e7598b5a412ce.html)

[RESOLVING]
Era só acessar ela direto sem logar e lá estava a flag:

Thank you for using &Aring;web!
The flag required for administration is all_javascript_is_open