
## Challenge Overview  
  
The challenge provides the following hint:  
  
> Every trail has a beginning. This one starts here:    
> https://gist.github.com/garvk07/3f9c505068c011e0fd6abd9ddf56aecb    
> Follow the breadcrumbs. The flag is at the end.  
  
Opening the GitHub Gist reveals encoded data.  
  
![Initial Gist](../../Screenshots/breadcrumbs-start.png)  
  
---  
  
## Step 1 – Base64 Decode  
  
The content from the first Gist appears to be **Base64 encoded**.    
Using CyberChef with the **Base64 Decode** operation reveals the next link in the chain:  

[https://gist.github.com/garvk07/ba406460f2e932b5496ca25977be25be](https://gist.github.com/garvk07/ba406460f2e932b5496ca25977be25be)

  
Opening that link shows another encoded message.  
  
![Second Gist](../../Screenshots/breadcrumbs-second.png)  
  
---  
  
## Step 2 – Hex Decode  
  
The new content appears to be **hexadecimal encoded**.  
  
Using CyberChef again and applying **From Hex** reveals another link:  

[https://gist.github.com/garvk07/5d5ef859f530c3d593a4a3c7580d2f29](https://gist.github.com/garvk07/5d5ef859f530c3d593a4a3c7580d2f29)

  
Opening this link shows another encoded string.  
  
![Third Gist](../../Screenshots/breadcrumbs-third.png)  
  
---  
  
## Step 3 – ROT13 Decode  
  
The final encoded string appears to be **ROT13 encoded**.  
  
Using a ROT13 decoder (for example https://rot13.com) reveals the flag.  
  
---  
  
## Flag  

utflag{f0ll0w1ng_th3_cr4wl_tr41l}