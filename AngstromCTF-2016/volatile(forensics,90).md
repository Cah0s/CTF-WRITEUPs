volatile (forensics, 90)
HINT: Ter um olhar para a volatility programa de python.

Socorro! Uma das nossas máquinas foi comprometida! Temos um despejo de memória[https://mega.co.nz/#!Bg5B3DTD!dgaV9sklrXPop2w-BdE63t2FUIrUb_8fEL-HQqtMhaM]. Encontre o processo suspeito. A máquina estava executando o Windows XP Service Pack 2.

[RESOLVING]
Primeiro você poderia analizar com {file} e {strings} porém não acharia nada de útil, então como sabemos ser um dump de imagem, volatility é a melhor opção, então vamos verificar o profile da imagem::

volatility imageinfo -f  memdump.mem

Volatility Foundation Volatility Framework 2.5
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : WinXPSP2x86, WinXPSP3x86 (Instantiated with WinXPSP2x86)
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/cah0s/Área de trabalho/CTF/angstromctf/Volatile/memdump.mem)
                      PAE type : PAE
                           DTB : 0x33f000L
                          KDBG : 0x80544ce0L
          Number of Processors : 1
     Image Type (Service Pack) : 2
                KPCR for CPU 0 : 0xffdff000L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2015-04-23 04:10:22 UTC+0000
     Image local date and time : 2015-04-23 00:10:22 -0400

Sabendo o profile WinXPSP2x86 vamos poder analizar a imagem com mais calma
Aqui você poderia tentar várias opções como clipboard, cmdline ... mas sendo direto era só usar pslist..::

volatility -f memdump.mem --profile=WinXPSP2x86 pslist

Volatility Foundation Volatility Framework 2.5
Offset(V)  Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
---------- -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x823c8830 System                    4      0     58      335 ------      0                                                              
0x81e90020 smss.exe                560      4      3       21 ------      0 2015-04-23 04:05:05 UTC+0000                                 
0x821b3da0 csrss.exe               616    560     12      397      0      0 2015-04-23 04:05:11 UTC+0000                                 
0x81ff9da0 winlogon.exe            640    560     23      522      0      0 2015-04-23 04:05:12 UTC+0000                                 
0x821ec6a0 services.exe            696    640     17      348      0      0 2015-04-23 04:05:15 UTC+0000                                 
0x821eb020 lsass.exe               708    640     23      358      0      0 2015-04-23 04:05:15 UTC+0000                                 
0x81f1cb78 vmacthlp.exe            868    696      1       24      0      0 2015-04-23 04:05:22 UTC+0000                                 
0x81fecb58 svchost.exe             904    696     18      198      0      0 2015-04-23 04:05:23 UTC+0000                                 
0x81fe8850 svchost.exe             972    696     10      256      0      0 2015-04-23 04:05:24 UTC+0000                                 
0x81dba570 svchost.exe            1064    696     71     1303      0      0 2015-04-23 04:05:24 UTC+0000                                 
0x81f10a70 svchost.exe            1148    696      6       76      0      0 2015-04-23 04:05:24 UTC+0000                                 
0x81fdf020 svchost.exe            1188    696     13      198      0      0 2015-04-23 04:05:24 UTC+0000                                 
0x81fdada0 spoolsv.exe            1400    696     15      116      0      0 2015-04-23 04:05:26 UTC+0000                                 
0x81effda0 vmtoolsd.exe           1724    696      7      253      0      0 2015-04-23 04:05:43 UTC+0000                                 
0x81d76da0 alg.exe                 376    696      6      100      0      0 2015-04-23 04:06:00 UTC+0000                                 
0x8217b8b8 wuauclt.exe            1872   1064      9      184      0      0 2015-04-23 04:06:38 UTC+0000                                 
0x81fc0770 wmiprvse.exe            476    904      6      138      0      0 2015-04-23 04:07:04 UTC+0000                                 
0x81db3da0 explorer.exe            500   1860     14      377      0      0 2015-04-23 04:07:33 UTC+0000                                 
0x81d78020 wscntfy.exe             244   1064      1       27      0      0 2015-04-23 04:07:35 UTC+0000                                 
0x821989b0 msiexec.exe             764    696      6      109      0      0 2015-04-23 04:07:40 UTC+0000                                 
0x8219b970 vmtoolsd.exe            588    500      3      116      0      0 2015-04-23 04:07:44 UTC+0000                                 
0x82027ad0 msmsgs.exe             1168    500      3      165      0      0 2015-04-23 04:07:44 UTC+0000                                 
0x81f88020 wtf_who_names_k        1768    500      1       15      0      0 2015-04-23 04:09:31 UTC+0000 << reparem em algo incomum ... 
0x8214b780 wpabaln.exe             292    640      1       57      0      0 2015-04-23 04:09:33 UTC+0000                                 
0x81fee020 FTK Imager.exe          408    500     10      241      0      0 2015-04-23 04:10:01 UTC+0000

Ja ficou interessante explorar e saber do que se trata ali do processo né ...::

volatility -f memdump.mem --profile=WinXPSP2x86 consoles

Volatility Foundation Volatility Framework 2.5
**************************************************
ConsoleProcess: csrss.exe Pid: 616
Console: 0x4e2350 CommandHistorySize: 50
HistoryBufferCount: 1 HistoryBufferMax: 4
OriginalTitle: C:\Documents and Settings\Administrator\Desktop\wtf_who_names_keyloggers_like_this.exe
Title: C:\Documents and Settings\Administrator\Desktop\wtf_who_names_keyloggers_like_this.exe
AttachedProcess: wtf_who_names_k Pid: 1768 Handle: 0x68c
----
CommandHistory: 0x10f86f8 Application: wtf_who_names_keyloggers_like_this.exe Flags: Allocated
CommandCount: 0 LastAdded: -1 LastDisplayed: -1
FirstCommand: 0 CommandCountMax: 50
ProcessHandle: 0x68c
----
Screen 0x4e2a58 X:80 Y:300
Dump:

bom, claro que explorar esse exe não tem como e nem é preciso pois ai está a flag >> wtf_who_names_keyloggers_like_this.exe[sem o .exe!!]