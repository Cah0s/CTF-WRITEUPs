Wher iz mai cheezburgr (forensics, 80)
HINT: Olhe para os cabeçalhos, eles podem te dizer algo.

Halp! Eu perdi meu cheezburger e eu não posso encontrá-lo! É neste arquivo[https://angstromctf.com/static/problems/forensics/meow_meow_chzbrgr/meow] em algum lugar, você pode ser encontrá-la? K Thx m8 muito apreciado.

[RESOLVING]
Sem muito blablabla, sabemos que se trata de uma imagem, e pelo tamanho aparenta de fato ser uma imagem o que pode-se confirmar com o comando {file} ... prossigamos, vamos montar essa bagaçeira e ver o que temos::

mount -t hfsplus -o loop meow.dmg /mnt/tmp && cd /mnt/tmp && ls -la

total 532
drwxrwxr-x 1 root root     10 Dez  6  2015 .
drwxr-xr-x 3 root root   4096 Jun  6 21:29 ..
drwxrwxrwx 1  501 utmp     56 Jan  1 14:10 chezbrgeur
-rw-r--r-- 1  501 utmp   8196 Jan  1 14:10 .DS_Store
drwx------ 1  501 utmp     11 Jan  1 14:10 .fseventsd
dr-xr-xr-t 1 root root      2 Dez  6  2015 '.HFS+ Private Directory Data'$'\r'
---------- 1 root root 524288 Dez  6  2015 .journal
---------- 1 root root   4096 Dez  6  2015 .journal_info_block
d-wx-wx-wt 1  501 utmp      3 Dez  7 11:09 .Trashes

Sem mais demoras interessante de primeira sempre olhar o lixo hehe::

cd .Trashes && ls -la

total 0
d-wx-wx-wt 1  501 utmp  3 Dez  7 11:09 .
drwxrwxr-x 1 root root 10 Dez  6  2015 ..
drwx------ 1  501 utmp  6 Jan  1 14:05 501

cd 501 && ls -la

total 20
drwx------ 1 501 utmp    6 Jan  1 14:05 .
d-wx-wx-wt 1 501 utmp    3 Dez  7 11:09 ..
-rw-r--r-- 1 501 utmp 6148 Jan  1 14:05 .DS_Store
-rwxrwxrwx 1 501 utmp 2555 Dez  6  2015 mysteries.fs
-rwxrwxrwx 1 501 utmp  885 Dez  7 11:09 'secret 12.05.37.fs'
-rwxrwxrwx 1 501 utmp  885 Dez  6  2015 secret.fs

hora de analizar::

file mysteries.fs 
mysteries.fs: gzip compressed data, last modified: Mon Dec  7 01:49:42 2015, from Unix

file secret\ 12.05.37.fs 
secret 12.05.37.fs: Zip archive data, at least v1.0 to extract

file secret.fs 
secret.fs: Zip archive data, at least v1.0 to extract

mv mysteries.{fs,gz}
gunzip mysteries.gz 
file mysteries
mysteries: POSIX tar archive

tar xvf mysteries
./._log.txt
log.txt
my_passwords.md

cat log.txt 
zip -er secret.zip SECRETDONOTTOUCH/
me0wn3k0i<3c4tt3sv3rymch
me0wn3k0i<3c4tt3sv3rymch
exit

Identificamos os arquivos, extraimos de acordo com o tipo e então temos uma senha e ainda um arquivo secret.fs(outro porém inpreciso).. basta aplicar a senha e pegar sua flag :)

unzip -P 'me0wn3k0i<3c4tt3sv3rymch' secret.fs 
Archive:  secret.fs
   creating: SECRETSDONOTTOUCH/
  inflating: SECRETSDONOTTOUCH/._flag.txt  
 extracting: SECRETSDONOTTOUCH/flag.txt  

cat SECRETSDONOTTOUCH/flag.txt 
angstromCTF{120x29y_dmg_no_haz_mai_chezburger}