<h1>Solution: It Has Begun</h1>

<h3>With this challenge it gives you a malisiouse shell script and you have to look through it and find the flag.</h3>

Initially looking at it you see a part of the flag reversed so I just reverse it with this command.

<img src="https://i.imgur.com/eIeC1N1.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>

```
echo 'user@tS_u0y_ll1w{BTH'| rev
```
I then get this.

<img src="https://i.imgur.com/Qkcd9oN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

I then noticed that there was something base64 encoded.

<img src="https://i.imgur.com/EdFCRMO.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>

I then put it in cyber cheff and get this.

<img src="https://i.imgur.com/WKIMnKd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The flag comes out to this.

```
HTB{w1ll_y0u_St@resu4nd_y0uR_Gr0uNd!!}
```

Which doesnt make any sense so i just looked and noticed that Im pretty sure the @resu shouldnt be there and got the flag!

<h3>The flag comes out to be HTB{w1ll_y0u_St4nd_y0uR_Gr0uNd!!}</h3>
