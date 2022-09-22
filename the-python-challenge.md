# The Python Challenge

Write-up til oppgavene i The Python Challenge (http://www.pythonchallenge.com/).



# [0]

Her ser vi et bilde hvor det står 2^38, altså 2 opphøyd i 38.

`
print(2**38)
`

Dette gir oss:  

`274877906944`  

Dermed endrer vi nettadressen til http://www.pythonchallenge.com/pc/def/274877906944.html for å komme til neste oppgave.

# [1]

Ut ifra bildet ser det ut til at vi skal bruke Cæsar-chiffer til å dekryptere teksten.  
Hver bokstav skal forskyves to plasser fremover i alfabetet.  

### Løsning 1
Ikke så veldig elegant, men gjør jobben:

```

char = "abcdefghijklmnopqrstuvwxyzab"

encrypted_message = """g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. 
bmgle gr gl zw fylb gq glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle.
sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj"""

decrypted_message = []

for letter in encrypted_message:

    if letter in char:
        decrypted_message.append(char[char.index(letter)+2])
    else:
        decrypted_message.append(letter)

print(''.join(decrypted_message))

```

Hvilket gir oss:

`i hope you didnt translate it by hand. thats what computers are for. doing it in by hand is inefficient and that's why this text is so long. using string.maketrans() is recommended. now apply on the url`

### Løsning 2

Vi tar med oss tipset, og prøver å finne en løsning som bruker `maketrans()`-funksjonen:

```
# her bruker vi maketrans()-funksjonen som foreslått i løsningen:

encrypted_message = """g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. 
bmgle gr gl zw fylb gq glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle.
sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj"""

intab = "abcdefghijklmnopqrstuvwxyz"

outtab = "cdefghijklmnopqrstuvwxyzab"

trantab = encrypted_message.maketrans(intab, outtab) # lager en oversettelsestabell

print(encrypted_message.translate(trantab))

```

Når vi kjører sciptet på URLen får vi:

`jvvr://yyy.ravjqpejcnngpig.eqo/re/fgh/ocr.jvon`

Etter litt prøving og feiling viser det seg at løsningsordet er `ocr`, og dermed blir neste URL:  
http://www.pythonchallenge.com/pc/def/ocr.html

# [2]

Her hintes det sterkt til at vi må kikke i kildekoden.  
Vi inspiserer og finner en stor vegg med tekst.  

Et lite utdrag:
```
%%$@_$^__#)^)&!_+]!*@&^}@[@%]()%+$&[(_@%+%$*^@$^!+]!&_#)_*}{}}!}_]$[%}@[{_@#_^{*
@##&{#&{&)*%(]{{([*}@[@&]+!!*{)!}{%+{))])[!^})+)$]#{*+^((@^@}$[**$&^{$!@#$%)!@(&
+^!{%_$&@^!}$_${)$_#)!({@!)(^}!*^&!$%_&&}&_#&@{)]{+)%*{&*%*&@%$+]!*__(#!*){%&@++
!_)^$&&%#+)}!@!)&^}**#!_$([$!$}#*^}$+&#[{*{}{((#$]{[$[$$()_#}!@}^@_&%^*!){*^^_$^
]@}#%[%!^[^_})+@&}{@*!(@$%$^)}[_!}(*}#}#___}!](@_{{(*#%!%%+*)^+#%}$+_]#}%!**#!^_
)@)$%%^{_%!@(&{!}$_$[)*!^&{}*#{!)@})!*{^&[&$#@)*@#@_@^_#*!@_#})+[^&!@*}^){%%{&#@
```

Copypaster teksten til en fil som får navnet `2.txt`.  

Videre i kildekoden står det "find rare characters in the mess below".  

Vi åpner fila vår i Python:  

```
f = open("2.txt", "r")

txt = f.read()
```

Hvor stor er egentlig teksten?

`len(txt)` gir oss `98773`

Altså ingen vits i å lete manuelt...

Første idé er å fjerne alt som ikke er alfanumerisk, altså bokstaver eller tall.  
Har en anelse om at regex kanskje er rett verktøy for jobben.  

Googler "remove non alpha numeric characthers python" og får opp flere forslag.  
Ender opp med et forslag herifra:  
https://stackoverflow.com/questions/1276764/stripping-everything-but-alphanumeric-chars-from-a-string-in-python

Dermed blir koden slik:
```
import re

f = open("2.txt", "r")

txt = f.read()

new_txt = re.sub(r"\W+", "", txt) # sub for substitute, "\W+" tilsvarer "[^0-9a-zA-Z]+"

new_txt = new_txt.replace("_", "") # fjerner understreker _ (regnes som alfanumerisk)

print(new_txt)
```

Dette gir oss løsningsordet:  
`equality`

Neste level:  
www.pythonchallenge.com/pc/def/equality.html

# [3]

Hint: "One small letter, surrounded by EXACTLY three big bodyguards on each of its sides."  

Nok en gang kikker vi i kildekoden og finner en stor vegg med tekst.  

Utdrag:
```
ENihrpCLhujoBqPRDPvfzcwadMMMbkmkzCCzoTPfbRlzBqMblmxTxNniNoCufprWXxgHZpldkoLCrHJq
vYuyJFCZtqXLhWiYzOXeglkzhVJIWmeUySGuFVmLTCyMshQtvZpPwuIbOHNoBauwvuJYCmqznOBgByPw
TDQheAbsaMLjTmAOKmNsLziVMenFxQdATQIjItwtyCHyeMwQTNxbbLXWZnGmDqHhXnLHfEyvzxMhSXzd
BEBaxeaPgQPttvqRvxHPEOUtIsttPDeeuGFgmDkKQcEYjuSuiGROGfYpzkQgvcCDBKrcYwHFlvPzDMEk
MyuPxvGtgSvWgrybKOnbEGhqHUXHhnyjFwSfTfaiWtAOMBZEScsOSumwPssjCPlLbLsPIGffDLpZzMKz
```

Det ser ut til å være bare bokstaver denne gangen.  
Vi tolker derfor hintet til å være at vi skal finne en liten bokstav, omgitt av nøyaktig tre bokstaver på hver side.  
Altså et slikt mønster: aBBBaBBBa  

Etter å ha googlet regex for n'te gang, endte jeg opp med et mønster som så slik ut:  

`pattern = "[a-z][A-Z]{3}[a-z][A-Z]{3}[a-z]"`

Hele koden endte opp slik:  

```
import re

f = open("3.txt", "r")

txt = f.read()


pattern = "[a-z][A-Z]{3}[a-z][A-Z]{3}[a-z]"

matches = re.findall(pattern, txt)

print(matches)

word = ""

for match in matches:
    #print(match[4])
    word = word + match[4]

print(word)
```

Kodetordet for neste oppgave ble dermed `linkedlist`.

Neste level:  
http://www.pythonchallenge.com/pc/def/linkedlist.html

# [4]

Vi blir møtt av en enkel `<p>` hvor det står `linkedlist.php`.  

