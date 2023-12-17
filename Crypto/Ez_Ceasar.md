**Chall**
```Python
import string
import random

alphabet = string.ascii_letters + string.digits + "!{_}?"

flag = 'KCSC{s0m3_r3ad4ble_5tr1ng_like_7his}'
assert all(i in alphabet for i in flag)

key = random.randint(0, 2**256)

ct = ""
for i in flag:
    ct += (alphabet[(alphabet.index(i) + key) % len(alphabet)])

print(f"{ct=}")

# ct='ldtdMdEQ8F7NC8Nd1F88CSF1NF3TNdBB1O'
```

```Python
import string
import time

alphabet = string.ascii_letters + string.digits + "!{_}?"

def brute_force(ciphertext):
    for key in range(2**256):
        decrypted = ""
        for i in ciphertext:
            decrypted += alphabet[(alphabet.index(i) + key) % len(alphabet)]
        if is_flag(decrypted):
            return decrypted
    return None

def is_flag(string):
    if "KCSC{" not in string:
        return False
    return True

if __name__ == "__main__":
    ciphertext = "ldtdMdEQ8F7NC8Nd1F88CSF1NF3TNdBB1O"
    print("Decrypting ciphertext...")
    start_time = time.time()
    decrypted = brute_force(ciphertext)
    end_time = time.time()
    print("Decrypted message:", decrypted)
    print("Time taken:", end_time - start_time)
```