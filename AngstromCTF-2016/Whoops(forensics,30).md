Whoops(forensics,30)
HINT: O que acontece quando você apaga um arquivo?

Whoops! I accidentally deleted the book I was reading from my flash drive!! I made an image[https://angstromctf.com/static/problems/forensics/oops/oops.img] of the drive afterwards though! Can you find the book, and the flag in it?

[RESOLVING]
use hexedit -> tab -> ctrl+s -> search flag .... flag{waw_.Trashes_isnt_useless_after_all} easy
or strings oops.img | grep flag{