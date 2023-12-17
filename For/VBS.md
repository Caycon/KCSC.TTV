**Chall**
- Là 1 file zip bị mã hóa chứa file .vbs.
- ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/849bcd6a-64d9-4324-8214-65aef2b6a60c)
-------
**Solve**
- Ta sẽ crack pass bằng `johntheripper`
- Thu được pass là `kma9239`
- Ta `cat code.vbs`:
- ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/0826e7e0-72dd-4e60-bec8-6066f02e2f7a)
- Truy cập vào từng link, trong đó có [link](https://pastebin.pl/view/a60d3da5): `https://pastebin.pl/view/a60d3da5`.
- ![image](https://github.com/Caycon/KCSC.TTV/assets/97203151/62aa7b7b-a030-4757-b55d-ffcffe71758d)
- Ta thu được 1 đoạn base64: `S0NTQ3tWYjRfaDAxX2xvciIiX2FlX3RoMG5nX2M0bV89KCgofQ==` 
- Decode ta thu được flag.
