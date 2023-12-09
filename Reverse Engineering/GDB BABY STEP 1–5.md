# GDB BABY STEP 1--5
**BABY STEP 1**
> Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. [CHall](https://artifacts.picoctf.net/c/512/debugger0_a)

* Mở chall bằng `GDB Peda` và `disas main` ta được 
```
0x0000555555555129 <+0>:	endbr64 
   0x000055555555512d <+4>:	push   rbp
   0x000055555555512e <+5>:	mov    rbp,rsp
   0x0000555555555131 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x0000555555555134 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x0000555555555138 <+15>:	mov    eax,0x86342
   0x000055555555513d <+20>:	pop    rbp
=> 0x000055555555513e <+21>:	ret 
```

* Kết quả cuối cùng của thanh eax là `0x86342` convert sang dec ta có flag `PicoCTF{549698}`



---
**BABY STEP 2**
> Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. [chall](https://artifacts.picoctf.net/c/520/debugger0_b)

* Tương tự như chall ở trên, quăng vô `GDB Peda` để debug và `disas main` để xem command hàm main 
> 0x0000000000401106 <+0>:	endbr64 
   0x000000000040110a <+4>:	push   rbp
   0x000000000040110b <+5>:	mov    rbp,rsp
   0x000000000040110e <+8>:	mov    DWORD PTR [rbp-0x14],edi
   0x0000000000401111 <+11>:	mov    QWORD PTR [rbp-0x20],rsi
   0x0000000000401115 <+15>:	mov    DWORD PTR [rbp-0x4],0x1e0da
   0x000000000040111c <+22>:	mov    DWORD PTR [rbp-0xc],0x25f
   0x0000000000401123 <+29>:	mov    DWORD PTR [rbp-0x8],0x0
   0x000000000040112a <+36>:	jmp    0x401136 <main+48>
   0x000000000040112c <+38>:	mov    eax,DWORD PTR [rbp-0x8]
   0x000000000040112f <+41>:	add    DWORD PTR [rbp-0x4],eax
   0x0000000000401132 <+44>:	add    DWORD PTR [rbp-0x8],0x1
   0x0000000000401136 <+48>:	mov    eax,DWORD PTR [rbp-0x8]
   0x0000000000401139 <+51>:	cmp    eax,DWORD PTR [rbp-0xc]
   0x000000000040113c <+54>:	jl     0x40112c <main+38>
   0x000000000040113e <+56>:	mov    eax,DWORD PTR [rbp-0x4]
   0x0000000000401141 <+59>:	pop    rbp
   0x0000000000401142 <+60>:	ret 

* Quan sát thấy thanh `eax` được thực hiện phép gán và tính tổng qua các phép toán, ở cuối hàm thì return lại giá trị của `eax` vì thế để lấy được giá trị của `eax`, mình sẽ đặt `breakpoint` ở dòng `0x0000000000401142 <+60>: ret` và `run` chương trình.
* Tiếp theo dùng lệnh `print/d $eax` để in ra giá trị sau khi đã return của `eax` và lấy flag `picoCTF{307019}`

---

**BABY STEP 3**

> Now for something a little different. 0x2262c96b is loaded into memory in the main function. Examine byte-wise the memory that the constant is loaded in by using the GDB command x/4xb addr. The flag is the four bytes as they are stored in memory. If you find the bytes 0x11 0x22 0x33 0x44 in the memory location, your flag would be: picoCTF{0x11223344}. [chall](https://artifacts.picoctf.net/c/531/debugger0_c)
 
* 
