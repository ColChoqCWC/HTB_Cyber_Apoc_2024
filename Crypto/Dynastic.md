<h1>Solution: Dynastic</h1>
<h3>Here there was a source pyhton file and a output.txt file the contained the encrypted flag DJF_CTA_SWYH_NPDKK_MBZ_QPHTIGPMZY_KRZSQE?!_ZL_CN_PGLIMCU_YU_KJODME_RYGZXL</h3>

The encryption code for the source file was this:

```python3
from secret import FLAG
from random import randint

def to_identity_map(a):
    return ord(a) - 0x41

def from_identity_map(a):
    return chr(a % 26 + 0x41)

def encrypt(m):
    c = ''
    for i in range(len(m)):
        ch = m[i]
        if not ch.isalpha():
            ech = ch
        else:
            chi = to_identity_map(ch)
            ech = from_identity_map(chi + i)
        c += ech
    return c

with open('output.txt', 'w') as f:
    f.write('Make sure you wrap the decrypted text with the HTB flag format :-]\n')
    f.write(encrypt(FLAG))
```

All I had ot do waas change the from_identity_map(chi + i) to from_identity_map(chi - i). While also getting rid of the imports and the open function at then end and replacing it with a function call and a print statment.

```python3
J_string = "DJF_CTA_SWYH_NPDKK_MBZ_QPHTIGPMZY_KRZSQE?!_ZL_CN_PGLIMCU_YU_KJODME_RYGZXL"

def to_identity_map(a):
    return ord(a) - 0x41

def from_identity_map(a):
    return chr(a % 26 + 0x41)

def decrypt(c):
    m = ''
    for i in range(len(c)):
        ch = c[i]
        if not ch.isalpha():
            mch = ch
        else:
            chi = to_identity_map(ch)
            mch = from_identity_map(chi - i)
        m += mch
    return m

decrypt_text = decrypt(J_string)
print(decrypt_text)
```
<h3>The falg came out to be HTB{DID_YOU_KNOW_ABOUT_THE_TRITHEMIUS_CIPHER?!_IT_IS_SIMILAR_TO_CAESAR_CIPHER}</h3>

