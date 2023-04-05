# SQL Oracle vs SQLİTE

hocam gördüğün gibi select kısmık aynı ancak değişkenler arasına , değil || konulur.
DEğikenler arasına bir şeyler yazmak için daha doğrusu değerler arasına bir şeyler yazdırmak için ' ' tırnak kullnaılır. 
Eğer tablonun ismini değiştirmek istersende AS kullanılır başlığıda "" tırnak içinde yazarsın. sqlite daki gibi tek tek değişken 
isimlendirmek yok. SAdece tablonun ismini belirleyebilirsin. DISTINCT ile büyükten küçüğe sıralama elde ederiz
```sql
            SELECT Department_id || Department_name FROM Departments;
            
            SELECT Department_id || ' - ' || Department_name FROM Departments;
            
            SELECT Department_id || ' - ' || Department_name AS "title" FROM Departments;
            
            SELECT first_name || ' ' || last_name || ' s salary for a year is  ' || salary*12 AS "pay" FROM Employees;
            
            SELECT DISTINCT department_id FROM departments;
```
virgül kullanırsan tabloda ayru row olarak alır. isim kısaltma ve where ilemide sqlite ile aynı
kullanilan operatorler <, <=, >, >=, <> sonuncu eşit değil demek. ooo sqlite'ı solluyorr ayrıca != ve ^= eşit değil demek  
yine WHERE ile string sorgulamam yapılabilir

```sql
            SELECT department_id , department_name FROM Departments; 
            
            SELECT first_name name, last_name, employee_id id FROM employees WHERE employee_id<102;
            
            SELECT first_name name, last_name, employee_id id FROM employees WHERE employee_id<>102;
            
            SELECT first_name name, last_name, employee_id id FROM employees WHERE last_name='Abel';

```

BETWEEN kullanımıda aynn mevcut. Ancak hocam burada kkolayıda var. direk şu ve şu aralıkta diyebilirliz. yani between kullanmasakta olur
string ifadeler de aralık içinde in kullanılır. yine tek tırnak iki tırnak sadece isimlendirirken kullanırız, IN yerine OR da kullanılabilir 
tabiki.
LIKE '%a%'  '%_a%'  '%a_%'  '%%a%'  
IS NULL ve IS NOT NULL var WHERE ile kullanılırlar 

```sql
            SELECT first_name name, salary FROM employees WHERE salary BETWEEN 5000 AND 12000;
            
            SELECT first_name name, salary FROM employees WHERE salary>=5000 AND salary<=12000;
            
            SELECT country_id FROM locations WHERE country_id IN ('CA','UK'); 
            
            SELECT first_name, job_id FROM employees WHERE job_id LIKE '%T_%'  ; 
            
            SELECT first_name, manager_id FROM employees WHERE manager_id IS NOT NULL  ; 

```

OREDER BY aynn kullanılır. Büyükten küçüğe sıralamk içinde DESC kullanılır.
ayricad eğişkne isimlendirince kodun devamınd abunu kullananmıyorduk sadece tablo isimlerinde yapabiliyprduk ya işte değişkenin adınında 
tablo adı gibi AS ve "" tırnka ile değiştirirsek kulllanabiliriz
Kanka bak ne buldum kullanmadığın değişkene göre de sıralayabiliyorsun
Üçüncü satıra bakalım. Birden fazla özellik ile sıralayabiliriz. burada aynı departmant_id e sahip çalışanlar var. sırayla önce 
department_id ile sıralar daha sonra bu değerleri aynı olanları kendi arasında first name'e göre sıralar
```sql
            SELECT first_name, hire_date FROM employees ORDER BY hire_date DESC;
            
            SELECT first_name, hire_date  AS "date" FROM employees ORDER BY "date" DESC;
            
            SELECT department_id, first_name  FROM employees ORDER BY department_id, first_name;
```

Gelelim dual muhabbetine. hesaplama yapmanı aslında olmyan data base den sanki değer çekiyormuşsun gibi yapmanı sağlar
UPPER/LOWER/INITCAP 
hocam ınıntcap verilen stringin ilk harfini upper yapar
CONCAT
SUBSTR(strİng_name, string_position, string_length) the string length is optianal. Hocam index saymaya 0 dan değil 1 den başlanıyor
LENGTH
RPAD/LPAD(string_name, wish_length, added_str) istenilen uzunluğa gelene kadar belirtilen karakteri ekler. rpad sağa lpad sola ekler
TRIM(cutting_type, 'char' FROM 'string')
REPLACE(string, removed_str, added_str) eklenecek string kısmı optional
row 13 ortaya karışık ornek 
=: giriş yapmayı sağlayan kod. bu arkaadaş oracle app e özel anladığım kadarıyla

```sql
            
            SELECT (35/7)+23 FROM dual;
            
            SELECT last_name FROM employees WHERE UPPER(last_name)='ABEL';
            
            SELECT LOWER(last_name) FROM employees;
            
            SELECT last_name FROM employees WHERE INITCAP(last_name)='Abel';
            
            SELECT CONCAT('DEÜ','_CMPE') AS "DREAM" FROM dual;

            SELECT SUBSTR('DEÜ_cmpe_new',5,4) AS "Table" FROM dual;

            SELECT LENGTH('DEÜ_cmpe_new') AS "Table" FROM dual;

            SELECT LENGTH(first_name) AS "Table" FROM employees;

            SELECT RPAD(first_name,10,'-') AS "Table" FROM employees;

            SELECT  TRIM(BOTH 'A' FROM 'ANKARA') AS "Table" FROM dual;

            SELECT  REPLACE('JACK AND JUE', 'J', 'BL') AS "Table" FROM dual;

            SELECT  REPLACE('FUCKING POLİTİCS', 'K', '*') AS "Table" FROM dual;

            SELECT LOWER(first_name) || '_' || UPPER(SUBSTR(last_name,1,1)) AS "user name" FROM employees;

            SELECT LOWER(first_name) || '_' || UPPER(SUBSTR(last_name,1,1)) AS "user name" FROM employees WHERE department_id=:enter_dep_id;

            SELECT department_id FROM employees WHERE department_id=:enter_dep_id;
```

Geldik numeric fonksiyonlara. Açıkçası zor heşdi hemen ROUND ile başlayalım rand değil round yani bildiğin yuvarlama burada sayıyı yazarsın birde hangi rakamı yuc-varlayacağını belirtirsin. 0.index 23.a34 a dediğimiz yer sırasıyla sağa doğru index artiyor sola soğru azalıypr yani dc.ba a=1, b=0, c=-1, d=-2 indexte hadi kolay gelsin :)) 
TRUNC seçim kısmı şndexkeme round ile aynı. trunc seçilen rakamı aşşağıya yuvarlar.
MOD bilfdiği mod işlemi 
```sql
            SELECT ROUND(62.34, -2) FROM DUAL;
            
            SELECT MOD(62, 5) FROM DUAL;
```
SYSDATE sistam zamanı yanı a+x dersek x gün ekler tariha
moths_between ikil tarih arasındaki ay sayısını dödürür hakikaten ilginç
add_months ilk tarihe ikinci arguman kaadar ay ekler
next_day arguman tarih olur bu tarih ten sonraki ikinci argumandaki lk gunu dondurur
last_day tek arguman alır. ayın son tarihini dondurur
row 6 ayı yuvarladık :) month dediğmizde ayın günleri oluyor. ayı başa yada yeni aya yuvarlıyor. yıl bazında yuvarlama yapıyorsada ya yeni 
yıla geçer yada yılın başına çeker
Trunc ile yaparsan da biliyorsun herzaman geriye yuvarlar
```sql
            SELECT SYSDATE+30 FROM dual;
            
            SELECT hire_date FROM employees WHERE MONTHS_BETWEEN ('17-Jun-1999', hire_date)<0 ORDER BY hire_date;
            
            SELECT  ADD_MONTHS(SYSDATE,12) AS "New Year" FROM dual;
            
            SELECT NEXT_DAY(SYSDATE,'Monday') AS "New Week" FROM dual;
            
            SELECT LAST_DAY(SYSDATE) AS "End Of The Month" FROM dual;
            
            SELECT hire_date, ROUND(hire_date,'MONTH') AS "interesting" FROM employees;
```
Tarih yazdırma char'a çevirme 
TO_CHAR(date,type) deriz. yazdırma type: 
DAY monday
Mon jun
Month june
YYYY 1994
YAER nineteen Ninety-four
sp yazıyla yazdırmak için
ddth 17th gibi yazdırmak için
HH:MI:SS AM 10:45:34 amsaat dakika saniye
TO_CHAR(sayı,format) 
TO_NUMBER(string_number, format) hocam burada format birebşr sayının kedi basanağı gibi olmaşı. to_char'da istesek virgülden sonraki kısmı 
değiştirebiliyorduk burada ise yapamayız. to_number'da format seçmiyor belirtiyoruz
TO_DATE(string_date, format)
```sql
    
            SELECT TO_CHAR(hire_date,'Day MON YYYY') FROM employees;

            SELECT TO_CHAR(SYSDATE,'HH:MI:SS AM') FROM dual;

            SELECT TO_CHAR(12345.789,'$99999.99') FROM dual;

            SELECT TO_NUMBER('55.1234','99.9999') FROM dual;

            SELECT first_name, TO_NUMBER(bonus,'9999') AS "bonus table"  FROM employees;

            SELECT TO_DATE('17 APRİL, 2020','dd MONTH, yyyy') FROM dual;


```

NULL ile mücadele. ilk olarak. NVL(değiken adı, nul bulduğumuzda yerine koyacaımız şey) hocam burada değişken adıyla yerine yazacağımız 
şetyin tipinin aynı olması onemli. haliyel :)): mesela NVL(int_degisken, char_type) yaparsak hata aşırız
NVL2(değişken adı, eğer null değilse dönecek değer, eğer null ise dönecek değer)
bu mücadeel değil. NULLIF() ikin argüman alır eğer eşitlerse  null döndürür değillerse ilk argumanı döndürür
COALESCE(par1,par2....parn) verilen paremetreleri tek tek gezer null olmayan ilk ifadeyi döndürür
```sql
            SELECT last_name, NVL(commission_pct,0) from employees;

            SELECT last_name, NVL2(commission_pct,commission_pct*10+salary,salary) from employees;

            SELECT last_name, first_name, NULLIF(LENGTH(last_name), LENGTH(first_name)) from employees;

            SELECT first_name, COALESCE(commission_pct, salary, 0) from employees;

```

şart condition. CAse ile yapılır. case sorgulanacak ifade when ihtimal than return .... end en son enfd yazömayo unuytmayalım
Birde DECODE diye bir şey var hocam bu aradaki when than ifadeelrini koymana gerek yok end de koymuyorun değişkenler returnler falan sırayla 
yazılıyor o kdr

```sql
            SELECT first_name, department_id, 
            CASE department_id WHEN 90 THEN 'Management' 
            WHEN 80 THEN 'Sales' 
            WHEN 60 THEN 'IT' 
            ELSE 'Other dep.' 
            END 
            AS "Department" FROM employees;


            SELECT first_name, department_id, DECODE(department_id,
            90, 'management',
            80,'sales',
            60,'IT',
            'other departments') 
            AS "Departments" from employees;
            
```