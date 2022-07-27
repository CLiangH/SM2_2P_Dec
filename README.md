项目目标
=

implement sm2 2P decrypt with real network communication

原理简介
=

![image](https://github.com/CLiangH/Picture/blob/main/SM22PD1.png)

代码解析
=

本项目为模仿真实世界通讯，创建了两个文件以模仿两位用户，两文件之间通过socket模块进行通信。

__用户A__
__________________

首先编写加密函数，求出C1,C2,C3，具体代码为：

`C1=T_mul(k,G) #C1=kG`

`R=T_mul(k,Pubk) #kP=(x2,y2)`
    
`t=SM3.SM3_test(str(R[0])+str(R[1])) #求解密钥t`
    
`C2=int(message)^int(t,16)`
    
`C3=hash(str(R[0])+message+str(R[1]))`

之后调用加密函数得到一组密文C1||C2||C3做例子
    
用户A求解出`T1=$d1^{-1}$G`并使用socket发送给用户B，等待B的操作。

从用户B那里接收T2，依照流程依次求出相关参数，直至得到$M^{''}$和u，若u==C3，则消息就是$M^{''}$。

__用户B__
__________________

用户B操作较为简单，只需使用socket接收A传来的T1，之后由T1计算T2，将T2传输回用户A即可。

运行指导
=

先打开用户A的进程，运行起来之后，打开用户B的进程即可成功运行。

运行截图
=

![image](https://github.com/CLiangH/Picture/blob/main/SM22PD2.png)










