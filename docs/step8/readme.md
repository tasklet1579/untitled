### ๐ฏ ํ์ต ๋ชฉํ

![image](../image/step8/image01.png)

- HTTP ๊ฐ์ ์ ๋ฐ๋ฅธ ์ฐจ์ด๋ฅผ ์ดํดํ๊ณ  Reverse Proxy ์ฑ๋ฅ ๊ฐ์ ์ ํด๋ด๋๋ค.
- HTTP Cache ์ ๋ต์ ์ดํดํ์ฌ ์ ์ ํ ์ ์ฑ์ ์ค์ ํด๋ด๋๋ค.
- ์ฟผ๋ฆฌ๋ฅผ ์ต์ ํํ์ฌ ์กฐํ ์ฑ๋ฅ์ ๊ฐ์ ํด๋ด๋๋ค.
- ์ธ๋ฑ์ค๋ฅผ ์ค์ ํ์ฌ ์กฐํ ์ฑ๋ฅ์ ๊ฐ์ ํด๋ด๋๋ค.

---

### 1. ํ๋ฉด ์๋ต ๊ฐ์ ํ๊ธฐ

โ๏ธ ์๊ตฌ์ฌํญ
- ๋ถํํ์คํธ ๊ฐ ์๋๋ฆฌ์ค์ ์์ฒญ์๊ฐ์ ๋ชฉํฏ๊ฐ ์ดํ๋ก ๊ฐ์ 
  - ๊ฐ์  ์  / ํ๋ฅผ ์ง์  ๊ณ์ธกํ์ฌ ํ์ธ

[๊ฐ์ 1](nginx.conf)
- gzip
- cache
- TLS, HTTP/2

[๊ฐ์ 2](redis.md)
- Redis
---

### 2. ์ค์ผ์ผ ์์

โ๏ธ ์๊ตฌ์ฌํญ
- springboot์ HTTP Cache, gzip ์ค์ ํ๊ธฐ
- Launch Template ์์ฑํ๊ธฐ
- Auto Scaling Group ์์ฑํ๊ธฐ
- Smoke, Load, Stress ํ์คํธ ํ ๊ฒฐ๊ณผ๋ฅผ ๊ธฐ๋ก

[๋ต๋ณ](scale.sh)
- jdk ์ค์น
- ๋ฐฉํ๋ฒฝ ์ค์ 
- nginx ์คํ
- ์ ํ๋ฆฌ์ผ์ด์ ๋ฐฐํฌ

---

### 3. ์ฟผ๋ฆฌ ์ต์ ํ

๐ฟ SQL
- [์ค์ต ์ฌ์ดํธ](https://www.w3schools.com/sql/trymysql.asp?filename=trysql_func_mysql_concat) ์์ ์๋ ์ฟผ๋ฆฌ๋ฅผ ์์ฑํด๋ณด์ธ์.
  - 200๊ฐ ์ด์ ํ๋ฆฐ ์ํ๋ช๊ณผ ๊ทธ ์๋์ ์๋ ๊ธฐ์ค ๋ด๋ฆผ์ฐจ์์ผ๋ก ๋ณด์ฌ์ฃผ์ธ์.
  - ๋ง์ด ์ฃผ๋ฌธํ ์์ผ๋ก ๊ณ ๊ฐ ๋ฆฌ์คํธ(ID, ๊ณ ๊ฐ๋ช)๋ฅผ ๊ตฌํด์ฃผ์ธ์.
  - ๋ง์ ๋์ ์ง์ถํ ์์ผ๋ก ๊ณ ๊ฐ ๋ฆฌ์คํธ๋ฅผ ๊ตฌํด์ฃผ์ธ์.

[๋ต๋ณ](sql-1.md)

โ๏ธ ์๊ตฌ์ฌํญ
- ํ๋์ค์ธ(Active) ๋ถ์์ ํ์ฌ ๋ถ์๊ด๋ฆฌ์(manager) ์ค ์ฐ๋ด ์์ 5์์์ ๋๋ ์ฌ๋๋ค์ด ์ต๊ทผ์ ๊ฐ ์ง์ญ๋ณ๋ก ์ธ์  ํด์ค(O)ํ๋์ง ์กฐํํด๋ณด์ธ์.
- ์ธ๋ฑ์ค ์ค์ ์ ์ถ๊ฐํ์ง ์๊ณ  1s ์ดํ๋ก ๋ฐํํฉ๋๋ค. 

[๋ต๋ณ](sql-2.md)

---

### 4. ์ธ๋ฑ์ค ์ค๊ณ

โ๏ธ ์๊ตฌ์ฌํญ
- ์ฃผ์ด์ง ๋ฐ์ดํฐ์์ ํ์ฉํ์ฌ ์๋ ์กฐํ ๊ฒฐ๊ณผ๋ฅผ 100ms ์ดํ๋ก ๋ฐํ 
  - [Coding as a Hobby](https://insights.stackoverflow.com/survey/2018#developer-profile-_-coding-as-a-hobby) ์ ๊ฐ์ ๊ฒฐ๊ณผ๋ฅผ ๋ฐํํ์ธ์.
  - ํ๋ก๊ทธ๋๋จธ๋ณ๋ก ํด๋นํ๋ ๋ณ์ ์ด๋ฆ์ ๋ฐํํ์ธ์. 
  - ํ๋ก๊ทธ๋๋ฐ์ด ์ทจ๋ฏธ์ธ ํ์ ํน์ ์ฃผ๋์ด(0-2๋)๋ค์ด ๋ค๋ ๋ณ์ ์ด๋ฆ์ ๋ฐํํ๊ณ  user.id ๊ธฐ์ค์ผ๋ก ์ ๋ ฌํ์ธ์.
  - ์์ธ๋๋ณ์์ ๋ค๋ 20๋ India ํ์๋ค์ ๋ณ์์ ๋จธ๋ฌธ ๊ธฐ๊ฐ๋ณ๋ก ์ง๊ณํ์ธ์. 
  - ์์ธ๋๋ณ์์ ๋ค๋ 30๋ ํ์๋ค์ ์ด๋ ํ์๋ณ๋ก ์ง๊ณํ์ธ์. 

[๋ต๋ณ](sql-3.md)
