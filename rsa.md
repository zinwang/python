# RSA 加密演算法



## 簡介

​	RSA加密演算法是一種非對稱加密演算法。在公開金鑰加密和電子商業中RSA被廣泛使用。RSA是1977年由羅納德·李維斯特（Ron Rivest）、阿迪·薩莫爾（Adi Shamir）和倫納德·阿德曼（Leonard Adleman）一起提出的。當時他們三人都在麻省理工學院工作。RSA就是他們三人姓氏開頭字母拼在一起組成的。

​	RSA破解的難度就在於對超大的數做質因數分解。到目前為止，世界上還沒有任何可靠攻擊RSA演算法的方式。只要其鑰匙的長度足夠長，用RSA加密的訊息實際上是不能被破解的。



## RSA加解密步驟

​	1. 隨意選擇兩個大的質數  $p$ 和  $q$ ， 且 $p$ 不等於 $q$ ，計算  $n=p*q$ 。

​	2. 根據尤拉函數，求得 $\varphi(n) = (p-1)*(q-1)$ 。關於尤拉函數，等一下會證明。

​	3. 取一個很大的隨機數 $d$，使  $\gcd(d , \varphi(n)) = 1$ 。

​	4. 求得 $d​$ 的模反元素  $e​$ ，使  $e*d \equiv 1\quad(\mod \varphi(n))​$ ，且 $1<e<\varphi(n)​$ 。（模反元素存在，若且唯若 $e​$	與 $\varphi(n) ​$互質，可用輾轉相除法證明)

​	5. 銷毀 $p$ 、$q$ 。

​	6. < $n​$ , $e​$ > 作為用戶之公開鑰，於加密時使用。分發 $d​$ 給特定用戶(不公開)，於解密時使用。

​	

##### 	加密

​		$C\equiv M^{e}\quad\pmod n​$

##### 	解密

​		$M\equiv C^{d}\quad\pmod n​$

​	

​	($M​$ 為明文， $C​$ 為密文)



## 數論

​	本文章將探討RSA數學證明，會用到一點數論和同餘的觀念。



### 尤拉定理及費馬小定理



#### 	尤拉定理

​		若 $p$ 、 $a$ 為正整數，且 $p$ 、 $a$  互質（即 $\gcd(a,n)=1$），

​		則

​			$a^{{\varphi (p)}}\equiv 1\quad{\pmod  p}$

​		

​		即  $p$ 整除 $a^{\varphi(p)}-1$；φ(p)為尤拉函數，小於 $p$ 且跟 $p$ 互質的正整數個數。



#### 		證明

​	假設$a​$、 $p​$ 互質，令小於 $p​$ 且跟 $p​$ 互質的正整數集合為 $\{b_{1},b_{2},b_{3},b_{4} ......b_{\varphi(p)}\}​$ 

​	將這個集合的每個元素都乘 $a​$ ，變成 $\{b_{1}*a,b_{2}*a,b_{3}*a,b_{4}*a ......b_{\varphi(p)}*a\}​$ 

​	然後再將每個元素都模 $p​$ ，餘數所組成的集合剛好是 $\{b_{1},b_{2},b_{3},b_{4} ......b_{\varphi(p)}\}​$ 

​	的重新排列。因為 $a​$、 $p​$ 互質， $a​$ 不為 $p​$ 的倍數，對於任兩個相異 $b_{k}*a​$ 、 $b_{k+x}*a​$

​	 ($k=1,2,3,4......\varphi(p), x=1, 2,3,4......\varphi(p) , k+x \leq \varphi(p)​$ )

​	，其差不是 $p$ 的倍數（所以不會有相同餘數），且任一個 $b_{k}*a$ 亦不為 $p$ 的倍數（所以餘數不為 0）



​	所以說若把 $\{b_{1}*a,b_{2}*a,b_{3}*a,b_{4}*a ......b_{\varphi(p)}*a\}$ 裡的每個元素乘起來模 $p$，

​	餘數為  $\{b_{1},b_{2},b_{3},b_{4} ......b_{\varphi(p)}\}$ 所有元素的乘積，即:



​		 $(b_{1}*a)*(b_{2}*a)*(b_{3}*a)*(b_{4}*a) ......*(b_{\varphi(p)}*a)\equiv b_{1}*b_{2}*b_{3}*b_{4} ......*b_{\varphi(p)}\quad \pmod p$

​	

​	所以

​		

​		$a^{\varphi(p)}\equiv 1 \quad\pmod p​$



​	若 $p$ 為質數，則  $\varphi(p) = p-1​$ ，則:
​		

​		$a^{p-1}\equiv 1 \quad\pmod p$

​	

​	此即為費馬小定理。					

​	

### RSA證明

​	欲證:

​		若 $C\equiv M^{e}\quad\pmod n​$ ，則 $M\equiv C^{d}\quad\pmod n​$ 

​	證明:

​		1. 因為 $p$ 、 $q$ 為質數，小於 $n$ 且為 $p$ 倍數的正整數有 $q-1$ 個 ($1*p, 2*p, 3*p ......(q-1)*p$)；小		於 $n$ 且為 $q$ 倍數的正整數有 $p-1$ 個 ($1*q, 2*q, 3*q ......(p-1)*q$)。所以 小於 $n$ 且與 $n$ 互質的		正整數個數 $\varphi(n)$ 為 $n-1-(p-1)-(q-1)$ 

​			

​			$\varphi(n)=p*q-1-(p-1)-(q-1)=p*q-p-q+1=(p-1)*(q-1)​$ 

​		

​		得 $\varphi(n)=(p-1)*(q-1)$ 



​		2.因為 $e*d \equiv 1\quad\pmod {\varphi(n)}$ ， 所以 $e*d-1$ 被 $\varphi(n)$ 整除 ，令  $e*d-1=k*(\varphi(n)) , k\in $ 整		數

​		

​		3. 接下來討論



​		$p$ 、 $q$ 皆不整除 $M$ 時:

​			則 $\gcd(M,n)=1$ , 根據尤拉定理， $M^{\varphi(n)}\equiv 1 \quad \pmod n$

​	

​				$M^{e*d-1}=M^{k*\varphi(n)}\equiv M^{\varphi(n)}\equiv 1 \quad \pmod n$

​				$C^{d}\equiv (M^{e})^{d}\equiv(M^{e})^{d}*M\equiv M \quad \pmod n​$

​			

​			得 $M\equiv C^{d}\quad\pmod n​$ 



​		$p$ 、 $q$ 其中一數整除 $M$ ，另一數不整除 $M$ 時:

​			令  $p$ 整除 $M$ ， $q$ 不整除 $M$，則 $\gcd(M,q)=1$ , 根據尤拉定理， $M^{\varphi(q)}\equiv 1 \quad \pmod q$

​			

​				$M^{\varphi(n)}\equiv M^{(p-1)*(q-1)} \equiv 1^{(p-1)}\quad \pmod q$

​				$C^{d}\equiv (M^{e})^{d}\equiv(M^{e})^{d}*M\equiv M \quad \pmod q​$

​			

​			得 $C^{d}\equiv M\quad\pmod q​$ ， $C^d-M​$ 被 $q​$ 整除

​			又 $p​$ 整除 $M​$ ，$(M^e)^d​$ 被  $p​$ 整除

​			$\Rightarrow​$  $(M^e)^d-M​$ 被  $p​$ 整除 

​			$\Rightarrow​$   $C^d-M​$ 被 $p​$整除



​			$C^d-M​$ 被  $p​$ 、 $q​$  整除 

​			$\Rightarrow​$  $C^d-M​$ 被  $n​$ 整除

​			$\Rightarrow$ $C^{d}\equiv M\quad\pmod n$



​			得 $M\equiv C^{d}\quad\pmod n​$ 



​		$p$ 、 $q$ 皆整除 $M$ 時:

​			$p$ 、 $q$  整除 $M$ ，$(M^e)^d$ 被 $p$ 、 $q$  整除

​			$\Rightarrow​$  $(M^e)^d-M​$ 被  $p​$ 、 $q​$ 整除 

​			$\Rightarrow​$   $C^d-M​$ 被 $p​$ 、 $q​$ 整除

​			

​			$C^d-M​$ 被  $p​$ 、 $q​$  整除 

​			$\Rightarrow$  $C^d-M$ 被  $n$ 整除

​			$\Rightarrow$ $C^{d}\equiv M\quad\pmod n$



​			得 $M\equiv C^{d}\quad\pmod n​$ 



## 密鑰產生

在RSA中，$p​$ 、 $q​$  是隨機亂數產生數字，然後再透過一些方法測試該數是否為質數(參見補充資料)。獲得 $p​$ 與 $q​$ 的值後，接下來就是尋找  $d​$ 與 $e​$ 。$d​$ 由隨機產生，且 $\gcd(d,\varphi(n))=1​$ ，根據擴展歐基里德演算法(參見補充資料)， $d​$ 必有一個關於 $\varphi(n)​$ 的模反元素 $e​$，使 $e*d\equiv 1\quad \pmod {\varphi(n)}​$ 。



所以我們能透過擴展歐基里德演算法，令 $e*d+k*\varphi(n)=1​$ ($k​$ 為整數) 求得 $e​$ (等一下會實作)。



##### 擴展歐基里德演算法舉例

假設 $11*x+72*y=1​$



透過輾轉相除法:

​	

​	$72=11*6+6$

​	$11=6*1+5$

​	$6=5*1+1$



再整理成:



​	$6=72+11*(-6)​$	-------(1)

​	$5=11+6*(-1)​$	---------(2)

​	$1=6+5*(-1)$	-----------(3)



然後(2)代入(3)產生(4)， 將(1)代入(4)得 $x$ 、 $y$



​	$1=6+[11+6*(-1)]*(-1)$

​	$1=11*(-1)+6*2$	-----------------(4)

​	$1=11*(-1)+[72+11*(-6)]*2$

​	$1=11*(-13)+72*(2)​$



得 $x=-13, y=2​$





## RSA的特性

1. 其實 $e$  和 $d$ 是可互換的，如果 $e$ 作為 公鑰，則 $d$ 就為私鑰；若 $e$ 作為私鑰，則 $d$ 就作為公鑰。這點可以從 $ (M^e)^d =(M^d)^e\equiv M \quad \pmod n$ 看出。

   

2. $e​$ 、 $d​$  不能為 $2​$ ， 因為 $\gcd(e,\varphi(n))=\gcd(e,(p-1)*(q-1))=1​$ ， $\gcd(d,\varphi(n))=\gcd(d,(p-1)*(q-1))=1​$  ， $p​$ 、 $q​$  皆為奇質數，若 $e​$ 、 $d​$ 為 $2​$ ，與 $\varphi(n)=(p-1)*(q-1)​$  的最大公因數將為 $2​$ 。

   

3. 明文 $M$ 需小於 $n$  ，因為  $M\equiv C^{d}\quad\pmod n$  ，若 $M$ 大於 $n$ ，$M=C^d-k*n$ ($k\in$ 整數)，無法確定$M$ 是多少。





## RSA質因數分解攻擊

其實RSA的本質就是在做大整數的質因數分解，只要成功把 $n$ 分解成 $p$ 、 $q$  ，就能得到 $\varphi(n)$ ，搭配公鑰 $e$ ，就能推出 $d$。但是難就難在把 $n$ 質因數分解，現行的憑證 $n$大概 600多位數，要分解成兩個超大質數相乘難度超高，

因為人類到現在還沒有一張這麼大沒有遺漏的質數表。對於超大的 $n$ 質因數分解是幾乎不可能辦到的。



## Python工具實作





## 有趣的補充

1995年有人提出了一種非常意想不到的攻擊方式：假如監聽者對加密者的硬體有充分的了解，而且知道它對一些特定的訊息加密時所需要的時間的話，那麼她可以很快地推導出 $d​$ 。這種攻擊方式之所以會成立，主要是因為在進行加密時所進行的模指數運算是一個位元一個位元進行的，而位元為 1 所花的運算比位元為 0 的運算要多很多，因此若能得到多組訊息與其加密時間，就會有機會可以反推出私鑰的內容。





## 後序



## 補充資料

[<https://bindog.github.io/blog/2014/07/19/how-to-generate-big-primes/>](<https://bindog.github.io/blog/2014/07/19/how-to-generate-big-primes/>) RSA周邊——大素數是怎樣生成的？

[<https://zh.wikipedia.org/wiki/%E6%89%A9%E5%B1%95%E6%AC%A7%E5%87%A0%E9%87%8C%E5%BE%97%E7%AE%97%E6%B3%95>](<https://zh.wikipedia.org/wiki/%E6%89%A9%E5%B1%95%E6%AC%A7%E5%87%A0%E9%87%8C%E5%BE%97%E7%AE%97%E6%B3%95>) 擴展歐幾里得算法

[<https://zh.wikipedia.org/wiki/%E6%A8%A1%E5%8F%8D%E5%85%83%E7%B4%A0>](<https://zh.wikipedia.org/wiki/%E6%A8%A1%E5%8F%8D%E5%85%83%E7%B4%A0>) 模反元素



## 參考資料

[<https://zh.wikipedia.org/wiki/RSA%E5%8A%A0%E5%AF%86%E6%BC%94%E7%AE%97%E6%B3%95>](<https://zh.wikipedia.org/wiki/RSA%E5%8A%A0%E5%AF%86%E6%BC%94%E7%AE%97%E6%B3%95>) RSA加密演算法

[<https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%AE%9A%E7%90%86_(%E6%95%B0%E8%AE%BA)>](<https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%AE%9A%E7%90%86_(%E6%95%B0%E8%AE%BA)>) 尤拉定理

[<https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%87%BD%E6%95%B0>](<https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%87%BD%E6%95%B0>) 尤拉函數

[<https://zh.wikipedia.org/wiki/%E8%B4%B9%E9%A9%AC%E5%B0%8F%E5%AE%9A%E7%90%86>](<https://zh.wikipedia.org/wiki/%E8%B4%B9%E9%A9%AC%E5%B0%8F%E5%AE%9A%E7%90%86>) 費馬小定理

[<https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/537802/>](<https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/537802/>) 尤拉定理，費馬小定理證明









​                                                                                                                         				   Author: TNFSHchin























































































```<script type="text/javascript"
   src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```


