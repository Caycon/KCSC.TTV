**Chall**
```Python
from Crypto.Cipher import AES
from Crypto.Util import Counter
from Crypto import Random

flag = b'KCSC{s0m3_r3ad4ble_5tr1ng_like_7his}'
nonce = Random.get_random_bytes(8)
countf = Counter.new(64, nonce)
key = Random.get_random_bytes(32)

encrypto = AES.new(key, AES.MODE_CTR, counter=countf)
encrypted = encrypto.encrypt(b"TODO:\n - ADD HARDER CHALLENGE IN CRYPTO\n - ADD FLAG TO THE CHALLENGE\n")

encrypto = AES.new(key, AES.MODE_CTR, counter=countf)
encrypted2 = encrypto.encrypt(flag)

print(f"encrypted: {encrypted.hex()}")
print(f"encrypted2: {encrypted2.hex()}")

# encrypted: 5e07dfa19e2b256c205df16b349c0863a15839d056ada1fb425449f2f9af9563eccca6d15cb01aabbe338c851f7b163982127033787fff49e74e3e09f0aee048a1d5b29f5a
# encrypted2: 410bc8addf6036125f5fe17d4bb61c00ba565a9e71d1bf846f625eeac5bfa972f9e7c4fd60800ac9aa689f9b280f5a09fd3768674401ac60
```
-------

**Solve**
- Ta biết được 2 plaintext trên được mã hóa từ cùng 1 key và 1 kiểu mã hóa là AES mode CTR, từ đó dựa vào ciphertext ta có được key bằng cách xor plaintext với ciphertext đã biết.
- Sau khi có được key ta tiến hành xor ciphertext với key tìm được để có flag.
```Python
from Crypto.Cipher import AES
from Crypto.Util import Counter
from Crypto import Random
from pwn import *
def hex_to_bytes(hex_string):
    return bytes.fromhex(hex_string)

def encrypt_decrypt_aes_ctr(key, nonce, plaintext):
    cipher = AES.new(key, AES.MODE_CTR, counter=Counter.new(128, initial_value=int(nonce, 16)))
    return cipher.encrypt(plaintext)

encrypted = "5e07dfa19e2b256c205df16b349c0863a15839d056ada1fb425449f2f9af9563eccca6d15cb01aabbe338c851f7b163982127033787fff49e74e3e09f0aee048a1d5b29f5a"
encrypted = hex_to_bytes(encrypted)
plaintext = b"TODO:\n - ADD HARDER CHALLENGE IN CRYPTO\n - ADD FLAG TO THE CHALLENGE\n"
key1 = xor(encrypted, plaintext)
encrypted2 = "410bc8addf6036125f5fe17d4bb61c00ba565a9e71d1bf846f625eeac5bfa972f9e7c4fd60800ac9aa689f9b280f5a09fd3768674401ac60"
encrypted2 = hex_to_bytes(encrypted2)
flag = xor(encrypted2, key1)
print(flag)

```