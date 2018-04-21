# CTF

##  1.  binwalk

- 2018.4.2----判断一个文件类型，并可以 自动提取 `binwalk -e [filename]`
- 2018.4.18---判断是否存在后门，原理未知



##  2.  Ziperello zip密码破解工具

##  3.  加密解密
-   回旋13踢
    -   ROT13（回转13位）是一种简易的替换式密码算法。
    -   解密 http://www.mxcz.net/tools/rot13.aspx

-   Bacon 加密法
    -   两个不同的符号，如 A 表示 0，B 表示 1。这个两个不同的符号，当然是可以其它的，如'+'和'-' 等，或者是不同的两种字体.  

    >​那么a到z对应的，密码表:  
    
        a AAAAA     g AABBA    n ABBAA    t BAABA
        b AAAAB    h AABBB   o ABBAB    u-v BAABB
        c AAABA    i-j ABAAA   p ABBBA    w BABAA
        d AAABB    k ABAAB    q ABBBB    x BABAB
        e AABAA    l ABABA    r BAAAA     y BABBA
        f AABAB    m ABABB    s BAAAB     z BABBB
    >  如果收到的密文是:
    AAAAB AAAAA ABAAA AAABB BAABB，则明文是 baidu， bajdu，baidv, bajdv， 我们就很容易知道它的正确意思是baidu.​

-   RSA
    -   第一步，随机选择两个不相等的质数p和q。
        -   爱丽丝选择了61和53。（实际应用中，这两个质数越大，就越难破解。）
    -   第二步，计算p和q的乘积n。
        -   爱丽丝就把61和53相乘。
        -   n = 61×53 = 3233
        -   n的长度就是密钥长度。3233写成二进制是110010100001，一共有12位，所以这个密钥就是12位。实际应用中，RSA密钥一般是1024位，重要场合则为2048位。
    -   第三步，计算n的欧拉函数φ(n)。
        -   根据公式：
            - φ(n) = (p-1)(q-1)
        -   爱丽丝算出φ(3233)等于60×52，即3120。
    -   第四步，随机选择一个整数e，条件是1< e < φ(n)，且e与φ(n) 互质。
        -   爱丽丝就在1到3120之间，随机选择了17。（实际应用中，常常选择65537。）
    -   第五步，计算e对于φ(n)的模反元素d。
        -   所谓"模反元素"就是指有一个整数d，可以使得ed被φ(n)除的余数为1。
            -   ed ≡ 1 (mod φ(n))
        -   这个式子等价于
            -   ed - 1 = kφ(n)
        -   于是，找到模反元素d，实质上就是对下面这个二元一次方程求解。
            -   ex + φ(n)y = 1
        -   已知 e=17, φ(n)=3120，
            -   17x + 3120y = 1
        -   这个方程可以用"扩展欧几里得算法"求解，此处省略具体过程。总之，爱丽丝算出一组整数解为 (x,y)=(2753,-15)，即 d=2753。
    -   第六步，将n和e封装成公钥，n和d封装成私钥。
        -   在爱丽丝的例子中，n=3233，e=17，d=2753，所以公钥就是 (3233,17)，私钥就是（3233, 2753）。
-   摩斯电码
-   凯撒
-   base32 64
    -   看到编码内容，只有大写和数字，根据Base64和Base32 区别：
        -   base64中包含大写字母（A-Z）、小写字母（a-z）、数字0——9以及+/；
        -   base32中只有大写字母（A-Z）和数字234567
## 4.   PHP
-   md5函数不能对数组进行处理

## 5.   Web
-   注意抓包
-   仔细观察
-   扫描发现了  .git    ???

-    注入：
     - 发现会网站会检查输入，过滤关键字，如：`index.php?id=1 order by 3 ` 会被过滤，可以考虑用如下的方式：
     - `index.php?id=1 or<>der by 3 `
     - `index.php?id=1 or/**/der by 3 `
-  `user.php`
-  `user.php.bak`
-  可以用浏览器修改浏览器内的标签