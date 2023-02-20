my solution for the trun vulnserver. tested on windows10 without any exploit guards. 
i might publish my other solutions aswell, but i would need to clean them up a bit.

**How does this work?**

![enter image description here](https://i.imgur.com/tivxflY.png)

Function 3 copies the contents from the heap onto a buffer on the stack without doing any boundary checks. causing a overflow. 

![enter image description here](https://i.imgur.com/DyKUWBC.png)

We can now override the instruction pointer (eip).

Now we just need a gadget to jmp esp, luckily since this is an easy target, there are multiple in essfunc.dll. 

![enter image description here](https://i.imgur.com/yMJ8gtC.png)

Now we have gained code execution.

![enter image description here](https://i.imgur.com/7acExSH.png)

**What does the shellcode do?**

 1. Get ProcAddress of LoadLibaryA
 2. Loads user32.dll (because of MessageBoxA)
 3. Get ProcAddress of MessageBoxA
 4. Setup MessageBoxA call MessageBoxA(NULL, "Hello World!", NULL, MB_OK);
 5. call eax

