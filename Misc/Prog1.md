**Chall**
- Tim max:
- ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/382223e7-77ce-4c74-b6be-8d43397f4563)

-------
**Solve**
```Python
from pwn import *
import json

def exploit():
    try:
        f = remote("103.162.14.116", 14002)
        for i in range(100):
            try:
                f.recvuntil(b'arr = ', timeout=5)
                a = json.loads(f.readline().decode())
                max_value = max(a)
                f.sendlineafter("max = ", str(max_value).encode())
                print(f"Attempt {i + 1}: Sent max value {max_value}")
            except (EOFError, KeyboardInterrupt):
                break
            except Exception as e:
                print(f"Error during attempt {i + 1}: {type(e).__name__}: {e}")
        f.close()
    except Exception as e:
        print(f"Connection error: {type(e).__name__}: {e}")

if __name__ == "__main__":
    exploit()
```
- Flag: ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/342b7166-6dfe-40ee-a62f-7d5a9186629e)
