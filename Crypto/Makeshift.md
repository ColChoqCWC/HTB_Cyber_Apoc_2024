<h1>Solution: Makeshift</h1>

<h3>In this challange it came with a folder that contained a source pyhton file and a output.txt that contained the encrypted flag !?}De!e3d_5n_nipaOw_3eTR3bt4{_THB</h3>

The encryption code was this:

```python3
flag = "HTB"
new_flag = ''

for i in range(0, len(flag), 3):
    new_flag += flag[i+1]
    new_flag += flag[i+2]
    new_flag += flag[i]

print(new_flag)
```

What I did was take the endcoded flag and make it a variable. I then made a empty string and then iterated through the encoded sting by a index of 3 and moving each character to the front of the string. Once done iterating it then reverses the flag and prints it out

```python3
J_flag = "!?}De!e3d_5n_nipaOw_3eTR3bt4{_THB"

unj_flag = ''

for i in range(0, len(J_flag), 3):
    unj_flag += J_flag[i+2] + J_flag[i:i+2]

decode_flag = unj_flag[::-1]

print(decode_flag)
```

<h3>This gives you the flag HTB{4_b3tTeR_w3apOn_i5_n3edeD!?!}</h3>
