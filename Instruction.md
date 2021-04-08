# x86架构条件跳转总结

## efl 状态标志位

|标志位|简称|置位含义|备注|
|:-:|:-:|:-:|:-:| 
|进位标志|CF|最高位向假象的位置进行借位或进位|常用于无符号数的运算|
|奇偶标志|PF|结果中最低8位中所有置位的总数为偶数个|上古时代用于对数据进行奇偶校验，检测数据是否出错|
|辅助进位|AF|低4位向高4位进行借位或进位|常用于BCD|
|零标志位|ZF|结果为0||
|符号标志|SF|结果为负||
|溢出标志|OF|次高位向最高位进行借位或进位|常用于有符号数的运算|

## 条件跳转指令

### 判断标志位

|助记符|标志位|英文|备注|场景|
|:-:|:-:|:-:|:-:|:-:|
|JS|SF=1|Jump if Sing|符号为负||
|JNS|SF=0|Jump if Not Sing|符号为正||
|JO|OF=1|Jump if Overflow|溢出||
|JNO|OF=0|Jump if Not Overflow|无溢出||
|JZ/JE|ZF=1|Jump if Zero/Equal|等于0/相等||
|JNZ/JNE|ZF=0|Jump if Not Zero/ Not Equal|不等于0/不相等||
|JP/JPE|PF=1|Jump if Parity/Parity Even|见标志位||
|JNP/JPO|PF=0|Jump if Not Parity/Parity Odd|见标志位||
|JL/JNGE|SF≠OF|Jump if Less/Not Greater or Equal|小于/不大于等于|有符号数比较|
|JNL/JGE|SF=OF|Jump if Not Less/Greater or Equal|不小于/大于等于|有符号数比较|
|JBE/JNA|CF=1或ZF=1|Jump if Below or Equal/Not Above|低于等于/不高于|无符号数比较|
|JNBE/JA|CF=0且ZF=0|Jump if Not Below or Equal/Above|不低于等于/高于|无符号数比较|
|JLE/JNG|SF≠OF或ZF=1|Jump if Less or Equal/Not Greater|小于等于/不大于|有符号数比较|
|JNLE/JG|SF=OF或ZF=0|Jump if Not Less or Equal/Greater|不小于等于/大于|有符号数比较|
|JC/JB/JNAE|CF=1|Jump if Carry/Below/Not Above or Equal|进位/低于/不高于等于|无符号数比较|
|JNC/JNB/JAE|CF=0|Jump if Not Carry/NotBelow/Above or Equal|无进位/不低于/高于等于|无符号数比较|

### 判断寄存器

|助记符|寄存器|备注|
|:-:|:-:|:-:|
|JCXZ|CX=0|CX=0跳转|
|JECXZ|ECX=0|ECX=0跳转|
|JRCXZ|RCX=0|RCX=0跳转|

## 移位指令

### 非循环移位

|助记符|类型|效果|备注|
|:-:|:-:|:-:|:-:| 
|SHL|逻辑左移|最高位进CF，最低位补0||
|SAL|算术左移|同SHL||
|SHR|逻辑右移|最低位进CF，最高位补0|常用于无符号数的运算|
|SAR|算术右移|最低位进CF，最高位保持不变|常用于有符号数的运算|

###循环移位

|助记符|类型|效果|备注|
|:-:|:-:|:-:|:-:| 
|ROL|循环左移|最高位复制到进CF和最低位||
|ROR|循环右移|最低位复制到进CF和最高位||
|RCL|带进位循环左移|最高位进CF，CF进最低位|首次移动要考虑原来的CF值|
|RCR|带进位循环右移|最低位进CF，CF进最高位|首次移动要考虑原来的CF值|

## 参考与引用

[1]Kip Irvine《汇编语言基于x86处理器》[M]机械工业出版社
[2]钱晓捷《微机原理与接口技术——基于IA-32处理器和32位汇编语言第5版》[M].机械工业出版社