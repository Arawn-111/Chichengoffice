#AES加密算法
##介绍
AES(Advanced Encryption Standard)，从命名就可以看出（进阶版的加密标准），非常非常的正式奥，就和.com一样（来自没舍得花米购买.com域名的怨念阿巴阿巴）。事实上，确实是由NIST(Natural Institute of Standards and Technology,美国国家标准局)于2001年制定的“对称加密算法”，以取代当时已不安全的DES算法，是Rijndael算法的变体。每个数据块采用固定的128位，密钥块采用可选的128、192、256位。
本篇Note以AES-128-ECB为例，其中128指128位密钥块（其中长度不足128会自动填充0X00），ECB(Electronic Codebook)是一种对称密码分组模式。
##加密流程
128 bits密钥块，即16 bytes -> 16个格子
![16 bytes](https://sxyz.blog/images/AES/grid.png)
为保证安全，执行10轮（作为常数记住就好，是反复测试和研究的结果，得出的过程比较复杂，但切记，轮数不能多也不能少）
每一轮所进行的操作：
初始轮（1）
&emsp;&emsp;AddRoundKey
中间轮（2-9）
&emsp;&emsp;SubBytes：将数据块（每一个小方格）中数据映射到S-Box，目的是消除数据的特征（其本质固有的规律
&emsp;&emsp;ShiftRows：将数据块按行移位，进行混淆（螺旋升天
&emsp;&emsp;MixColumns：将数据块按列和一个由多项式构成的matrix，做矩阵乘法。目的是将单个错误扩散到整体，达到雪崩效应的预期，使其更难破解
&emsp;&emsp;AddRoundKey：将本轮的Key与数据块相加
最终轮（10）
&emsp;&emsp;SubBytes
&emsp;&emsp;ShiftRows
&emsp;&emsp;AddRoundKey
##解密流程
解密就是将加密反过来
###SubBytes
将4×4格子中的数据，映射到16×16的S-Box中
![映射](https://sxyz.blog/images/AES/sub-bytes.svg)
####S-Box
S-Box本质上就是一个input/output系统，输入，加工，输出，于是就有：
![Alt text](image.png)

