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
