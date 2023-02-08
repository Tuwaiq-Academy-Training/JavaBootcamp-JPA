
ماهو JPA :

تعد واجهة برمجة تطبيقات جافا (JPA) أحد مواصفات جافا. يتم استخدامه لاستمرار البيانات بين  Java Object وقاعدة البيانات العلائقية. يعمل JPA كجسر بين نماذج المجال الموجهة للObject وأنظمة قواعد البيانات العلائقية.

نظرًا لأن JPA هي مجرد مواصفات ، فهي لا تقوم بأي عملية بمفردها. يتطلب التنفيذ. لذا ، فإن أدوات ORM مثل Hibernate و TopLink و iBatis تنفذ مواصفات JPA لاستمرار البيانات.


----------


ماهو Hibernate :

الHibernate إطار عمل Java يستخدم لتخزين Java Objects في نظام قاعدة البيانات العلائقية. إنها أداة مفتوحة المصدر وخفيفة الوزن Object Relational Mapping) ORM)
يعد Hibernate هو تنفيذ JPA. لذلك ، فهو يتبع المعايير المشتركة التي توفرها JPA.


----------


ماهو Repository :

المستودع (persistence layer, or adapter) يلخص عمليات الثبات: البحث (بواسطة ID أو معايير أخرى) ، حفظ (إنشاء ، تحديث) وحذف السجلات. يجب أن لا شيء أكثر من ذلك.




![](https://paper-attachments.dropbox.com/s_BFB0ED6EADDF6D8B91026AFB6AA747E8B5FDC90E1D3D1685F74542EE4343EBE6_1651144267803_image.png)



----------


ماهو Java Persistence Query language ( JPQL )

الJPQL is Java Persistence Query Language المحددة في مواصفات JPA. يتم استخدامه لإنشاء استعلامات مقابل الكيانات لتخزينها في قاعدة بيانات علائقية. تم تطوير JPQL على أساس بناء جملة SQL. لكنها لن تؤثر على قاعدة البيانات بشكل مباشر.


-----------


انواع الـ Query بإستخدام JPA : 


1- النوع الاول : 

بإستخدام الدوال الجاهزة 


    @Repository
    public interface UserRepository extends JpaRepository<User, Long> {
    }


2- النوع الثاني :

بإنشاء دوال جاهزة

| Keyword                | Sample                                                        | JPQL snippet                                                       |
| ---------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------ |
| `Distinct`             | `findDistinctByLastnameAndFirstname`                          | `select distinct … where x.lastname = ?1 and x.firstname = ?2`     |
| `And`                  | `findByLastnameAndFirstname`                                  | `… where x.lastname = ?1 and x.firstname = ?2`                     |
| `Or`                   | `findByLastnameOrFirstname`                                   | `… where x.lastname = ?1 or x.firstname = ?2`                      |
| `Is`, `Equals`         | `findByFirstname`,`findByFirstnameIs`,`findByFirstnameEquals` | `… where x.firstname = ?1`                                         |
| `Between`              | `findByStartDateBetween`                                      | `… where x.startDate between ?1 and ?2`                            |
| `LessThan`             | `findByAgeLessThan`                                           | `… where x.age < ?1`                                               |
| `LessThanEqual`        | `findByAgeLessThanEqual`                                      | `… where x.age <= ?1`                                              |
| `GreaterThan`          | `findByAgeGreaterThan`                                        | `… where x.age > ?1`                                               |
| `GreaterThanEqual`     | `findByAgeGreaterThanEqual`                                   | `… where x.age >= ?1`                                              |
| `After`                | `findByStartDateAfter`                                        | `… where x.startDate > ?1`                                         |
| `Before`               | `findByStartDateBefore`                                       | `… where x.startDate < ?1`                                         |
| `IsNull`, `Null`       | `findByAge(Is)Null`                                           | `… where x.age is null`                                            |
| `IsNotNull`, `NotNull` | `findByAge(Is)NotNull`                                        | `… where x.age not null`                                           |
| `Like`                 | `findByFirstnameLike`                                         | `… where x.firstname like ?1`                                      |
| `NotLike`              | `findByFirstnameNotLike`                                      | `… where x.firstname not like ?1`                                  |
| `StartingWith`         | `findByFirstnameStartingWith`                                 | `… where x.firstname like ?1` (parameter bound with appended `%`)  |
| `EndingWith`           | `findByFirstnameEndingWith`                                   | `… where x.firstname like ?1` (parameter bound with prepended `%`) |
| `Containing`           | `findByFirstnameContaining`                                   | `… where x.firstname like ?1` (parameter bound wrapped in `%`)     |
| `OrderBy`              | `findByAgeOrderByLastnameDesc`                                | `… where x.age = ?1 order by x.lastname desc`                      |
| `Not`                  | `findByLastnameNot`                                           | `… where x.lastname <> ?1`                                         |
| `In`                   | `findByAgeIn(Collection<Age> ages)`                           | `… where x.age in ?1`                                              |
| `NotIn`                | `findByAgeNotIn(Collection<Age> ages)`                        | `… where x.age not in ?1`                                          |
| `True`                 | `findByActiveTrue()`                                          | `… where x.active = true`                                          |
| `False`                | `findByActiveFalse()`                                         | `… where x.active = false`                                         |
| `IgnoreCase`           | `findByFirstnameIgnoreCase`                                   | `… where UPPER(x.firstname) = UPPER(?1)`                           |



3- النوع الثالث :

بكتابة JPQL 


    @Repository
    public interface UserRepository extends JpaRepository<User, Long> { 
    
    @Query("select u from User u where u.emailAddress = ?1") 
    User findByEmailAddress(String emailAddress); 
    
    }




