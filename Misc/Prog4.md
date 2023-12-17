**Chall**
- ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/a7d4a7a1-02fc-4425-b5bf-c2a7ba35f547)
-------
**Solve**
- Tính số theo quy tắc chẵn lẻ:
- Xét f(n):
  - f(0)= 0.
  - f(1)= 1,
  - f(n)= n+ f(n-1) với n lẻ.
  - f(n)= n* f(n-1) với n chẵn.
```Python:
from pwn import *
import json

def exploit():
    try:
        f = remote("103.162.14.116", 14005)
        f.recv()  # Receive the initial message
        for i in range(100):
            f.recvuntil("n = ")
            recv = json.loads(f.recvline().decode().strip("\n"))
            n = recv
            a_n = 1
            for j in range(1, n + 1):
                a_n = a_n * j if j % 2 == 0 else a_n + j
            f.sendlineafter("= ", str(a_n).encode())
            print(f"Attempt {i + 1}: Sent result {a_n}")
        last_line = f.recvline().decode().strip()
        print(f"Last line from the server: {last_line}")
    except (EOFError, KeyboardInterrupt):
        pass
    except Exception as e:
        print(f"Error: {type(e).__name__}: {e}")
    finally:
        # Close the connection
        f.close()
if __name__ == "__main__":
    exploit()
