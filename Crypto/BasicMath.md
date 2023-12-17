**Chall**
```Python
from Crypto.Util.number import getPrime

flag = b'KCSC{fake_flag}'

def verify(g, p, y, x, k, h):
    return (y*x*pow(g, k, p)) % p == pow(g, h, p)

p = getPrime(256)
g = getPrime(128)
y = 65537

lst_x = []
lst_h = []

print(f"p = {p}")
print(f"g = {g}")
print(f"y = {y}")

try:
    for i in range(20):
        x = 0
        h = 0
        x = int(input("x = "))
        h = int(input("h = "))
        if x in lst_x or h in lst_h:
            print('get out !!!')
            exit(-1)
        rs = verify(g, p, y, x, i, h)
        if rs:
            lst_x.append(x)
            lst_h.append(h)
        else:
            print('get out !!!')
            exit(-1)
            
    flag = open('flag.txt', 'rb').read()
    print(flag)
except:
    print("something went wrong")

```
- Đọc code `chall.py` ta thấy được h= k là phương án tối ưu nhất, mà k= i nên sau mỗi vòng lặp h= i. Đồng thời thấy được x*y= 1 mod(p). `Lưu ý rằng hàm pow(g, k, p)= g**k mod(p)`.
- Nên giờ ta cần tìm x để thỏa mãn x*y= 1 mod(p) hay đó chính là tính modul nghịch đảo.
- P/s: do làm ra r nên mình cx lười dùng pwn:)))
```Python
def extended_gcd(a, b):
    if a == 0:
        return b, 0, 1
    else:
        g, x, y = extended_gcd(b % a, a)
        return g, y - (b // a) * x, x

def modinv(a, m):
    g, x, y = extended_gcd(a, m)
    if g != 1:
        raise Exception('Modular inverse does not exist')
    else:
        return x % m

p = 76700494270582878664201772158933427825564440858388192645693976651835849252291  # Thay đổi p nha mng.
y = 65537

try:
    x = modinv(y, p)
    print(f"The value of x is: {x}")
except Exception as e:
    print(f"Error: {e}")
for i in range(20):
    print(i)
    print(x*((p+1)**i))
    print()

```
