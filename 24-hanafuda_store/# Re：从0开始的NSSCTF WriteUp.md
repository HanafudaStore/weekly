# Re：从0开始的NSSCTF WriteUp
### 1.[SWPUCTF 2021 新生赛]re1
下载附件后用IDA打开按F5即可看到反汇编后的代码如下
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SUEHC54yXqqSL8U5KysHXKQxNDqPnk7C2siilefnlhnLm3v9Xh8TrODW2qq8gqGf8Vxy4rXObe.E9abSmfXa7XM!/b&bo=EQNvAgAAAAADF00!&rf=viewer_4)
这里的代码表示在遍历Str1中的每一个元素，当遇到a(ASCII码值为97)或e(ASCII码值为101)时将它们分别替换为3和4(ASCII码值分别为51和52)，然后于于Str2比较。由此可逆向推导出flag为{easy_reverse},加上NSSCTF头提交即可

### 2.[SWPUCTF 2021 新生赛]简简单单的逻辑
打开附件中的python文件，该程序遍历一个数字列表，对每个列表元素进行位操作以计算出一个key，然后将flag变量的每个字符与这个key进行异或运算。result变量会累加异或运算的十六进制值并转为字符串。最终打印输出result
可根据这样的思路解出flag：
1.将 result 中的每对十六进制字符转换为整数
2.计算对应的key
3.反向执行异或操作以获取 flag 中每个字符的原始 ASCII 值
4.使用从列表计算出的 key 来解码原始信息
由此可写出解密代码：
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SQm5mAI1Z.9TnF7byUBGHD1WnxKuTdhw.kqKKQoYa*wSf2Lo5pfes0WAQuR1NM7Vtggkzke*dhGdVfn*.zQzTNQ!/b&bo=nwTVAgAAAAADF34!&rf=viewer_4)
说明：int()可进行强制类型转换，得到整型数据，要转换的数据后还可加上一个用逗号隔开的数字表示这是几进制的数据；str()可强制转换为字符串类型；对字符串进行操作时，+=进行的是字符串的拼接而不是相加！！！

### NSSCTF 2022 Spring Recruit]easy C
打开附件查看代码可知该程序在对输入的a字符串中的的数据每一项加1后与2异或后的值与b字符串进行比较。
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*Scse83QiRWbFKxkHQhznFqvFbeiyAxgamWShNkwZO2oEdVk.79Yw6q4SoSAXsRTplKTAH9Fxyas8S94xtT42WQc!/b&bo=WgK2AwAAAAADF98!&rf=viewer_4)
由此可反向推理写出解密代码：
![](https://a1.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SUOL0JHwaJNHz2cPhx4k1dQct4Z.NmRZbCk8ocGVPrdwvW2HVy370ULEPwUVzSwTGHL8qk2N6x94XrUK5bkFgpU!/b&ek=1&kp=1&pt=0&bo=SQJPAgAAAAADFzQ!&tl=1&vuin=934483106&tm=1730379600&dis_t=1730380221&dis_k=12f05ed960fa8f001fe381158f17fe5a&sce=60-2-2&rf=viewer_4)
注意：逆向操作时要注意顺序和对应运算的逆运算！！！

### [LitCTF 2023]世界上最棒的程序员
下载附件后用IDA打开按F5即可看到反汇编后的代码如下
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SZ2eWnJMqyarbnnqmpoyRzMcc0qV8EzxO6L0*9fWTg9Xvg7U4W1wPvJIl469Yu3VOyh3XbcH2Q0exkr5uqGhHCw!/b&bo=*wL0AAAAAAADBys!&rf=viewer_4)
点进start查看内容
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SUSV1mULupMHNi3af.WeJiO7t7ThKFJkkTEB.xGsmfjl5qVXsKFMhDJy7*nzjTF8K9yFaZv06HsVOut0WDyhCcY!/b&bo=3QKVAQAAAAADB2k!&rf=viewer_4)
可直接看到flag
### [LitCTF 2023]enbase64
下载附件后用IDA打开按F5即可看到反汇编后的代码如下
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*Seen9pnUcskVRvfVQUCRpz.4hy8XqvjxQxVnzOnq46HFjja89kUb3beKxqDCv05TERMDh95IzqhqTBswujKhiFE!/b&bo=OwX.AQAAAAADB.M!&rf=viewer_4)
由反汇编结果和题目提示可知进行的是Base64加密，但是用工具无法解密，推测其为换表的Base64.点开base64()函数继续分析
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SRTN4pIqfdsfk2uovSGVcbXgnNaZsFlnBlfLHzIS11iD9X25QvV6OEO4vK2t13bgwYvbRHE5xQKhzkgQFCOM6d0!/b&bo=RgMXAgAAAAADF2I!&rf=viewer_4)
继续打开Basechange函数查看换表的过程

![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*STTpF1*UEVG6pr5H0DamErgjqslTtMZ1kulr*DXnEY5*yYdyRMnrvjDwArIfmAEbbEfmzNJbAxVfTXBjNsLWnJM!/b&bo=MgE8AAAAAAADFz0!&rf=viewer_4)这里初始化了一个v3数组，使其成员全部为0
![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SWFVhi6iCtTb82fyipwkwLNLrF9KSYePW92Po9fkj0Ijp05PnXv5LpIrVUeaZVOyGFh9DUpRC1GsJyv0erpWzBo!/b&bo=0QHdAQAAAAADFz4!&rf=viewer_4)
最后将元素按照相应的方式打乱48次

注意：![](https://m.qpic.cn/psc?/V52mtLJJ3HJION2p4keN1yJtcH3fCpcu/LiySpxowE0yeWXwBdXN*SZ9.8vmHD1PqAnQbE5eUymOIf.tR5YatMGgLWM5m.FO4TCTQBN1.z3MhNjB9N0XXIZlcf8SSEUOys6xxaLMBT*g!/b&bo=rgByAAAAAAADF.4!&rf=viewer_4)

此处没有对v3操作的原因是其对应值为0，而所有元素为零的初始化设置在开头就已经说明，需特别注意