
## Challenge Overview  
  
The challenge description states:  
  
> We've heard tell of a hidden message that's been placed somewhere nearby. Can you find it?  
  
No files were provided for download, suggesting the flag might be hidden somewhere within the challenge webpage itself.  

## Initial Investigation  
  
Inspecting the page source did not reveal anything unusual.  

![Nothing Unusual](../../Screenshots/page-source.png)  

Next, I opened **Browser Developer Tools** and checked the **Network tab** while interacting with the page. After pressing the **Submit** button, several requests appeared.  
  
One request returned a JSON object containing the names of all challenges along with additional data.  

## Discovering the Hidden Text  
  
Looking at the entry corresponding to **Hidden in Plain Sight**, I noticed some unusual characters:  
  
![Invisible Unicode Text](../../Screenshots/hidden-unicode.png)  
  
The characters appeared invisible, suggesting they might be **Unicode characters from the private use range**.  

## Extracting the Unicode Values  
  
To inspect the characters more closely:  
  
1. Copy the invisible text.  
2. Paste it into a Unicode inspection tool.  
  
Using:  
  
- https://r12a.github.io/app-conversion/  
  
I converted the characters into their **Unicode code points**, which looked something like:  

U+E0066 U+E0074 U+E0066 ...

  
---  
  
## Decoding the Data  
  
The characters shared the prefix `E00`, suggesting the actual encoded data might be the remaining hex values.  
  
To decode this:  
  
1. Copy the Unicode values.  
2. Remove the `E00` prefix.  
3. Paste the resulting hex string into **CyberChef**.  
4. Apply **From Hex**.  
  
This reveals the flag.  
  
![CyberChef Decode](../../Screenshots/hidden-unicode-decode.png)  
  
---  
  
## Flag  

utflag{1nv1s1bl3_un1c0d3}