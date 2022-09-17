# [0]

Her ser vi et bilde hvor det står 2^38, altså 2 opphøyd i 38.

`
print(2**38)
`

Dette gir oss:  

`274877906944`  

Dermed endrer vi nettadressen til http://www.pythonchallenge.com/pc/def/274877906944.html for å komme til neste oppgave.

# 1

Ut ifra bildet ser det ut til at vi skal bruke Cæsar-chiffer til å dekryptere teksten.  
Hver bokstav skal forskyves to plasser fremover i alfabetet.  

Første løsning, ikke så veldig elegant, men gjør jobben:

```

char = "abcdefghijklmnopqrstuvwxyzab"

encrypted_message = "g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp. bmgle gr gl zw fylb gq glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle. sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj"

decrypted_message = []

for letter in encrypted_message:

    if letter in char:
        
        print(char.index(letter)) # gir oss index til hver bokstav

        decrypted_message.append(char[char.index(letter)+2])
    else:
        decrypted_message.append(letter)

print(''.join(decrypted_message))

```

Hvilket gir oss:

`i hope you didnt translate it by hand. thats what computers are for. doing it in by hand is inefficient and that's why this text is so long. using string.maketrans() is recommended. now apply on the url`

