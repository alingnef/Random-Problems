<div style="text-align:center">
<h1>Random Number Generator (RNG)</h1>
</div>

Bản chất của tính ngẫu nhiên từ lâu đã gây trăn trở cho các triết gia, những nhà khoa học, các nhà thống kê và cả những người bình thường. Trong nhiều năm qua, con người đã đưa ra những câu trả lời khác nhau cho câu hỏi : **Dữ liệu như thế nào thì được xem là ngẫu nhiên, và bản chất của xác suất là gì???** 

Chuyển động của các hành tinh ban đầu trông có vẻ ngẫu nhiên và tùy tiện, nhưng rồi các nhà thiên văn học đầu tiên đã phát hiện ra trật tự và có thể đưa ra dự đoán về chúng. Tương tự như vậy, chúng ta đã đạt được những tiến bộ lớn trong việc dự đoán thời tiết và rất có thể sẽ tiếp tục tiến bộ hơn nữa.

Vì vậy, mặc dù ngày nay có vẻ như việc trời có mưa hay không trong một tuần tới là ngẫu nhiên, chúng ta vẫn có thể hình dung rằng trong tương lai, con người sẽ có thể dự đoán chính xác thời tiết. Ngay cả một thí nghiệm ngẫu nhiên quen thuộc – tung đồng xu – cũng có thể không ngẫu nhiên như bạn nghĩ : Lần tung thứ hai có thể sẽ cho kết quả giống với lần đầu tiên với **xác suất khoảng 51%**. (Tham khảo thí nghiệm về vấn đề này **[ở đây](https://www.stat.berkeley.edu/~aldous/Real-World/coin_tosses.html)**.)

Có thể tưởng tượng rằng vào một thời điểm nào đó, ai đó sẽ khám phá ra một hàm số $f$ nào đó sao cho : **Dựa vào kết quả của 100 lần tung đầu tiên bởi một người cụ thể, có thể dự đoán được giá trị của lần tung thứ 101 một cách chính xác.**

Trong tất cả các ví dụ trên, dù là chuyển động của hành tinh, thời tiết hay tung đồng xu – không thay đổi, chỉ có khả năng dự đoán của con người thay đổi. Vì vậy, ở một mức độ lớn, tính ngẫu nhiên là một hàm của người quan sát, hay nói cách khác :
>Khi một đại lượng quá khó để tính toán, ta có thể coi nó là ngẫu nhiên về mặt thực tiễn.</span>

---

Bây giờ, chúng ta sẽ bàn về vấn đề ngẫu nhiên trong việc sinh ra một con số tự nhiên nào đó để có thể thấy được những điều thú vị của chúng. 

# RNG
**RNG** là viết tắt của **Random Number Generator**, nghĩa là bộ sinh số ngẫu nhiên. Nó dùng để tạo ra một dãy số không thể đoán trước, không có quy luật. Các số trong dãy số đó có thể được dùng cho nhiều mục đích khác nhau, phổ biến nhất là dùng để sinh khóa cho các hệ mật như : RSA, AES, ECC,...

Dù là một công cụ rất hữu ích trong bảo mật, thế nhưng **RNG** lại mang cho mình những vấn đề khá là khó giải quyết hoặc khó có thể đưa ra một câu trả lời chuẩn xác trong thực tiễn.

Hãy thử giả sử rằng : Nếu như bây giờ tôi nói bạn hãy chọn ra một con số bất kì trong khoảng từ $1$ tới $10$ thì bạn sẽ chọn số nào? 

Có một **[khảo sát thực tế](https://www.reddit.com/r/dataisbeautiful/comments/acow6y/asking_over_8500_students_to_pick_a_random_number/?utm_source=chatgpt.com)** chỉ ra rằng, số $7$ thường được chọn nhiều hơn bởi vì : 
- Số $1$ và số $10$ ít được chọn nhất vì nhiều người cảm thấy chúng không trông giống như là ngẫu nhiên lắm. Và cũng bởi vì chúng là hai đầu mút trong dãy số mà người đặt câu hỏi đưa ra nên gần như chúng rất dễ để đoán nên sẽ bị loại trừ.
- Số $5$ là số nằm ở giữa khoảng $[1,10]$, nó thường được coi là không có bất ngờ vì chúng ta hay có xu hướng nghĩ rằng số ngẫu nhiên nên lệch một chút, chứ không đứng đúng ở giữa.
- Số $2$, $4$, $6$, $8$ là các số chẵn hay bị coi là “có quy luật”, dễ đoán. Trong vô thức, người ta ưu tiên số lẻ vì chúng có vẻ ngẫu nhiên hơn (không chia hết cho 2, không đối xứng).
- Bây giờ chỉ còn lại $3$, $7$ và $9$. Đến đây, số $9$ thường dễ bị loại bỏ vì tâm lý cũng giống với số $1$ : nếu là cuối danh sách, thì thường bị nghi ngờ là lựa chọn thiếu ngẫu nhiên. Ngoài ra, người ta thường không đếm tới $9–10$ trong đời sống thường ngày, nên nó cũng ít quen thuộc.
- Và cuối cùng, số $3$ thường sẽ bị loại bởi vì trông nó đã quá quen thuộc trong đời sống hằng ngày. Chúng ta thường hay đếm nhẩm từ $1$ tới $3$ thế nên nó là con số khá "tầm thường" để chọn.

Như vậy ta chỉ còn lại số $7$. Đến đây có một câu hỏi được đặt ra là : Liệu có phải có điều gì đó ngẫu nhiên bẩm sinh về số $7$ hay không? - Tất nhiên là **không**. Nếu tôi hỏi bạn hãy chọn ra một con số ngẫu nhiên và bạn chọn là $5$, làm sao để tôi biết được nó có ngẫu nhiên hay không? Nếu như tôi yêu cầu bạn làm lại và bạn liên tục đưa ra kết quả là $5$ thì rõ ràng số $5$ **không phải là số ngẫu nhiên.**

![{A209141A-93F5-4FFB-A620-49810FAC23A7}](https://hackmd.io/_uploads/SyUlwEH4ge.png)

Tính chất làm cho một con số trở nên ngẫu nhiên không nằm ở chính con số đó mà nằm ở chuỗi số chứa nó. Không hề có con số đơn lẻ nào là ngẫu nhiên cả. Ví dụ, số $1$, nếu như nó  chỉ là một lựa chọn duy nhất thì nó chẳng có gì là ngẫu nhiên cả. Nhưng nếu như ta thêm vào đó các số như : $5,2,8,7,4$ thì số $1$ khi này nó là một phần ngẫu nhiên của chuỗi đó. 

Như vậy có thể nói : 
>Một con số sẽ trông ngẫu nhiên khi được đặt trong một dãy không có quy luật rõ ràng.</span>

---

Một điều chắc chắn rằng : Khi tôi yêu cầu bạn chọn ra một số ngẫu nhiên, bạn sẽ có thể gần như trả lời được. Đó không phải là một việc gì khó cả. Tuy nhiên, đối với máy tính thì đó lại là một câu chuyện khác. 


Những cỗ máy tính từng đưa con người lên mặt trăng, hay những chiếc siêu máy tính hiện nay thường có xu hướng gặp khó khăn đối với một yêu cầu đơn giản như này. Vấn đề này không chỉ là vấn đề hạn chế về công nghệ mà nó còn đưa ra một câu hỏi triết học đầy khó khăn để trả lời : **Liệu ngẫu nhiên thực sự (True Randomness) có thực sự tồn tại?** 

Để trả lời cho câu hỏi đó, ta sẽ tìm hiểu về hai khái niệm rất quan trọng trong khoa học máy tính, toán học, triết học, đặc biệt trong lĩnh vực như lập trình, thuật toán, mã hóa, và mô phỏng : 
- Khái niệm về **Determinism (tính tất định)** : là tính chất mà trong đó một hệ thống, thuật toán hoặc quá trình luôn cho ra kết quả giống nhau nếu bắt đầu với cùng một đầu vào.
- Khái niệm về **Non-determinism (tính không tất định)** : Trái ngược với tính chất trên, khi có cùng một đầu vào thì hệ thống hoặc thuật toán có thể cho ra nhiều kết quả khác nhau mỗi lần chạy.

Đó chính là hai tính chất rất quan trọng để ta xây dựng nên các khái niệm, định nghĩa về hai nhánh nhỏ của RNG sau đây


## TRNG
**TRNG** là viết tắt của **True Random Number Generator** – Bộ sinh số ngẫu nhiên thực sự. Đây chính là thứ sẽ cho ta thấy được sự ngẫu nhiên tuyệt đối là như thế nào. Thật vậy, TRNG sẽ sinh ra những số hoàn toàn là ngẫu nhiên, không hề có quy luật nào cả. Kể cả khi bạn có cho đầu vào là một thứ gì đó xác định đi chăng nữa, thì với mỗi lần khởi động, chúng đều sẽ cho ra các kết quả khác nhau.

Một ví dụ rất hay cho vấn đề này chính là $100$ chiếc đèn dung nham (lava lamp) đặt tại trụ sở chính của Cloudflare ở San Francisco.

![image](https://hackmd.io/_uploads/rkaVztN4el.png)

Tại đây, một camera ghi hình liên tục các chuyển động hỗn loạn của đèn. Các pixel ảnh/video thu được được chuyển thành bit nhị phân. Sau đó, dữ liệu này được xử lý (băm, trộn, hash, entropy pool) để sinh ra các số ngẫu nhiên chất lượng cao dùng trong các công cụ bảo mật.


Có thể nói, đó chính là minh chứng cụ thể cho tính **Non-determinism (tính không tất định)**. Một trong các ví dụ về tính chất đó là **ý chí tự do của con người**. Nói một cách dễ hiểu, con người là những sinh vật khó đoán, không phải lúc nào họ cũng lý trí, thường thiên vị về một số xu hướng nhất định. Nhưng xét trên tổng thể, cuộc sống và sự lựa chọn của chúng ta rất hỗn loạn và khó đoán. Điều này đưa chúng ta trở lại câu hỏi ban đầu : **Tại sao máy tính không thể tạo ra một con số hoàn toàn ngẫu nhiên?**

Không có cách nào để máy tính tạo ra một chuỗi số thật sự hoàn toàn ngẫu nhiên. Đó không phải là một cỗ máy ngẫu nhiên. Tính ngẫu nhiên vốn không thể đoán trước và không mang tính xác định. Và rõ ràng, máy tính không hoạt động dựa trên sự hỗn loạn, chúng làm việc theo nguyên tắc có trật tự. Đầu ra của một chương trình máy tính mang tính xác định và do đó có thể dự đoán được.

Nhưng nếu đúng là như vậy, làm sao vẫn có thể tồn tại cơ chế ngẫu nhiên như hòm may mắn trong các trò chơi điện tử hay sòng bài trực tuyến? Để trả lời cho câu hỏi đó, ta sẽ đến với thứ cùng tồn tại song song với TRNG, đó là PRNG.



## PRNG
**PRNG** là viết tắt của **Pseudo-Random Number Generator** - Bộ sinh số giả ngẫu nhiên. Gần giống với TRNG, thế nhưng PRNG sẽ sinh ra các số trông có vẻ ngẫu nhiên, nhưng thực chất là xác định (deterministic), được tạo ra từ một thuật toán và một giá trị khởi tạo gọi là `seed`.

Chúng ta phải tạo ra một chuỗi số mà trông nó có vẻ ngẫu nhiên đối với chúng ta. Nhưng suy cho cùng chúng không phải là ngẫu nhiên. Đó chính là công việc của PRNG.

Về cơ chế của một PRNG, ta có cấu trúc tổng quát chung về nó như sau : 
- Để có thể tạo ra một số nào đó ngẫu nhiên, ta sẽ thiết lập một bộ sinh số dựa theo cấu trúc chính đó là : Từ một số ban đầu, gọi là **seed**, ta sẽ sinh ra một số mới dựa trên **seed** đó thông qua một hàm tuyến tính $f$ nào đó. Hay ta có công thức tổng quát như sau:

$$
\text{Random\ Number}=f(seed)
$$

- Với một số ngẫu nhiên mới sinh ra, ta đều mong muốn đầu vào của nó luôn được thay đổi, bởi lẽ hàm $f$ là một hàm tuyến tính xác định, nó chỉ cho ra một giá trị **xác định duy nhất** với mỗi giá trị đầu vào.
- Giả sử ta có một giá trị khởi tạo ban đầu là : $s_0$ 
- Giá trị được gọi là **seed**, đó là giá trị hoàn toàn ngẫu nhiên, có thể là do bạn tự nghĩ ra hoặc ai đó chọn, không sao cả. Bây giờ, ta sẽ dùng giá trị ban đầu đó mà tạo ra được một chuỗi số trông có vẻ như là ngẫu nhiên.
- Ta sẽ định nghĩa hai hàm $f(x)$ và $g(x)$ như sau : 
    - Với $f(x)$ : Ta xem đó như là một hàm để sinh ra trạng thái tiếp theo của một PRNG, hay nói đúng hơn là hàm sinh ra đầu vào tiếp theo của một PRNG. Khi đó ta có công thức sau : $$s_{n+1}=f(s_n)$$
    - Với $g(x)$ : Hàm này sẽ nhận vào một giá trị xác định $s$ làm đầu vào để từ đó sinh ra một giá trị xác định $r$ và dùng nó cho các hoạt động bảo mật. Công thức như sau : $$r_i=g(s_i)$$

- Hai hàm $f(x)$ và $g(x)$ đều được thiết kế tùy theo mong muốn của người tạo ra nó. Điều quan trọng nhất của việc thiết kế các hàm này là chúng phải là hàm một chiều, tức nếu như kẻ tấn công biết được cấu trúc của $f(x)$ và $g(x)$ thì việc đảo ngược chúng sẽ rất khó khăn, hoặc thậm chí là không thể, và thứ hai là không được để lộ **“cửa sau” (backdoor)**, tức nó cho phép kẻ thứ ba can thiệp vào dữ liệu nhạy cảm mà người dùng không cho phép.

- Như vậy, với mỗi đầu vào $s_i$ khác nhau, ta sẽ sinh ra được các số ngẫu nhiên $r_i$ mà khi nhìn vào ta đều sẽ khó đoán được quy luật của chúng. 

Sơ đồ tổng quát của một PRNG như sau :

![{4047A127-CC22-4A7E-873B-63A80413C6AF}](https://hackmd.io/_uploads/rkWbfew4gg.png)


Hãy thử giả sử như này : 
- Chúng ta có một giá trị ban đầu là : $X_0$
- Giá trị đó là ngẫu nhiên, có thể là do bạn tự nghĩ ra hoặc ai đó chọn, không sao cả. Bây giờ, ta sẽ dùng giá trị ban đầu đó mà tạo ra được một chuỗi số trông có vẻ như là ngẫu nhiên. 
- Ta sẽ nhân giá trị ban đầu đó với một giá trị $a$ lớn nào đó để có được số $aX_0$. Chúng vẫn chưa hề được xem như là ngẫu nhiên vì vẫn còn dễ đoán.
- Tiếp theo, vì đã nhân nên ta có thể thêm vào đó một phép toán cộng với một số nào đó (tất nhiên có thể là trừ nhưng bản chất của phép trừ một số chính là cộng số đối của chính số đó). Ta gọi số cộng thêm là $c$. Đến đây nó vẫn chưa được gọi là ngẫu nhiên.
- Và cuối cùng, ta sẽ đem con số mà ta vừa mới tính được là $aX_0+c$ đem đi lấy phần dư cho một con số $m$ nào đó. Hay nói đúng hơn ta sẽ có một con số cuối cùng là $(aX_0+c)$ % $m$.
- Chúng ta đã tạo ra cho mình một con số trông có vẻ là ngẫu nhiên, tuy nhiên nó vẫn còn thiếu một thứ. Như đã nói, một con số sẽ trông ngẫu nhiên khi được đặt trong một dãy không có quy luật rõ ràng. Thứ chúng ta thiếu ở đây chính là những con số khác. Vậy thì ta phải làm sao? 
- Đơn giản, ta đặt : 
$$
X_1=(aX_0+c)\text{ % }m
$$ 
Khi này để tính được giá trị tiếp theo, ta chỉ cần thay thế $X_1$ vào vị trí của $X_0$ thì khi đó ta sẽ có : 
$$
X_2=(aX_1+c)\text{ % }m
$$ 
Cứ như thế, ta sẽ rút ra được công thức tổng quát cho chuỗi số như sau : 
$$
X_{n+1}=(aX_{n}+c)\text{ % }m
$$ 

- Đó chính là ví dụ cơ bản của một PRNG, hay nói chính xác hơn, đó là **LCG - Linear Congruential Generator** (Bộ sinh số giả ngẫu nhiên tuyến tính theo đồng dư) mà ta sẽ nói rõ ở phần sau. 

- Có thể nói, dựa theo công thức truy hồi như trên, ta đã phần nào hiểu được vai trò của phép Modulo $m$ là giữ cho bộ số sinh ra đều nằm dưới $m$. Nếu không có phép tính đó thì các con số về sau sinh ra sẽ ngày càng lớn bởi lẽ khi này, bộ sinh số của ta sẽ là hàm tuyến tính bậc nhất có xu hướng đi lên dạng $y=ax+b,\hspace{2mm}a>0$.
- Thế nhưng, Modulo $m$ cũng chính là lý do lớn nhất để ta gọi chúng là giả ngẫu nhiên (Pseudo-Random). Bởi vì đến một lúc nào đó, dù sớm hay muộn, chúng sẽ sinh lại các con số đã sinh trước đó. Và cứ như thế, một vòng lặp sẽ diễn ra. Ví dụ cơ bản nhất là khi ta có một LCG có dạng : $X_{n+1}=(2X_{n}+2)\text{ % }8$.
- Với $X_0=1$ thì ta có $X_1=4$, $X_2=2$, $X_3=6$, $X_4=6$, $X_5=6$,... Hàm sinh số này sẽ luôn bị kẹt mãi ở số $6$, khiến cho nó trở nên không còn là ngẫu nhiên trong mắt chúng ta nữa.


Cũng bởi chính vì các ví dụ minh họa như trên, ta gọi các con số như trên là các con số giả ngẫu nhiên được sinh ra từ một PRNG bởi vì chúng trông giống như ngẫu nhiên nhưng chúng không thật sự ngẫu nhiên. Và đó chính là minh chứng cụ thể cho tính **Determinism (tính tất định)** mà ta đã nói ở trên.

Còn bây giờ ta sẽ tìm hiểu về một số PRNG phổ biến trong đời sống của chúng ta.

---

### LCG - Linear Congruential Generator
**Linear Congruential Generator** là một thuật toán PRNG (pseudo-random number generator) — sinh ra dãy số có vẻ ngẫu nhiên bằng cách dùng phép toán đồng dư tuyến tính.

Công thức của LCG là : 
$$
X_{n+1}=(aX_{n}+c)\text{ % }m
$$

Trong đó : 
- $a$ được gọi là Hệ số nhân (multiplier - mul)
- $c$ được gọi là Hệ số cộng (increment - inc)
- $m$ được gọi là số của phép toán Modulo (mod), tượng trưng cho phạm vi của các số được sinh ra.

Một giá trị ban đầu là $X_0$ sẽ được gọi là **seed** của bộ sinh số LCG, sẽ được dùng để sinh ra các số giả ngẫu nhiên phía sau.

Việc chọn các tham số cho LCG là rất quan trọng vì chúng sẽ ảnh hưởng tới chu kì sinh số của LCG. Chọn không cẩn thận sẽ khiến cho LCG sinh số bị sai hoặc không đầy đủ như ví dụ trên. Để khắc phục và đảm bảo cho LCG hoạt động hiệu quả nhất, **định lý Hull–Dobell** đã ra đời để thực hiện điều đó.

Cụ thể, định lý phát biểu như sau : 
> Để LCG đạt chu kỳ đầy đủ $=m$ (tức là sinh ra tất cả các số từ $0$ đến $m−1$, không trùng lặp sớm) nếu và chỉ nếu $3$ điều kiện sau đều đúng : 
> - $gcd(c,m)=1$.
> - Với mỗi $p$ là ước số nguyên tố của $m$ thì $(a-1)$ chia hết cho $p$.
> - Nếu $m$ chia hết cho $4$ thì $(a-1)$ cũng chia hết cho $4$.

Ví dụ : Ta xét hai hàm sinh số LCG $L_1$ và $L_2$ như sau : 
$$
\begin{cases}
L_1:X_{n+1}=(5X_{n}+5)\text{ % }16\\
L_2:X_{n+1}=(2X_{n}+2)\text{ % }15
\end{cases}
$$

Xét hàm $L_1$ ta có : 
- $gcd(5,16)=1$
- $m=2^4\Rightarrow p=2\Rightarrow (5-1)=4\hspace{2mm}\vdots\hspace{2mm} 2$
- $16\hspace{2mm}\vdots\hspace{2mm} 4$ và $4\hspace{2mm}\vdots\hspace{2mm} 4$

Như vậy có thể nói : $L_1$ **đạt chu kỳ đầy đủ**
Code minh họa : 
```python
class LCG:
    mul = 5
    inc = 5
    mod = 16

    def __init__(self, seed):
        self.state = seed

    def next(self):
        self.state = (self.state * self.mul + self.inc) % self.mod
        return self.state

x = LCG(1)
ls = []
for _ in range(16):
    ls.append(x.next())
    #print(x.next())

sum = 0
for i in ls:
    sum += i
print(ls)
print(sum == 0+1+2+3+4+5+6+7+8+9+10+11+12+13+14+15) #True
```

Xét hàm $L_2$ ta có : 
- $gcd(2,15)=1$
- $m=3.5\Rightarrow p_1=3, p_2=5\Rightarrow\hspace{2mm}1\nmid 3\text{ và }1\nmid 5$

Có thể thấy, vì điều kiện thứ hai không thỏa mãn nên ta không cần xét điều kiện thứ ba mà có thể kết luận ngay $L_2$ **không đạt chu kỳ đầy đủ**.
Code minh họa : 
```python
class LCG:
    mul = 2
    inc = 2
    mod = 15

    def __init__(self, seed):
        self.state = seed

    def next(self):
        self.state = (self.state * self.mul + self.inc) % self.mod
        return self.state

x = LCG(1)
ls = []
for _ in range(8):
    ls.append(x.next())
    #print(x.next())
print(ls)
# [4, 10, 7, 1, 4, 10, 7, 1]
```

---

### LFSR - Linear-Feedback Shift Register
**LFSR** là viết tắt của **Linear-feedback shift register** (Thanh ghi dịch phản hồi tuyến tính) là một cấu trúc đơn giản dùng để sinh các dãy bits giả ngẫu nhiên dựa trên phép dịch và phép phản hồi tuyến tính. Cụ thể hơn ta có thể phân tích ý nghĩa của tên bộ sinh số này như sau : 
- **Register** : Nói một cách đơn giản, register là một vùng lưu trữ dễ truy cập mà bộ xử lý (CPU) sử dụng để lưu trữ dữ liệu mà nó cần thao tác. Trong kiến trúc máy tính, các thanh ghi là lựa chọn nhanh nhất để truy xuất dữ liệu. Tuy nhiên, trong bối cảnh LFSR dùng cho mật mã, điều bạn cần biết là register đơn giản chỉ là một vùng lưu trữ (bộ chứa dữ liệu) mà thôi. Ví dụ về một Register : 
![image](https://hackmd.io/_uploads/rJxzENDExx.png)

- **Shift** : Tại đây, dãy bit trong thanh ghi sẽ được dịch sang trái hoặc sang phải. Ta có thể giả sử rằng nó dịch sang phải, khi đó bit cuối cùng của thanh ghi sẽ bị “dịch ra ngoài” khỏi thanh ghi và có thể được đưa vào xử lý bởi một tiến trình bên ngoài. Hãy tưởng tượng chúng ta muốn dùng cơ chế này để tạo ra một chuỗi bit ngẫu nhiên (bit stream). Trong ví dụ dưới đây, ta sẽ lần lượt nhận được các giá trị 0, sau đó 1, rồi 0, và cứ tiếp tục như vậy. Trong ví dụ này, ta cũng giả định rằng các vị trí trống ở bên trái sau khi dịch chuyển sẽ được lấp đầy bằng các số 0.
![image](https://hackmd.io/_uploads/ry31HVw4ge.png)

- **Feedback** : Trong quá trình dịch (Shift) như vậy thì đến một lúc nào đó thanh ghi sẽ chỉ toàn là bit $0$. Khi đó chuỗi bit (bit stream) mà ta thu được cũng chẳng còn gì hấp dẫn nữa. Để khắc phục điều đó ta sẽ thêm vào một cơ chế phản hồi (feedback mechanism). Cụ thể, ta sẽ thực hiện phép XOR một số giá trị trong thanh ghi lại với nhau và dùng kết quả đó làm giá trị đầu vào, thay vì lúc nào cũng nhét số $0$ vào như trước. Trong LFSR, các vị trí trong thanh ghi được chọn để thực hiện phép XOR gọi là **taps** (các điểm gõ hoặc điểm lấy mẫu). Trong ví dụ này, ta sẽ “tapped” (lấy mẫu) bốn bit, tính từ trái sang phải, đó là các bit ở vị trí chỉ số $1,2,4,6$ (với bit bên trái nhất là bit thứ $0$).
![image](https://hackmd.io/_uploads/SJDCrNPEee.png)

- **Linear** : Bây giờ hãy nói đến phần cuối cùng trong cụm từ LFSR, chính là từ linear (tuyến tính). Thực ra phần này cũng khá đơn giản thôi. Hàm mà chúng ta sử dụng để tạo ra bit thay thế chính là phép XOR. Và như bạn có thể đoán được, phép XOR trên các bit đơn lẻ là một hàm tuyến tính, đó là lý do vì sao chúng ta thêm từ linear vào trước từ feedback trong tên gọi, để mô tả loại phản hồi mà hệ thống đang sử dụng.

Đó chính là ý nghĩa của tên bộ sinh số giả ngẫu nhiên này. Thông qua cái tên ta cũng phần nào hiểu được cơ chế họat động của nó. Và cũng giống như các PRNG khác, LFSR cũng sẽ yêu cầu một **seed** ban đầu để khởi tạo lên bộ PRNG này. Trong ví dụ trên, seed của ta có thể coi là một mảng bit là $(1,0,0,1,0,1,0)$.

Bên cạnh đó, LFSR là hệ thống xác định (**deterministic**). Nghĩa là, nếu bạn biết seed ban đầu và vị trí các **taps** không thay đổi, bạn sẽ luôn thu được cùng một chuỗi bit đầu ra.

Một hệ quả khác của tính xác định này là dù sớm hay muộn, chúng ta sẽ rơi vào một chu kỳ lặp lại của các trạng thái nội bộ. Khi giá trị trong thanh ghi quay trở lại một trạng thái mà trước đó đã xuất hiện, toàn bộ quá trình dịch bit và tính toán phản hồi sẽ lặp lại.

Chu kì của một LFSR phụ thuộc rất lớn vào việc chọn các **taps**. Có những vị trí **taps "tốt"** được nghiên cứu và lựa chọn dựa trên độ dài thanh ghi để tối đa hóa chu kỳ lặp. Có thể tham khảo **[ở đây](https://en.wikipedia.org/wiki/Linear-feedback_shift_register#Example_polynomials_for_maximal_LFSRs)**.

Nhìn chung, chu kỳ tối đa mà một LFSR có thể đạt được là $(2^n - 1)$, trong đó $n$ là kích thước của thanh ghi. Điều này hoàn toàn hợp lý vì với một thanh ghi có kích thước cố định, số lượng trạng thái khác nhau là hữu hạn (trừ trường hợp tất cả các bit đều bằng 0, trạng thái này thường không sinh thêm giá trị mới nên bị loại trừ).

Một LFSR đạt được chu kỳ tối đa $(2^n - 1)$ được gọi là **Maximal LFSR**, và đây là loại được ưu tiên sử dụng trong các ứng dụng yêu cầu chuỗi bit dài và khó dự đoán hơn.

Code ví dụ : 
```python
class LFSR:
    def __init__(self, seed):
        if len(seed) != 7:
            raise ValueError("Seed phải có đúng 7 bit")
        self.register = seed.copy()

    def next(self):
        taps = [1, 2, 4, 6] 
        feedback = 0
        for t in taps:
            feedback ^= self.register[t]
        
        output_bit = self.register[-1] 

        for i in range(len(self.register) - 1, 0, -1):
            self.register[i] = self.register[i - 1]

        self.register[0] = feedback  
        return output_bit 
    
    def run(self, steps):
        output = []
        for _ in range(steps):
            out_bit = self.next()
            output.append(out_bit)
        return output


seed = [1, 0, 0, 1, 0, 1, 0]
lfsr = LFSR(seed)

print(f"Dãy bit sinh ra là : {lfsr.run(20)}")
```

Ngoài lý thuyết cơ bản trên, ta cũng sẽ tìm hiểu thêm về một phần rất là quan trọng khác, đó là đa thức đặc trưng (Characteristic Polynomial) trong LFSR. 

---

**Đa thức đặc trưng** (Characteristic Polynomial) là một cách biểu diễn quá trình Feedback của LFSR bằng cách cho ta biết độ dài của thanh ghi và vị trí các taps tham gia vào quá trình XOR. 

Như ta đã biết về cấu trúc của LFSR, phần Feedback sẽ là một hàm để tính giá trị tiếp theo trong thanh ghi


Trước hết ta có thể hiểu một thanh ghi sẽ có $n$ ô, với mỗi ô có giá trị $s_i\in [0,1]$ và một bộ hệ số $c_i\in [0,1]$ với $i\in [0, n-1]$ 

Một hàm Feedback với phép cộng Modulo $2$ (hay phép XOR) dùng để tính toán giá trị state mới $s_n$ bằng cách sử dụng các state và hệ số trước đó dưới dạng phương trình : 
$$
s_n\equiv c_0s_0+c_1s_1+...+c_{n-1}s_{n-1}\pmod{2}
$$

$$
\Leftrightarrow s_n=c_0s_0\oplus c_1s_1\oplus ...\oplus c_{n-1}s_{n-1}
$$

Sau đó, thanh ghi sẽ dịch sang phải (tùy trường hợp nó có thể dịch sang trái) và sẽ thêm giá trị vừa mới tính vào bên trái nhất : 
$$
(s_{n-1},s_{n-2},...,s_1,s_0)\rightarrow(s_{n},s_{n-1},...,s_2,s_1)
$$

Tham khảo ở hình vẽ này : 
![{7A43D941-8861-40CC-BE93-BEDDFB2F208C}](https://hackmd.io/_uploads/B1qUal3Nxg.png)



Ở đây ta có một thanh ghi có độ dài là $4$ bits và hãy giả sử ta có một vector state là $(s_3,s_2,s_1,s_0)$ và một vector hệ số là $(c_3,c_2,c_1,c_0)$

Với $s_0$ là output của LFSR sau mỗi lần dịch sang phải, ở bên trái khi này đang trống $1$ bit, ta sẽ tính giá trị state $4$ vào trong đó bằng cách : 
$$
s_4\equiv c_3s_3+c_2s_2+c_1s_1+c_0s_0\pmod{2}
$$


Có thể nói, các hệ số đó tượng trưng cho việc giá trị tại $s_i$ có tham gia vào quá trình Feedback hay không. Ta có lấy một ví dụ như sau : 

- Cho vector hệ số $(c_3,c_2,c_1,c_0)=(1,1,1,1)$ và vector state ban đầu là $(s_3,s_2,s_1,s_0)=(0,0,0,1)$, ta sẽ tính giá trị tiếp theo $s_4$ như sau : 
$$
s_4\equiv c_3s_3+c_2s_2+c_1s_1+c_0s_0\pmod{2}
$$

$$
\Leftrightarrow s_4\equiv 1.0+1.0+1.0+1.1\pmod{2}
$$

$$
\Leftrightarrow s_4\equiv 1\pmod{2}
$$

- Khi đó, ta có state mới là $(s_4,s_3,s_2,s_1)=(1,0,0,0)$
- Tiếp tục dựa theo các tính đó, ta có $s_5$ là : 
$$
s_5\equiv c_3s_4+c_2s_3+c_1s_2+c_0s_1\pmod{2}
$$

$$
\Leftrightarrow s_5\equiv 1.1+1.0+1.0+1.0\pmod{2}
$$

$$
\Leftrightarrow s_5\equiv 1\pmod{2}
$$
- Và có state mới là : $(s_5,s_4,s_3,s_2)=(1,1,0,0)$

Bằng cách tính liên tục theo quy trình như vậy ta sẽ có : 

![{F94015DD-2750-4287-8630-DC9DF8748F0B}](https://hackmd.io/_uploads/SyevW8hElg.png)


Như đã nói, đến một lúc nào đó ta sẽ quay trở lại trạng thái ban đầu, như trong ví dụ trên, chu kì của LFSR với state khởi tạo này là $5$. Chí ít thì điều đó nó vẫn còn tốt hơn so với việc state của ta chỉ toàn là $0$. Bởi vì khi đó giá trị tiếp theo của ta sẽ là : 
$$
s_4\equiv c_3.0+c_2.0+c_1.0+c_0.0\equiv 0\pmod{2}
$$

Với mỗi thanh ghi có độ dài là $n$, với từng giá trị $s_i\in [0,1]$ thì tổng số trường hợp có thể là $2^n$. Tuy nhiên, trong đó cũng bao gồm luôn trường hợp state toàn là số $0$. Như thế là không được đối với LFSR. Chính vì vậy, một LFSR có thể có tới $2^n-1$ state có thể, với trường hợp toàn là số $0$ đã bị loại trừ.

Hãy đặt một ví dụ khác : Cho vector hệ số $(c_3,c_2,c_1,c_0)=(0,0,1,1)$ và vector state ban đầu là $(s_3,s_2,s_1,s_0)=(0,0,0,1)$, ta sẽ tính giá trị state tiếp theo như sau : 

![{5B06007D-2849-44DC-A8C9-90828845C0D9}](https://hackmd.io/_uploads/HJKr-83Vlg.png)


Có thể thấy, vẫn sử dụng lại state ban đầu ở ví dụ trên, lần này ta thay đổi hệ số đi thì ta đã thu được chu kì là $15$. Đó cũng chính là chu kì tối đa của một LFSR dài $4$ bits là : $2^4-1=15$

Có thể thấy, chu kì của LFSR $4$-bits này sẽ luôn luôn là $15$ với mọi giá trị state đầu vào bất kì, tất nhiên là trừ trường hợp tất cả bằng $0$. Nói chung, chu kì của một LFSR là một hàm tuyến tính có vector hệ số và vector state khởi tạo

Ở ví dụ đầu tiên, ta có vector hệ số là $(c_3,c_2,c_1,c_0)=(1,1,1,1)$. Với hệ số này, chu kì của LFSR sẽ luôn luôn là $5$ bất kể đầu vào có là gì đi nữa. Minh họa : 

![{121EBB4B-2D18-4CE5-8A17-7A39500F5EE1}](https://hackmd.io/_uploads/BkEEWIn4xg.png)







Như vậy, dựa vào lý thuyết về các hệ số và giá trị state như ở trên, ta sẽ rút ra được một định nghĩa về Đa thức đặc trưng (Characteristic Polynomial) như sau : 

- **Định nghĩa** về **Đa thức đặc trưng** (Characteristic Polynomial) : Cho thanh ghi có độ dài $n$ bits, được sắp xếp theo thứ tự : $s_{n-1}s_{n-2}...s_1s_0$ cùng với đó là vector hệ số $(c_{n-1},c_{n-2},...,c_1,c_0)$. Khi đó, đa thức đặc trưng bậc $n$ là : 
$$
c(x)=x^n+c_{n−1}x^{n−1}+c_{n−2}x^{n−2}+···+c_1x+c_0
$$

>Trong đó : 
>- $c_0=1$. 
>- $x^n$ và $c_0$ sẽ luôn có mặt vì chúng đại diện cho bit input và bit output của LFSR. Ngoài ra $x^n$ cũng sẽ cho ta biết về độ dài của thanh ghi là $n$.

Ví dụ, với một thanh ghi dài $4$ bits với vector hệ số là $(c_3,c_2,c_1,c_0)=(1,1,1,1)$, khi đó ta có đa thức đặc trưng là : $x^4+x^3+x^2+x+1$ với bậc cao nhất là $4$. Tương tự, khi vector hệ số là $(c_3,c_2,c_1,c_0)=(0,0,1,1)$ thì đa thức của nó là $x^4+x+1$

Các hệ số luôn thuộc $[0,1]$, hay nói theo nghĩa khác, các đa thức như này được định nghĩa trên trường hữu hạn $\mathbb{F}_2$

Ta cũng sẽ tìm hiểu thêm về một trong các tính chất đặc biệt của các đa thức dạng như này : 
- **Định nghĩa** : Một đa thức được gọi là **khả quy** nếu như nó có thể phân tích được thành tích của các đa thức có bậc nhỏ hơn.

Ví dụ về một số đa thức khả quy như : 
$$
x^2=x.x
$$

$$
x^2+x=x(x+1)
$$

$$
x^2+1=(x+1).(x+1)
$$

Lưu ý rằng : Ta đang phân tích các đa thức với các hệ số thuộc trường hữu hạn $\mathbb{F}_2$, thế nên các phép toán đa thức với nhau đều sẽ thuộc trong trường hữu hạn này. Ví dụ ta có $1+1=0$ thì $x+x=0$. Như vậy, sở dĩ đa thức $x^2+1=(x+1).(x+1)$ là bởi vì : 
$$
(x+1)(x+1)=x^2+x+x+1=x^2+1
$$

- Trái với các đa thức trên, một đa thức **không thể** phân tích được thành tích các đa thức có bậc bé hơn gọi là **đa thức bất khả quy**.

Ví dụ : 
![{D423E332-7BC3-45AD-AC4C-56A312C71088}](https://hackmd.io/_uploads/B1wCIL34xl.png)


Và từ định nghĩa về các đa thức bất khả quy trên, ta có được một định lý như sau : 
>Nếu đa thức đặc trưng của một LFSR $n$-bits là đa thức khả quy thì chu kì của LFSR đó sẽ không thể đạt được số lượng tối đa, tức không thể bằng $2^n-1$

Ví dụ : Xét một LFSR $3$-bits có vector hệ số là $(c_2,c_1,c_0)=(1,1,1)$. Khi đó đa thức đặc trưng sẽ là : $c(x)=x^3+x^2+x+1$. Đa thức này là một đa thức khả quy khi mà : 
$$
x^3+x^2+x+1=x^2.(x+1)+(x+1)=(x+1)(x^2+1)
$$

Do đó chu kì của LFSR này sẽ không đạt tối đa. Đây là sơ đồ hoạt động của nó với mọi state khởi tạo bất kì : 
![{B2E12E05-D960-43B2-B7EA-24D7F1E476BC}](https://hackmd.io/_uploads/BkrKdLnNgx.png)

Có thể nói, đối với các nhà toán học và các nhà khoa học máy tính, đa thức bất khả quy là rất quan trọng trong việc khai thác và xây dựng nên trường mở rộng, hay cụ thể hơn trong phần này ta sẽ bàn về trường nhị phân mở rộng ($\mathbb{F}_2$ extension field hay $GF(2^k)$). 

Và điều đặc biệt nhất ở đây là : **Đa thức đặc trưng của một LFSR cần ít nhất phải là đa thức bất khả quy thì nó mới đạt được chu kì tối đa.**

Ở đây mình có dùng từ **ít nhất** nhằm ám chỉ việc có những đa thức tuy là bất khả quy nhưng vẫn chưa chắc có thể giúp cho LFSR đạt được chu kì tối đa. Cụ thể xét ví dụ : Cho vector hệ số $(c_3,c_2,c_1,c_0)=(1,1,1,1)$, khi đó ta có đa thức là $x^4+x^3+x^2+x+1$. Đa thức đó tuy là bất khả quy thế nhưng chu kì mà nó đạt được chỉ là $5$ mà thôi (Bạn có thể tự kiểm chứng).

Như vậy, chúng ta cần phải thay đổi lại định nghĩa để sao cho có một đa thức thỏa mãn tính chất nào đó thì nó sẽ cho ta một LFSR với chu kì tối đa ($2^n-1$)

Thật may mắn, chúng ta đã có một định nghĩa mới, hay nó đúng hơn, đó chính là **Golomb’s Second Theorem** : 
> Nếu đa thức đặc trưng bậc $n$ là một đa thức **nguyên thủy** thì khi đó LFSR sẽ có chu kì tối đa.

Vậy đa thức nguyên thủy là gì? Nói một cách dễ hiểu, đa thức bất khả quy $p(x)$ bậc $n$ trên trường hữu hạn $GF(2)$ được gọi là **đa thức nguyên thủy** nếu tồn tại một số nguyên $e$ nhỏ nhất sao cho $x^e-1$ chia hết cho $p(x)$ với $e=2^n-1$.




Ví dụ về một số đa thức nguyên thủy : 
![{5B8D5D69-C3D7-4ECE-AC4E-AEA543CE4F5C}](https://hackmd.io/_uploads/r1si0Pn4ex.png)


Về cơ bản mà nói : 
- LFSR thường được triển khai bằng phần cứng do tính đơn giản và chi phí thấp của nó. Ví dụ, một LFSR $100$-bits chỉ cần vài trăm bóng bán dẫn là đủ.
- Trong các triển khai phần cứng, đa thức đặc trưng được cố định và nhìn chung không thể thay đổi. Vì vậy, ta chỉ có thể coi đa thức đó như một khóa bí mật (đã cố định), cùng với độ dài của LFSR và các hệ số.
- Mặt khác, trong các trường hợp sử dụng phổ biến, LFSR bắt đầu với một trạng thái khởi tạo (initial state) được xác định bởi giá trị seed. Thông thường, trạng thái ban đầu chính là seed.
- Hơn nữa, các bits đầu ra của LFSR thực chất chỉ là các giá trị trạng thái được dịch phải qua từng bước.

Như vậy, ta có thể đặt ra một câu hỏi như sau : Liệu có thể tính được bậc và các hệ số của đa thức đặc trưng của một LFSR, nếu biết một tập hợp các bits output hay không?

Câu trả lời là có, và đó chính là **Thuật toán Berlekamp-Massey** mà ta tìm hiểu ở phần sau.

Dưới đây là bảng của một số đa thức đặc trưng sẽ giúp cho LFSR có độ dài $n$ bits đạt được chu kì tối đa ($2^n-1$) :



![{A80ACC8B-F1DE-49A9-BD41-65806F8894E2}](https://hackmd.io/_uploads/BkmU70KNee.png)





















### Dual_EC_DRBG - Dual Elliptic Curve Deterministic Random Bit Generator
**Dual_EC_DRBG** là viết tắt của **Dual Elliptic Curve Deterministic Random Bit Generator** (Bộ sinh số giả ngẫu nhiên dựa trên đường cong elliptic kép) là một trong bốn thuật toán sinh số ngẫu nhiên xác định (DRBG) được đưa vào **[NIST SP 800-90A](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-90a.pdf)** công bố năm 2006. 

Thuật toán này dựa trên phép toán nhân điểm trên đường cong elliptic (elliptic curve), lợi dụng độ khó của bài toán ECDLP mà đã được quảng cáo là có độ bảo mật tốt. Tuy nhiên, ngay sau khi tiêu chuẩn công bố, đã có nhiều cảnh báo về khả năng tồn tại “cửa sau” (backdoor) và các vấn đề về hiệu năng, độ lệch phân phối kết quả, khiến Dual_EC_DRBG trở thành một trong những ví dụ điển hình về thất bại trong chuẩn hóa mật mã học.

Cụ thể ta có thuật toán như sau : 
- **Dual_EC_DRBG** dạng cơ bản sử dụng đường cong **[P-256](https://neuromancer.sk/std/nist/P-256)** làm tiêu chuẩn sinh số.
- Về cơ bản, thuật toán sinh số của Dual_EC_DRBG giống như trong sơ đồ sinh số tổng quát như ở trên, cụ thể hơn ta có định nghĩa hai hàm $f(x)$ và $g(x)$ như sau : Cho $P,Q$ là hai điểm bất kì thuộc đường cong **P-256**, khi đó ta có : 
$$
\begin{cases}
s_{i}=f(s_{i-1})=s_{i-1}.P\\
r_i=g(s_i)=s_i.Q
\end{cases}
$$
- Lúc này, $s_i$ và $r_i$ sẽ là tọa độ $x$ của phép nhân điểm của một số với điểm $P$ và $Q$.
- Giá trị của $r_i$ sẽ có độ dài là $256$ bits. Ta sẽ loại bỏ đi $16$ bits đầu, chỉ giữ lại $240$ bits cuối. Khi đó ta đã có được số giả ngẫu nhiên rồi.
 
Sơ đồ thuật toán sinh số như sau : 
![{FE818DE1-0583-40E1-8243-8EC6860974F8}](https://hackmd.io/_uploads/Hk1WrzvNee.png)

Tuy hay là thế nhưng như đã nói, đã có nhiều cảnh báo về khả năng tồn tại “cửa sau” (backdoor) và các vấn đề về hiệu năng. Trong đó vấn đề đáng được chú ý nhất là việc chọn $P$ và $Q$. 

Thông thường, $P$ thường được chọn là điểm sinh của **P-256**. Và vì là điểm sinh nên với mỗi $k$ xác định, ta đều có thể tính được $Q=kP$. Nếu như kẻ tấn công biết được $k$ và một output như là $r_1$, thì hắn ta sẽ có thể biết trước được số tiếp theo được sinh ra là gì.

Về bản chất : Ai biết $k$ sẽ nắm quyền kiểm soát bộ sinh, còn người ngoài không biết $k$ thì không phát hiện được gì bất thường. Chính vì vậy, đã có nhiều cáo buộc xoay quanh bộ sinh số giả ngẫu nhiên này. Ví dụ như : 
- NSA bị cáo buộc là đơn vị đứng sau việc cài cắm backdoor khi đề xuất Dual_EC_DRBG vào tiêu chuẩn.
- Năm 2007, Dan Shumow và Niels Ferguson (Microsoft) **[cảnh báo về khả năng có backdoor](https://www.wired.com/2013/09/nsa-backdoor/)** trong thiết kế này tại hội nghị Crypto 2007.
- Năm 2013, sau tiết lộ từ Edward Snowden, tài liệu nội bộ NSA xác nhận rằng họ từng tích cực thúc đẩy Dual_EC_DRBG và giữ quyền kiểm soát thông qua tham số $k$.
- Cuối cùng, năm 2014, NIST khuyến cáo **[ngừng sử dụng Dual_EC_DRBG](https://thehackernews.com/2014/04/nist-removes-dualecdrbg-random-number.html#:~:text=In%20response%20to%20the%20accusations%20on%20NSA%20and,Random%20Bit%20Generators%20%28NIST%20Special%20Publication%20800-90A%2C%20Rev.1%29.)**.

Ngoài phiên bản Dual_EC_DRBG cơ bản trên, ta còn có một số phiên bản khác như : 
- **Dual_EC_DRBG 2006** : 
![{F382A683-AD69-4031-B7B5-C0BB01E30686}](https://hackmd.io/_uploads/r13GxXvVll.png)

- **Dual_EC_DRBG 2007** :
![{139FDEDF-921E-4FFF-8C9F-E0D0E7264FBE}](https://hackmd.io/_uploads/SJrExXPVle.png)
>**adin** là additional input, là một chuỗi ngẫu nhiên do người dùng nhập vào, sau đó sẽ được đem vào hàm băm $H(x)$ để tạo ra các state $s_i$ mới ngẫu nhiên hơn.

Ví dụ về một Dual_EC_DRBG cơ bản : 
```python
from ecdsa.curves import NIST256p
from ecdsa.ellipticcurve import Point
from random import getrandbits

class Dual_EC_DRBG:
    def __init__(self, seed, P, Q):
        self.seed = seed
        self.P = P
        self.Q = Q

    def next(self):
        t = self.seed
        s = (t * self.P).x()
        self.seed = s
        r = (s * self.Q).x()
        r_leak = r & (2**(8 * 30) - 1)
        return r_leak

gen = NIST256p.generator
P = Point(curve=NIST256p.curve, x=gen.x(), y=gen.y())
Q = 19*P
seed = getrandbits(256)

PRNG = Dual_EC_DRBG(seed, P, Q)
print(PRNG.next())
```






# Attack
## Truncated LCGs

Thông thường, các state của LCG có thể bị rò rỉ theo một cách nào đó. Chúng có thể thường bị lộ ra những bits đầu tiên hoặc những bits cuối cùng. Khi đó, các state bị rò rỉ một số bits như vậy gọi là **Truncated LCG states**. 

Đôi khi, các state có thể bị lộ đầy đủ nhưng ta lại không biết các tham số $a,c,m$ của LCG nên sẽ không thể đoán được số tiếp theo hoặc **seed** là gì.

Và khi đó, nếu ta có đủ nhiều các state liên tiếp nhau, hoặc ít nhất là có đủ các state bị truncated của một LCG thì ta hoàn toàn có thể khôi phục lại toàn bộ các tham số cũng như là seed của LCG đó. Dưới đây là một vài công cụ hữu ích để ta làm điều đó.
>Tất cả các công cụ đều được tham khảo từ **[đây](https://github.com/jvdsn/crypto-attacks/tree/master)**.

### Parameter recovery
Ở đây nếu như ta có đủ các state liên tiếp nhau của một LCG thì ta hoàn toàn có thể recover lại $3$ tham số của LCG đó là $a,c,m$, kể cả khi ta không hề biết cả ba tham số đó. 

Code minh họa :
```python
from Crypto.Util.number import GCD
from sage.all import Zmod

def attack(y, m=None, a=None, c=None):
    """
    Recovers the parameters from a linear congruential generator.
    If no modulus is provided, attempts to recover the modulus from the outputs (may require many outputs).
    If no multiplier is provided, attempts to recover the multiplier from the outputs (requires at least 3 outputs).
    If no increment is provided, attempts to recover the increment from the outputs (requires at least 2 outputs).
    :param y: the sequential output values obtained from the LCG
    :param m: the modulus of the LCG (can be None)
    :param a: the multiplier of the LCG (can be None)
    :param c: the increment of the LCG (can be None)
    :return: a tuple containing the modulus, multiplier, and the increment
    """
    if m is None:
        assert len(y) >= 4, "At least 4 outputs are required to recover the modulus"
        for i in range(len(y) - 3):
            d0 = y[i + 1] - y[i]
            d1 = y[i + 2] - y[i + 1]
            d2 = y[i + 3] - y[i + 2]
            g = d2 * d0 - d1 * d1
            m = g if m is None else GCD(g, m)

    gf = Zmod(m)
    
    if a is None:
        assert len(y) >= 3, "At least 3 outputs are required to recover the multiplier"
        x0 = gf(y[0])
        x1 = gf(y[1])
        x2 = gf(y[2])
        a = int((x2 - x1) / (x1 - x0))

    if c is None:
        assert len(y) >= 2, "At least 2 outputs are required to recover the multiplier"
        x0 = gf(y[0])
        x1 = gf(y[1])
        c = int(x1 - a * x0)

    return m, a, c



# Ví dụ : 
# a = 21130680057583
# b = 157472211850417
# m = 267589112958697
# seed = 114441602941445

list_state = [66320052326885, 196648052286517, 143226036948570, 192329747199943, 79611648247501, 50511844748207, 54162275291895, 42701274401171]
list_truncated = [60, 178, 130, 174, 72, 45, 49, 38]

ans = attack(list_state, m=None, a=None, c=None)
print(ans)
# (267589112958697, 21130680057583, 157472211850417)
```

Khi số lượng các state là $5$ thì xác suất recovery thành công là $60\text{%}$, nếu số lượng là $6$ thì sẽ là $80\text{%}$. Và lưu ý là chúng phải liên tiếp nhau và không được tách rời.


### Truncated state recovery
Như đã nói, các state của LCG có thể bị rò rỉ theo một cách nào đó. Thông thường chúng hay bị rò rỉ ở những bits đầu (Most Significant Bits - MSB). Khi đó, khi có đủ các state cần thiết, ta hoàn toàn có thể recover lại các state đó bằng Lattice Reduction như sau : 
```python
from sage.all import QQ, ZZ, matrix, vector

def attack(y, k, s, m, a, c):
    """
    Recovers the states associated with the outputs from a truncated linear congruential generator.
    More information: Frieze, A. et al., "Reconstructing Truncated Integer Variables Satisfying Linear Congruences"
    :param y: the sequential output values obtained from the truncated LCG (the states truncated to s most significant bits)
    :param k: the bit length of the states
    :param s: the bit length of the outputs
    :param m: the modulus of the LCG
    :param a: the multiplier of the LCG
    :param c: the increment of the LCG
    :return: a list containing the states associated with the provided outputs
    """
    diff_bit_length = k - s

    # Preparing for the lattice reduction.
    delta = c % m
    y = vector(ZZ, y)
    for i in range(len(y)):
        # Shift output value to the MSBs and remove the increment.
        y[i] = (y[i] << diff_bit_length) - delta
        delta = (a * delta + c) % m

    # This lattice only works for increment = 0.
    B = matrix(ZZ, len(y), len(y))
    B[0, 0] = m
    for i in range(1, len(y)):
        B[i, 0] = a ** i
        B[i, i] = -1

    B = B.LLL()

    # Finding the target value to solve the equation for the states.
    b = B * y
    for i in range(len(b)):
        b[i] = round(QQ(b[i]) / m) * m - b[i]

    # Recovering the states
    delta = c % m
    x = list(B.solve_right(b))
    for i, state in enumerate(x):
        # Adding the MSBs and the increment back again.
        x[i] = int(y[i] + state + delta)
        delta = (a * delta + c) % m

    return x



# Ví dụ : 
a = 21130680057583
b = 0
m = 2 ** 48
origin_len_bit = 48
truncated_len_bit = 8

# seed = 114441602941445

list_state = [65390861615077, 5388025519307, 75690594782085, 97324705036075, 4463254563621, 255400775449995, 2132311465669, 227920676990955]
list_truncated = [59, 4, 68, 88, 4, 232, 1, 207]

ans = attack(list_truncated, origin_len_bin, truncated_len_bit, m, a, b)
print(ans==list_state)
```

Để có thể recover lại các state một cách chính xác thì cần có ít nhất $8$ output Truncated state liên tiếp nhau là được.




## LFSR - Recover state bằng Berlekamp-Massey
**[Thuật toán Berlekamp-Massey](https://en.wikipedia.org/wiki/Berlekamp%E2%80%93Massey_algorithm)** là thuật toán được phát triển bởi hai nhà toán học người Mỹ là **Elwyn Berlekamp** và **James Massey**. Đây là một thuật toán tìm đa thức đặc trưng ngắn nhất sinh ra một dãy nhị phân cho trước. Thuật toán cũng tìm ra đa thức nhỏ nhất của một quan hệ truy toán tuyến tính trên một trường bất kì.

Dưới đây là code của thuật toán (do mình lụm được) : 
```python
def berlekamp_massey(s):
    n = len(s)
    c = [0] * n
    b = [0] * n
    c[0], b[0] = 1, 1
    l, m = 0, -1
    for i in range(n):
        d = s[i]
        for j in range(1, l+1):
            d ^= c[j] & s[i - j]
        if d:
            t = c.copy()
            for j in range(i - m, n):
                c[j] ^= b[j - (i - m)]
            if 2 * l <= i:
                l = i + 1 - l
                b = t
                m = i
    return c[:l+1], l  # trả về đa thức và độ phức tạp tuyến tính

def coef_to_polynomial(coef):
    deg = len(coef) - 1 
    terms = []
    for i, c in enumerate(coef):
        if c == 1:
            power = deg - i
            if power > 1:
                terms.append(f"x^{power}")
            elif power == 1:
                terms.append("x")
            else:
                terms.append("1")
    return " + ".join(terms)

poly, lc = berlekamp_massey(y)



"""
Ví dụ : 
Cho một Output sinh ra từ LFSR 10-bits là : 
output = [1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 0, 1, 0]

Ở đây ta sẽ không hề biết được các taps và seed ban đầu là gì
Bằng cách sử dụng Thuật toán Berlekamp-Massey sẽ giúp cho ta biết được đa thức đặc trưng của nó là gì
"""

poly, lc = berlekamp_massey(output)
print(f"Linear Complexity: {lc}")
print(f"Đa thức đặc trưng là : {coef_to_polynomial(poly)}")
# Linear Complexity: 10
# Đa thức đặc trưng là : x^10 + x^9 + x^8 + x^5 + x -> taps là [1,5,8,9].
# Bạn cũng có thể tự kiểm chứng với seed = [1,1,1,0,1,0,0,0,1,0] 
# và LFSR này dịch sang trái 
```






