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
## Join

## Natural Join
kendisi orta isimli column ile birleştirir. Evet yani ortak column olamlı ve bunların veri tiplaride aynı olmallı.

```sql
            Select first_name, job_id from employees NATURAL JOİN jobs;
```

## Cross Join 
birleştirdiğinde tüm olası kombinasyonları yapar. 
8 row table CROSS JOIN 20 row table; = 160 row table olur :))

birde JOIN ile birlikte kullanılan kelimeler var. onların da özellikleirne bakalım

## Join Using 
hocam bu using varya kral bir şey. Şimdi natural joinde aynı isimde fakat farklı veri tipli column birleştirilirken hata veriliyor. ytani bu adamlar aynı isimde fakat farklı veri tipinde işte tam bu nokta da using işimize yarıyor. using ile kullanammız gereken calomns belirtiyoruz. :))

```sql
            SELECT first_name, employee_id, department_id, department from employees JOIN departments USING (department_id) WHERE last_name = 'Higgins';
```

## Join On
ya isimler bile farklıyse. Hop ON clause yanımızda. bu arada where ile de kullanılabilir.

```sql
            SELECT last_name, job_title from employees e JOIN jobs j ON (e.job_id = j.job_id);
```
hocam gördüğün gibi isimler aynı olmasa dahi bu eşitlemeyi yapman gerekir. çünkü öyle tipi böyle istiyo :))

where ile de kullanalım
```sql
            SELECT last_name, job_title from eployees e JOIN jobs j ON (e.job_id = j.job_id) WHERE last_name LIKE 'H%';
```


```sql
            SELECT last_name, salary, grade_level, lowest_salary, highest_salary from employees JOIN job_grades ON (salary BETWEEN lowest_salary AND highest_salary);
```

NOT: istersen birden fazla using kullanarak yada using v eon kullanarak üç ve daha fazla tabloyu birleştirebilirsin.

```sql
            SELECT last_name, department_name AS "Department", city from employees JOIN departments USING (department_id) JOIN location USING (location_id);
```
## left- right full outer join

```sql
            SELECT e.last_name, d.department_id, d.department_name from employees e LEFT OUTER JOIN departments d ON (e.department_id = d.department_id);
```


## mini özet:
sadece **join** olduğunda tabloyu farklı isimlerle tekrar oluşturursun. **inner join** de istedğin columler ın sadece ortak satırlarını görürsün. 
**left-right join** de ortak satılar ve endexli olunan tablonun tüm satırları alınır join yapıldığında karşı tabloda karşılığı olmamasına 
rağmen bu satırlar yazaılır. **full join** ise tüm hepsini alır. ortaklığa dahil olsun olmasın her iki tablonunda tüm satırları yazılır. 
hatta dublicate sorunu yaşanmadan :))
**cross join** de ise olası tüm kombinasyonlar yazılır. 

## relationship with itself

ERD de biliyorsun kendisiyle bağlantı kuran oluyor. for example an employee can be a manager as well. that's the example code
```sql
            SELECT worker.last_name || 'works for' || manager.last_name AS "works for" from employees woker JOIN employees manager ON (worker.manager_id = manager.employee_id);
```
## Hierarchial query

hocam tabloda dikine bağlantılar kurmanı sağlar. mesala tabloda senin patronnun hemen bir üstünde yazılı oluyorsa.
```sql
            SELECT employee_id, last_name, job_id, manager_id from employees START WITH employee_id = 100
            CONNECT BY PRIOR employee_id = manager_id;
```
hatta soy isme bağlı bir yazı da yazdırabiliirz. bu hierarchial sorgunun kendine özel keyword leri var. 
select LEVEL dediğinde sıralamış oluyor daha doğrusu sırasını başına yazmış oluyor. bu biizm tablolarımızda olması gereken birattribute değil. 
hierarchial sorgunun kendi özelliği :))
prior önceki hangi değişkenle bağlantı kuracak bunu belirtiyor.
start wirth adı üstünde ne ile başlayacağını hangı row dan başlayacağını belirtir.
connect by prior hangi iki değişknei bir öncekiyle bağlaycak. mesala burda kendi, manager_id si bir öncekinin employee_id si oöur. 
yanş yukarıdaji employee_id bu saturdaki manger_id olur. 

```sql
            SELECT LEVEL, last_name || ' reporst to ' || 
            PRIOR last_name
            AS "Walk Top Down" from employees 
            START WITH last_name = 'King'
            CONNECT BY PRIOR employee_id = manager_id;
```

output:
1 Kings reports to 
2 Kochar reports to King
3 Whalen report to Kochar

sırayı tersten yazdırmak içinse prior yazdığımız yeri değiştiririz
```sql
            SELECT LPAD(last_name LENGTH(last_name)+(level*2)-2,'_'), AS org_chart
            from employees
            START WITH last_name = 'Grant'
            CONNECT BY employee_id = PRIOR manager_id;
```
anladın mı hocam connect  by prior yazmak yerine ikinci değişkenin başına yazdık böyle olunca tersten sıralıyor.
LPAD a gelince hierarchial a özek değil. left padding soldan doldurma demek. verilen uzunluğa gelinene kadar kelimenin soluna 
eğer verilmişse verilen karakterle verilmemişse boşlukla doldurulur.

hocam birde bu bağlantı olayında bir satırı hariç tutmak istiyorsak where kullanabiliriz. eğer ki where kullanırsak sadece bu istemediğimiz row yazılmaz ama bbu durumda 
bu çıkarttığımız rowun altındakş ona bağlı olan row çıkartılan row un üstüne bağlı gibi gözükür. 
diğer bir yöntemde connect by kısmından sonra and ekleyip istemediğimiz satırı belirtmektir bu durumda ise istemediğimiz row ile birlikte onun altında
ona bağlı tüm rowlar çıkatılır.

```sql
            SELECT last_name
            from employees 
            where last_name != 'Higgings'
            START WITH last_name = 'Kochar'
            CONNECT BY PRIOR employee_id = manager_id;
```
```sql
            SELECT last_name 
            from employee
            START WITH last_name 'sabbah'
            CONNECT BY PRIOR last_name='putin'
            AND last_name != 'soylu';
```
## Equijoin
hocam NATURAL, USING, ON(if use = ) equijoin türleridir. bunları yazmadan direkt where ilede join yapılabilir. 
sayrıca bu yazım sayesinde birden fazla tablodan birden sorgu yapabiliriz
önce neyi alacağımızı sonra nereden alacağımızı en sonra danasıl alacağımızı yazarız
```sql
            SELECT table1.column, table2.column 
            from table1, table2
            WHERE table1.column = table2.column;
```
gerçek bir örnek
```sql
            SELECT employee.last_name, departments.depaerment_id
            from employee, departments
            WHERE employee.department_d = departments.department_id;
```
aliese her iki tabloda aynı column yoksa kısa ad dahi yazmana gerek yoktur. ayrıca filtrelemek içinde and kullanabiliriz.
mesala burada istediğimiz bilgileri sadece 80 id nuber lı depaertman için yazdırıcaz.

```sql 
            SELECT last_name, e.job_id, job_title
            from employees e, jobs j
            WHERE e.job_id = j.job_id
            AND department_id = 80;
```
Birde hocam böyle from kısmında kısa ad belirtiysen ister öncesş ister sonrası tablonunn kendi adının  yazarsan hata alırsın. 
yanı from kısmında kısa ad belirtiyorsan her zaman onu kullanmak zorundasın.

## Cartesian Product 
eğer ki where kullanmazsan nasıl birleştireciğini bielemz ve ona göre yapayım buna göre mi yapayım derken kartezyen çarpar :))
```sql
            SELECT last_name, job_id
            from employees e, jobs j;
```
nur topu gibi cross join oldu.


## üç tablo birleştirme
şimdi üç tabloyu sadece where ve and kullanarak birleştirelim.
```sql
            SELECT last_name, city
            from employees e, departments d, locations l
            WHERE e.department_id = d.department_id
            AND d.location_id, l.location_id;
```
## Nonequijoin 

buna da iki tür girer bir ON join nin between ile kullanılanı = kullanılmayanı varya o birde outer joins (left, right) full olmaz :))
hadi yazımına da bakalım
bu left outer join oluyor :))
```sql 
            SELECT e.last_name, d.department_id, d.department_name
            from employee e, departments d
            WHERE e.department_id = d.department_id(+)
```
bu da right outer join
```sql 
            SELECT e.last_name, d.department_id, d.department_name
            from employee e, departments d
            WHERE e.department_id(+) = d.department_id
```
bu sol sağ ters unutmayalım. 

## Group Functions
öncelikle numeric olanlardan başlayalım **SUM**, **AVG**, **COUNT**, **MIN**, **MAX**, **VARIANCE** (varyans), **STDDEV** (standard sapma)
-> sum toplamı count satır sayısını döndürür.
hepsinin syntaxı aynı mantıkta
```sql
            SELECT MIN(salary) from employees;
```

onemli not grup fonksiyonlarını where 'in yanında kullamazsın. joinleri kullanıyorduk ama grup fonksiyonları olmaz
where salary = avg(salary) gibi bir kodda hata alırsın BOM! birde grup fonksiyonşarı NULL değerini göz ardı eder!

MIN, MAX ve COUNT her verei tipi için kullanılabilir. hani stringde str uzunluğına tarşhte en erken tarihe bakar fln

SUM, AVG, STDDEV, VARIANCE tahmin edeceğin üzere sadece numeric veride çalışır

**count adına notlar**  hocam count(*) da diyebiliriz mesela
```sql
            SELECT COUNT(*) from employees WHERE hire_date < '01-JAN-1996';
```
burada verilen tarihten önce işe giren kaç kişi oldjuğunu yazdırır bu satırların null değer içerip içermemesi önemli değildir.

örneğin her meslek bir defa yazdırılacak şekilde meslek adı ve id sıne ulaşırız.
**DISTINCT** dublicated satırlardan kurtarır her birininden bir defa olmasının sağlar
```sql
            SELECT DISTIMCT job_id, job_id from employee ;
```
aşşağıdaki kodda ise kaç farlı meslek türü olduğunun sayısına ulaşırız :))
```sql
            SELECT COUNT(DISTINCT job_id) 
```

**NVL** iki argüman alır ilki null ise ikiciyi say der. mesala siparişleir hesaplıyaz ama null olunca avg hesaba katmıhyor ama biz onun sıfır olarak kabul edilip hesaplanmasını istiyoruz.
```sql
            SELECT AVG(NVL(comission_pct ,0)) FROM employees;
```

## Group By 
gruplandırm aişine yarar.
```sql
            SELECT MAX(salary), department_i from employees
            GROUP BY department_id;
```
her departmanın max maaşını yazdırır. mesala burada birde selection ın yanına last_name yazdırmaya kalkışsaydık hata alırdık çünkü 
department_id e göre gruplaması gerekiyor ama last_name özel ve gruplanamaz.

**group by ve count** birlikte kullanımı 
```sql
            SELECT COUNT(country_name), region_id from counrties 
            GROUP BY region_id;
```
işte her bölgede kaç tane ülke olduğunu yazdırır. biliyorsun ki count null değeri görmezden geleceği için hiç ülkeye 
sahip olmayan bölgeler yazdırılmayacaktır. mesala bu kodda count(*) deseydikte aynı region_id değerine sahip ka.ç satur avr onu öğreniridk
* group by ile where de kullanılabilr sıkıntı olmaz

iç içe gruplar yapabilirz
```sql
            SELECT department_id, job_id, count(*)
            from employees
            GROUP BY department_id, job_id;
```
bu şekilde her departmanda kaç iş ve her iş te kaç çalışan  oldupunu görebileceğiz.

* **HAVING** kullanımı
having kullandığımız zaman çnce gruplamayı yapar sonra sadece şarta uyan grupları yazdırır.
```sql
            SELECT region_id, ROUND(AVG(population))
            from countries 
            GROUP BY region_id
            HAVING MIN(population)>300000 ;
```
önce her ortalam populasyon sayılarına bölge bölge bulur sonra gruplardan içerisinde verilen sayıdan küçük popilasyon bulundurmayan gruplar yazdırılır.
dikkat edelim maksat ort ın bu sayıyı sağlaması değil yapılna grubun her hangi bir üyesinin uyumsuzluk çıkarmaması sayıya uyması :))

kodda order by kullanma durumda da her zaman sona yazılır.

## Rollup 
group by ile kullanılır. birden fazla gruplama bir nevi iç içe gruplama sağlar. gruplamayı verilen listede sağdan sola doğru yapar
```sql
            SELECT departmentt_id, job_id, SUM(salary)
            from employees
            WHERE department_id < 50
            GROUP BY ROLLUP department_id, job_id;
```
sonuç nasıl olur dersek hocam rollup a iiki argüman veririsen üç çıktı alırsın yanı çıktı column sayısı argüma sayısı+1 olur :)
eğer burada rollup kullanmasaydık her department_id için değerleri gözlemlerdik fakat her job_id için olmazdı. rollup kullandığımız sonuç satırı daha fazla olur
