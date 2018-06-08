# String Analysis Functions  

## Catalogue

* [Suammary](#归类)
* [Find](#查找)
* [Split](#分割)
* [concatenate](#连接)
* [Scan](#扫描输入)
* [Compare](#比较)
* [Copy](#复制)
* [Reversal](#反转)
* [C++ string](#string)

### 查找

**[strchr](http://www.cplusplus.com/reference/cstring/strchr/?kw=strchr)**
>功 能：查找串中给定字符的第一个匹配处地址  
>用 法： char *strchr(char *str, char c);  
>注意：return NULL则没找到  
  
```c
 int main(void) {  
    //查找字符串的匹配处  
    char *x = "check who we are";  
    char c = 'w';  
    char *ptr = strchr(x, c);  
    if (ptr) {  
        printf("find it");  
    } else {  
        printf("not find it");  
    }  
    return EXIT_SUCCESS;  
}  
```

**[strstr](http://www.cplusplus.com/reference/cstring/strstr/?kw=strstr)**
>功 能：在串中查找给定字符串的首次出现的地址  
>用 法： char *strchr(char *str, char c);  
>注意：返回一个指针，如果为NULL则没找到  
  
```c++
 int main ()  
 {
     char str[]="1234xyz";

     char *str1=strstr(str,"34");

     cout << str1 << endl;
 }
```

**[strpbrk](http://www.cplusplus.com/reference/cstring/strpbrk/)**
>功 能：在串中查找给定字符串的任何字符首次出现的地址  
>用 法： char * strpbrk ( const char *, const char * );   
>注意：A pointer to the first occurrence in str1 of any of the characters that are part of str2, or a null pointer  
```c
原型：
extern char *strpbrk(const char *s1, const char *s2);
char * strpbrk(const char * cs,const char * ct)
{
    const char *sc1,*sc2;
    for( sc1 = cs; *sc1 != '\0'; ++sc1)
    {
        for( sc2 = ct; *sc2 != '\0'; ++sc2)
        {
            if (*sc1 == *sc2)
            {
                return (char *) sc1;
            }
        }
    }
    return NULL;
}

#include <string.h>

int main ()
{
  char str[] = "This is a sample string";
  char key[] = "aeiou";
  char * pch;
  printf ("Vowels in '%s': ",str);
  pch = strpbrk (str, key);
  while (pch != NULL)
  {
    printf ("%c " , *pch);
    pch = strpbrk (pch+1,key);
  }
  printf ("\n");
  return 0;
}
```

**[strcspn](http://www.cplusplus.com/reference/cstring/strcspn/)**  
Get span until character in string  
**[strspn](http://www.cplusplus.com/reference/cstring/strspn/)**  
Get span of character set in string  
**[strerror](http://www.cplusplus.com/reference/cstring/strerror/)**  
char * strerror ( int errnum );  
通过标准错误的标号，获得错误的描述字符串 ，将单纯的错误标号转为字符串描述  
```c
#include <string.h>
#include <errno.h>

int main ()
{
  FILE * pFile;
  pFile = fopen ("unexist.ent","r");
  if (pFile == NULL)
    printf ("Error opening file unexist.ent: %s\n",strerror(errno));
  return 0;
}
```
* * *  



### 分割

**[strtok](http://www.cplusplus.com/reference/cstring/strtok/)**
>功 能：以指定分割符分解字符串为一组字符串  
>用 法：char *strtok(char *s, const char *delim);   
>注意：  
>1. 会改变源字符串，想要避免，可以使用strdupa（由allocate实现）或strdup（由malloc实现）；
>2. 线程不安全，使用内部静态变量来记录字符串中下一个需要解析的标记的当前位置, POSIX定义了一个线程安全的函数——[strtok_r](https://linux.die.net/man/3/strtok_r)，以此来代替strtok。_r表示可以重入(reentrant)；
>3. 到达末尾返回NULL   
  
```c
 void stokOption ()  
 {
    char optionstr[] = "XT:A:U  NM:i:0  XG:i:0  MD:Z:35";
    opt = strtok(optionstr, "\t");
    while (opt != NULL) {
        if (strlen(opt) > 0) {
            sscanf(opt, optionRule, optName, key);
            if (strcmp(optName, "XT") == 0)
                line.optField.xt = *key;
            else if (strcmp(optName, "NM") == 0)
                line.optField.nm = atoi(key);
            else if (strcmp(optName, "MD") == 0)
                strcpy(line.optField.md, key);
        }

        opt = strtok(NULL, "\t");    // continue previous
    }
 }
```
* * *

### 连接

**[strcat](http://www.cplusplus.com/reference/cstring/strtok/)**
>功 能：把src所指字符串添加到dest结尾处(覆盖dest结尾处的'\0')   
>用 法：char *strcat(char *dest, const char *src);   
>注意：src和dest所指内存区域不可以重叠且dest必须有足够的空间来容纳src的字符串;  
使用char *strncat(char *dest, const char *src, size_t n)更安全

 
  
```c
int main()
{
    char d[20] = "GoldenGlobal";
    char* s = "View";
    clrscr();
    strcat(d,s);
    printf("%s",d);
    getchar();
    return 0;
}
```
* * *
### 扫描输入

**[sscanf](https://www.tutorialspoint.com/c_standard_library/c_function_sscanf.htm)**
>功 能：从一个字符串中读进与指定格式相符的数据  
>用 法：int sscanf( string str, string format, mixed var1, mixed var2 ... );   
>注意：
sscanf与scanf类似，都是用于输入的，只是后者以屏幕(stdin)为输入源，前者以固定字符串为输入源。  
　　format可以是一个或多个 {%[*] [width] [{h | l | I64 | L}]type | ' ' | '\t' | '\n' | 非%符号}  
　　注：  
　　1、 *  (即 %*d 和 %*s) 加了星号 (*) 表示跳过此数据不读入.  
　　2、{a|b|c}表示a,b,c中选一，[d],表示可以有d也可以没有d。  
　　3、width表示读取宽度。  
　　4、{h | l | I64 | L}:参数的size,通常h表示单字节size，I表示2字节 size,L表示4字节size(double例外),l64表示8字节size。  
　　5、type :格式，如%s,%d
　　6、特别的：%*[width] [{h | l | I64 | L}]type   表示满足该条件的被过滤掉，不会向目标参数中写入值  
　　支持集合操作：  
　　%[a-z] 表示匹配a到z中任意字符，贪婪性(尽可能多的匹配)  
　　%[aB'] 匹配a、B、'中一员，贪婪性  
　　%[^a] 匹配非a的任意字符，贪婪性  
  
```c++
const static char mandoryRule[] = "%s\t%d\t%s\t%d\t%d\t%s\t%s\t%d\t%d\t%s\t%s\t%[^:]:%*[^:]:%[^:]"

char record[] = "CL100020961L1C001R001_738       16      chr18   56625123        0       35M     *       0       0       CCCATCTCTACTAAAAGTACAAAAATGTGCTGGGC     E>A?35@AEC=EEFFDCEBBEEDDEEEFEDCCDDF     XT:A:R ";

void checkRecord(char* record, SamLine& line)
{
    sscanf(record, mandoryRule, line.seqName, &line.flag, line.RefName, \
          &line.RefPos, &line.mapQ, line.cicarStr, line.mateRefName, &line.mateRefPos, \
          &line.tLen, line.readSeq, line.readQual, &str, &str2);
    
}
```
* * *

### 比较

**[strcmp](http://www.cplusplus.com/reference/cstring/strcmp/?kw=strcmp)**
>功 能：串比较  
>用 法：int strcmp(char *str1, char *str2);   
>注意：Asic码，str1>str2，返回值 >0；两串相等，返回0   
  
```c
 int main(void) {  
    //串比较  
    char *x = "woshixixihaha";  
    char *y = "woshixixihaha";  
    int ptr = strcmp(x, y);  
    if (ptr == 0) {  
        printf("相等");  
    } else {  
        printf("不相等");  
    }  
    return EXIT_SUCCESS;  
}  
```
* * *

### 复制

**[strcpy](http://www.cplusplus.com/reference/cstring/strcpy/?kw=strcpy)**
>功 能：拷贝字符串  
>用 法：char *stpcpy(char *destin, char *source);   
>注意：destin空间需要大于源source
  
```c
 int main(void) {  
    char x[10];  
    char *y = "hello";  
    stpcpy(x, y);  
    printf("%s\n", x);  
    return EXIT_SUCCESS;  
}  
```
**strdup**  
>char *strdup(const char *s);   
>strdup函数返回指向被复制的字符串的指针，所需空间由malloc()函数分配且可以由free()函数释放。stdrup可以直接把要复制的内容复制给没有初始化的指针，因为它会自动分配空间给目的指针。

**[strncpy](http://www.cplusplus.com/reference/cstring/strncpy/?kw=strncpy)**
>注意：比strcpy更安全，指定size，但注意size需要装下最后null terminator

* * *

### 反转
**[strrev](https://baike.baidu.com/item/strrev)**
>功能：字符串逆置
>用法：char *strrev(char *str)；
>注意：strrev()不会生成新字符串，而是修改原有字符串。因此它只能逆置字符数组，而不能逆置字符串指针指向的字符串，因为字符串指针指向的是字符串常量，常量不能被修改。 （string.h）（c++ std::reverse）

```c
char forward[] = "string";  
printf("Before strrev(): %s\n", forward);  
strrev(forward);  
printf("After strrev(): %s\n", forward);  
```


### [string](http://www.cplusplus.com/reference/string/string/?kw=string)  

**字符串内部**  

C中，字符串是以null teminator结尾的字符型数组

引用计数实现	 reference-counted implementation
减少同一数据的拷贝副本

写时复制		copy-on-write 
适应 string作为值参数（value parameter）及其他只读情形

**初始化**    
string duplicateChar (5, 'a');   
 不允许使用单个字符去初始化

**操作**  

string.substr （size_t pos = 0, size_t length = 0）
string.substr (index, 1) 	
string.substr （）复制整串

size = length
capacity () 当前分配存储的规模
（当系统进行存储空间再分配遇到偶数字（word，全整数full-integer）的边界时，会隐含增加一个字节，方便容纳空结束符）

reserve() 优化机制，预留空间
resize截短或追加，可指定填充字符

string.replace(pos, len, newchars) 	必要时扩增内存
将string看作STL序列，使用STL算法 replace(str.begin(), str.end(), 'x', 'y')

**查找**  
string::npos  空位置  
string.find (string, start_pos=0) 返回首次匹配的开始位置  
find_first_of 	第1个与指定字符组中任何字符匹配的pos  
find_last_of	最后1个...  
find_first_not_of 	第1个...任何字符都不匹配...  
find_last_not_of	最后...  
rfind 	逆向查找  

**改变大小写**  
C lib	  
toupper(char)   
tolower() 单个字符

### 归类


  
* **已经不赞成使用的函数归类**

函数名 | 用途 | 替换方案
--- | --- | ---
int bcmp(const void *s1, const void *s2, size_t n) | compare byte sequences                    |    memcmp
 void bcopy(const void *src, void *dest, size_t n)     |     copy byte sequence                        |    memcpy Or memmove
void bzero(void *s, size_t n)                          |    write zero-valued bytes                     |  memset
char *index(const char *s, int c);                      |    locate character in string                 |   strchr 
char *rindex(const char *s, int c);                      |   locate character in string                   | strrchr


* **内存或字符串查找函数归类**

函数名     |      用途     |      备注  
---|---|---
void *memchr(const void *s, int c, size_t n); |      scan memory for a character (Forward)    |   return a pointer to the matching byte or NULL if the character does not occur  in  the  given  memory area.  
void *memrchr(const void *s, int c, size_t n); |     scan memory for a character  (Backward)   |   UP  
 char *strchr(const char *s, int c);           |      locate character in string  (Forward)     |   return a pointer to the matched character or NULL ifcharacter is not found.  
char *strrchr(const char *s, int c);          |      locate character in string  (Backward)  |     UP  
char *strstr(const char *haystack, const char *needle); |      locate a substring        |         return a pointer to the beginning of the substring,if the substring is not found.  
char *strcasestr(const char *haystack, const char *needle);  | locate a substring,ignores the case of both arguments.   |  UP

* **内存及字符串拷贝、比较函数归类**

函数名     |      用途     |      备注  
---|---|---  
void *memcpy(void *dest, const void *src, size_t n);   |     copy memory area       | returns a pointer to dest.
void *memmove(void *dest, const void *src, size_t n);    |   copy memory area , may overlap    |    UP
int memcmp(const void *s1, const void *s2, size_t n);  |     compare memory areas   |           returns an integer less than, equal to, or greater than zero if the first n bytes of s1 is found
int strcmp(const char *s1, const char *s2);         |        compare two strings       |            return an integer less than, equal to, or greater than zero if s1 is foundfound
int strncmp(const char *s1, const char *s2, size_t n);  |    compare two strings          |         UP
int strcasecmp(const char *s1, const char *s2);       |      compare two strings ignoring case  |   UP
int strncasecmp(const char *s1, const char *s2, size_t n); | compare two strings ignoring case   |  UP
char *strdup(const char *s);              |                duplicate a string             |        returns a pointer to a new string which is a duplicate of the string s.  Memory for the new string is obtained with  


* **字符串测试归类**  

函数名 |  用途 | 备注  
--- |---|--- 
int isalnum(int c);     |                    英文或者数字               |       正确返回1，错误返回0
int isalpha(int c);      |                   英文字母            |              UP
int isascii(int c);         |                ASCII 码          |                UP
int isblank(int c);         |                a space or a tab         |             UP
int isgraph(int c);           |              可打印字符，不包括空格     |         UP 
int iscntrl(int c);           |              控制字符            |             UP         当c在0x00-0x1F之间或等于0x7F(DEL)时，返回非零值，否则返回零
int isdigit(int c);                |         十进制数字字符       |            UP               
int isprint(int c);               |          可打印字符，包括空格       |         UP
int ispunct(int c);             |            标点符号或特殊字符             |         UP
int isspace(int c);             |           space     |         UP
int isupper(int c);              |          大写英文字母                         |     UP       
int isxdigit(int c);              |         十六进制                      |        UP    

**[附注-ASCII](https://zh.wikipedia.org/wiki/ASCII)**  


* **字符串转换归类**    

函数名     |      用途     |      备注  
---|---|---   
double atof(const char *nptr);        |      float, double   |     不检查错误，不对就返回0
int atoi(const char *nptr);          |       to integer  |    UP
long long atoll(const char *nptr);    |      UP                           |       UP
float strtof(const char *nptr, char **endptr); |  转换float，endptr设置为数字后起始地址        |                      If endptr is not NULL, a pointer to the character after the last character used in the conversion is stored in the location referenced by
double strtod(const char *nptr, char **endptr); | double | UP
long int strtol(const char *nptr,char **endptr,int base); | 转换为长整数 | base 表示进制，取值[2, 36] or 0 (十进制)
int toascii(int c);            |             to ASCII     |     The value returned is that of the converted character.
int toupper(int c);              |           upper |  The value returned is that of the converted letter, or c if the conversion was not possible.
int tolower(int c);             |            UP                  |                UP
char *gcvt(double number, size_t ndigit, char *buf); | convert a floating-point | returns the address of the string pointed to by buf.  


* **内存控制类归纳**    

函数名     |      用途     |      备注  
---|---|---  
void *malloc(size_t size);        |          分配size Bytes               |                      默认不初始化
void *calloc(size_t nmemb, size_t size);  |  申请size个nmemb大小的空间       |        默认初始为0
void *realloc(void *ptr, size_t size);   |   扩展内存区域                    |        新扩展的部分默认不初始化
void free(void *ptr);                  |     释放内存区域              |              memcpy，memmove等操作使用不当可破坏内存边界，使free过度释放，破坏程序内存；free之后设为NULL，避免重复free



<html>
<font color=#0080FF size=4 face="微软雅黑"><b> The End </b></font>  
</html>  

![robot](https://image.ibb.co/equXa8/robot.jpg)