What the Hex(crypto,15)

Decodifique usando Hex e veja o que vê... 
6236343a20615735305a584a755a58526659323975646d567963326c76626c3930623239736331397962324e72

[RESOLVING]
Decodifique o hex, obtenha uma base64 , basta decodar a mesma também para ter a flag...

echo 6236343a20615735305a584a755a58526659323975646d567963326c76626c3930623239736331397962324e72 | xxd -r -p
b64: aW50ZXJuZXRfY29udmVyc2lvbl90b29sc19yb2Nr

echo aW50ZXJuZXRfY29udmVyc2lvbl90b29sc19yb2Nr | base64 -d
internet_conversion_tools_rock
