# Oracle SQL 

değişke tipleri

hocam cahr ve varcahr arasında  şöyle bir fark var char(50) dersen  5 karakter girdiğinde kalan 45  boşlukta doldurulur🥲
varchar ise sadece 5 kaarkterlik yer kaplar. 50 max sayısı olur.
number(10,2) birinci kısım anlamsı sayı ikinci sayı  virgülden sonraki dikkate alınacak kısımdır.

# Tablo oluşturma
kral döndü :))

tablo oluşturmak için CREATE TABLE komuutunu kullanırız. not null olanlar boş bırakılamaz. diğer değişkenlerin boş bırakırsan 
null olur. sıkıntı çıkmaz.
```sql
            CREATE TABLE new_table
            (
                name varchar2(20) not null,
                sur_name varchar(20),
                age number(3)
            );
```

# ALTER TABLE

## Yeni kolon keleme 
alter table + add
```sql
            ALTER TABLE new_table
            ADD(new_colomn varchar(20) Default 'empty' );
```

## değişkne tipi/ size/ default
hocam char varcah arasında dönüşüm yapılabilr ama ya belirlediğin size bukunan değerlerden daha az omaycak yada null olacak.
defaut değerde bundan sonra ekleneen satırlada geçerli olur. 
keyword MODIFY
```sql
            ALTER TABLE new_table
            MODIFY (age number(4));

            ALTER TABLE new_table
            MODIFY(age number(4) DEFAULT 0);
```
## Kolon Silme
```sql
            ALTER TABLE new_table DROP COLUMN new_tale; 
```

# INSERT INTO
## SATIR EKLME
iki şekilde kulanılır ya direkt yeni satır eklersin tüm değişknelri içerir yada belli değişkenleri içeren yeni satır eklersin.
kısaca insert into ile her zaman yeni satır oluşturulur ancak tüm değişkelerimi gireceğiz yoksa belli değişkneler doldurulup gerisi boş mu bırakılacak onu belirleriz.
```sql
        INSERT INTO new_table
        VALUES('Necmiye','Soylu',22);

        INSERT INTO new_table (name,age)
        VALUES('kemal',25);
```

