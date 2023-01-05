
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


----------
مثال برنامج القهوة بإستخدام قاعدة بيانات `SQL Database`

قاعدة البيانات هي وسيلة لحفظ وترتيب البيانات، وكلمة `SQL` تعني `Structured Query` ```Language` وتعني `لغة الاستعلام الهيكلية`.


تعتمد القواعد من نوع `SQL` بشكل أساسي على مفهوم الجداول `T``able` بحيث أنه عند إضافة بيانات جديدة يجب علينا مسبقًا تعريف جدول خاص لهذا النوع من المعلومات، ومن الممكن تشبيه Table في SQL في Class في لغات البرمجة إضافة إلى أهمية وجود أعمدة أو Column، ويمكن تشبيه الأعمدة بالخواص الخاصة بكل Class. وتحتوي قاعدة البيانات على سجلات وتسمى Records وهي البيانات الخاصة بهذا الجدول.
من المهم احتواء الجداول على عمود يحتوي على `primery key` وهو بمثابة المفتاح التعريفي الخاص بهذه البيانات.
ويمكننا تمثيل القهوة بهذا الشكل:

![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638445313570_Blank+diagram+-+Page+1+3.png)

- حددنا اسم الجدول Coffee.
- العمود id هو `primery key` الخاص بهذا الجدول ونوعه هو varchar(255)، أي أن قيمته يمكن أن تحتوي على ٢٥٥ حرف.
- العمود name ونوعه هو varchar(255)، أي أن قيمته يمكن أن تحتوي على ٢٥٥ حرف.
- العمود price ونوعه هو double، أي من الممكن أن يحتوي على قيمة من نوع عدد عشري.


    
العلاقات في `SQL Database`

قواعد البيانات من نوع `SQL Database` أو ما تسمى `Relational database`، بمعنى أنها قاعدة بيانات أساسها هو العلاقات بين الجداول. وتنقسم هذه العلاقات إلى ثلاثة أنواع أساسية:
 
علاقة one to one 
في هذه العلاقة يقترن سجل واحد في جدول بسجل واحد فقط في جدول آخر. على سبيل المثال في قاعدة بيانات المدرسة يكون لكل طالب معرف طالب واحد فقط، ويتم تعيين معرف الطالب لشخص واحد فقط.

تبدو العلاقة كما في الرسم البياني التالي للعلاقات:

![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638446314831_Blank+diagram+-+Page+1+4.png)


نلاحظ في الشكل الأعلى ارتباط جدول الطالب بجدول معلومات التواصل بعلاقة one to one بحيث أن لكل سجل في جدول الطالب معلومة واحدة في جدول معلومات التواصل. 

علاقة one to many 
في هذه العلاقة يمكن إقران سجل واحد في جدول بسجل واحد أو أكثر في جدول آخر. على سبيل المثال يمكن أن يكون لكل عميل العديد من الطلبات.

تبدو علاقة one to many على النحو التالي في الرسم البياني للعلاقات:

![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638446922720_Blank+diagram+-+Page+1+5.png)


نلاحظ في الشكل أعلاه إرتباط جدول العميل بجدول الطلبات بعلاقة one to many، بحيث أن من الممكن أن يكون هناك العديد من الطلبات لكل عميل، ونلاحظ كذلك وجود كلمة Foreign key عند جدول الطلبات وهو عبارة عن مفتاح يرتبط بـ PRIMERY_KEY الخاص بجدول العميل.

علاقة many to many 
تحدث علاقة many to many عندما تقترن سجلات متعددة في جدول بسجلات متعددة في جدول آخر. على سبيل المثال توجد علاقة many to many بين العملاء والمنتجات، حيث يمكن للعملاء شراء منتجات متنوعة، ويمكن للعديد من العملاء شراء المنتجات.

لا تسمح لك أنظمة قواعد البيانات الارتباطية عادةً بتنفيذ علاقة many to many مباشرة بين جدولين. بالنظر على سبيل المثال لتتبع الفواتير، فإن كان هناك العديد من الفواتير بنفس رقم الفاتورة واستفسر أحد العملاء عن رقم هذه الفاتورة، فلن يتم التعرف على الفاتورة الخاصة به، وهذا أحد أسباب تعيين قيمة فريدة لكل فاتورة.

لتجنب هذه المشكلة يمكن تقسيم علاقة many to many إلى علاقتين one to many باستخدام جدول ثالث يسمى جدول الربط `JOIN`. يتضمن كل سجل في جدول `JOIN` حقل تطابق يحتوي على قيمة `PRIMERY_KEY` للجدولين اللذين ينضمان إليه (في جدول `JOIN` حقول المطابقة هي `Foreign key`). يتم ملء حقول المفاتيح الخارجية بالبيانات حيث يتم إنشاء السجلات في جدول `JOIN` من أي جدول ينضم إليه.

فالعلاقة بين الطلاب والفصول تمثل علاقة many to many، حيث يمكن للطالب التسجيل في العديد من الفصول ويمكن أن يضم الفصل العديد من الطلاب.

يتضمن المثال التالي جدول الطلاب والذي يحتوي على سجل لكل طالب، وجدول الفصول والذي يحتوي على سجل لكل فصل. ولإضافة علاقة many to many بين جدول الطالب وجدول الفصل سنقوم بإنشاء جدول ثالث يحتوي على علاقتين one to many مع الجداول التي بينها علاقة many to many. في الشكل التالي قمنا بإنشاء جدول `enreolment` ويحتوي على `Foreign key` لكل من جدول الطالب وجدول الصف:

![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638447694113_Blank+diagram+-+Page+1+6.png)



إنشاء `postgresql` باستخدام `Docker`

سنقوم في هذه الوحدة بإنشاء قاعدة بيانات `postgresql` باستخدام `Docker`.
يمكنك تحميل docker من هنا.
بعد تحميل وتثبيت Docker سنقوم بكتابة هذا الأمر في Terminal:

    docker run --name postgresql-1  -e POSTGRES_PASSWORD=docker -p 5432:5432  -d postgres

والذي سيقوم بإنشاء حاوية خاصة بقاعدة البيانات، ويمكننا رؤيتها من خلال الذهاب إلى `Docker Desktop`.

- خاصية —name خاصة باسم الحاوية `C``ontainer`.
- خاصية -e خاصة بخواص البيئة وقمنا بإضافة POSTGRES_PASSWORD وإعطائه قيمة Docker وهو الرمز الخاص به.
- خاصية -p وهو خاص بالمنفذ أو `port` الخاص بهذا `C``ontainer`. 
![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638456904648_image.png)


ثم سنقوم بالضغط على الأيقونة وسوف تفتح نافذة `T``erminal` خاصة بهذه الحاوية. ثم سنقوم بكتابة هذا الأمر وهو الأمر الخاص بدخول psql والذي من خلاله يمكننا إضافة قواعد بيانات أو جداول:

     psql -U postgres

الآن سوف ننشئ قاعدة بيانات باسم coffee-shop:

    CREATE DATABASE coffee shop:

ويمكننا الدخول إلى قاعدة البيانات عن طريق كتابة هذا الأمر:

    \c coffee_shop;


![](https://paper-attachments.dropbox.com/s_4E5081556D8D7995404A88F735C9A07394B3AAF32E4850A4FE39753C3240EBAD_1638457416937_image.png)




ربط `Spring Boot` بقاعدة البيانات 

في هذه الوحدة سنقوم بربط مشروع `Spring Boot` بقاعدة البيانات، كما سنقوم باستخدام JPA من أجل استخراج وإضافة بيانات إلى قاعدة البيانات.
 

ماذا سنتعلم؟ 
- إضافة مكتبات إلى مشروع `Spring Boot`.
- ربط `Spring Boot` بقاعدة البيانات. 
- استخدام `JPA`.
- تحديث مشروع القهوة.


إضافة مكتبات إلى مشروع `Spring Boot`

من أجل استخدام قاعدة البيانات مع مشروع Spring Boot فنحن بحاجة إلى إضافة بعض المكتبات، ومن أجل إضافة هذه المكتبات سنقوم بالدخول إلى ملف pom.xml.

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>


- مكتبة spring-boot-starter-data-jpa وهي المكتبة المسؤولة عن إضافة طبقة ORM والتي ستجعل عملية استخراج البيانات من قاعدة البيانات أسهل. 
- مكتبة postgresql وهي المكتبة المسؤولة عن ربط مشروع Spring Boot بقاعدة بيانات من نوع postgresql. 
- كما أن هناك العديد من المكتبات الأخرى وهي لأنواع أخرى من قواعد البيانات.
ربط `Spring Boot` بقاعدة البيانات 

لربط المشروع بقاعدة البيانات سنقوم بإضافة بعض التفضيلات في ملف application.properties
الموجود في هذا المسار:

    src/main/resources/application.properties

 وسنقوم بإضافة هذه الأسطر:

    spring.jpa.database=postgresql 
    spring.datasource.url=jdbc:postgresql://localhost:5432/coffee_shop
    spring.datasource.username=postgres
    spring.datasource.password=docker
    spring.jpa.show-sql=true
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
    spring.jpa.properties.hibernate.format_sql=true
    spring.jpa.hibernate.ddl-auto=create


استخدام JPA

الآن سوف نتجه إلى ملف Coffee.java وسنقوم بإضافة بعض `Anatoations` الخاصة JPA.


    package com.coffeeshop.coffeeshop.Coffee;
    import javax.persistence.Entity;
    import javax.persistence.GeneratedValue;
    import javax.persistence.GenerationType;
    import javax.persistence.Id;
    import javax.persistence.Table;
    @Entity
    @Table
    public class Coffee {
        @Id
        @GeneratedValue(strategy = GenerationType.SEQUENCE)
        Long id;
        String name;
        double price;
        public Coffee() {
        }
        public Coffee(String name, double price) {
            this.name = name;
            this.price = price;
        }
        public Coffee(Long id, String name, double price) {
            this.id = id;
            this.name = name;
            this.price = price;
        }
        public void updateCoffee(Coffee c) {
            this.name = c.name;
            this.price = c.price;
        }
        public Long getId() {
            return id;
        }
        public String getName() {
            return name;
        }
        public double getPrice() {
            return price;
        }
        public void setName(String name) {
            this.name = name;
        }
        public void setPrice(double price) {
            this.price = price;
        }
        @Override
        public String toString() {
            return "Coffee [id=" + id + ", name=" + name + ", price=" + price + "]";
        }
    }
    


- رمز `@Entity و @Table` لإثبات أن هذا Class سيصبح جدول في قاعدة البيانات. 
- رمز `@id و @GeneratedValue(strategy = GenerationType.SEQUENCE)` لتحديد المفتاح الأساسي الخاص بهذا الجدول.
- الآن عند القيام بتشغيل المشروع سوف نلاحظ إنشاء جدول خاص بالقهوة coffee.
    
      .   ____          _            __ _ _
     /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
    ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
     \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
      '  |____| .__|_| |_|_| |_\__, | / / / /
     =========|_|==============|___/=/_/_/_/
     :: Spring Boot ::                (v2.6.1)
    
    
    Hibernate: 
        
        drop table if exists coffee cascade
    Hibernate: 
        
        drop sequence if exists hibernate_sequence
    Hibernate: create sequence hibernate_sequence start 1 increment 1
    Hibernate: 
        create table coffee (
           id int8 not null,
            name varchar(255),
            price float8 not null,
            primary key (id)
        )

سنقوم الآن بإضافة الملفات الخاصة بتعديل وإضافة البيانات من وإلى قاعدة البيانات، وسنضعهم بداخل مجلد coffee.

ملف `CoffeeRepository.java`


    package com.coffeeshop.coffeeshop.Coffee;
    import org.springframework.data.jpa.repository.JpaRepository;
    import org.springframework.stereotype.Repository;
    @Repository
    public interface CoffeeRepository extends JpaRepository<Coffee, Long> {
    }

 وهو ملف خاص لإنشاء `interface` خاصة بالقهوة لكي نستعمل جميع خواص `JpaRepository` الخاصة. من المهم إضافة نوع `C``lass` المطلوب ونوع id الخاص بهذا `C``lass`.  
 كذلك من المهم إضافة `@Repository`  لتحديد أن هذا `interface` عبارة عن `Repository`.

 
ملف `CoffeeService.java`


    package com.coffeeshop.coffeeshop.Coffee;
    import java.util.List;
    import java.util.Optional;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    @Service
    public class CoffeeService {
        private final CoffeeRepository coffeeRepository;
        @Autowired
        public CoffeeService(CoffeeRepository coffeeRepository) {
            this.coffeeRepository = coffeeRepository;
        }
    }

 
 هو الملف الخاص بإضافة واستخدام خصائص `JpaRepository`.

- في البداية علينا إضافة `@Service` لتحديد أن هذا `C``lass` عبارة عن `Service`.
- قمنا بإضافة `final` من نوع `CoffeeRepository` باسم `coffeeRepository` .
- قمنا بإضافة `initializer` خاص بهذا `C``lass`. 
- قمنا بإضافة `@Autowired` وذلك لإضافة هذا `C``lass` بشكل مباشر عند إنشاء مشروع `SpringBoot`.


سنقوم الآن بإضافة خواص `CRUD` باستخدام `coffeeRepository`:


    List<Coffee> getAllCoffees() {
        return coffeeRepository.findAll();
    }
    Optional<Coffee> getCoffeeById(Long id) {
        return coffeeRepository.findById(id);
    }
    Coffee addNewCoffees(Coffee c) {
        return coffeeRepository.save(c);
    }
    Optional<Coffee> editCoffeeById(Long id, Coffee c) {
        if (coffeeRepository.existsById(id)) {
            Coffee chosenCoffee = coffeeRepository.getById(id);
            chosenCoffee.setName(c.name);
            chosenCoffee.setPrice(c.price);
            return Optional.of(coffeeRepository.save(chosenCoffee));
        }
        return Optional.empty();
    }
    boolean removeCoffee(Long id) {
        if (coffeeRepository.existsById(id)) {
            coffeeRepository.deleteById(id);
            return true;
        }
        return false;
    }

باستخدام هذه الدوال يمكننا الوصول إلى قاعدة البيانات وإضافة وتعديل وحذف البيانات.


- دالة `getAllCoffees` مسؤولة عن إظهار جميع البيانات.
- دالة `getCoffeeById` مسؤولة عن إظهار قهوة باستخدام id.
- دالة `addNewCoffees` مسؤولة عن إضافة قهوة جديدة.
- دالة `editCoffeeById` مسؤولة عن تعديل بيانات القهوة.
- دالة `removeCoffee` مسؤولة عن حذف بيانات القهوة.


تعديل ملف `CoffeeController.java`


    @RestController()
    @RequestMapping("/coffee")
    public class CoffeeController {
        private final CoffeeService coffeeService;
        @Autowired
        public CoffeeController(CoffeeService coffeeService) {
            this.coffeeService = coffeeService;
        }
    ...


- قمنا بإضافة `final` من نوع `CoffeeService` باسم `coffeeService`.
- وقمنا بتعديل `initializer` خاص بهذا `C``lass`. 
- قمنا بإضافة `@Autowired` وذلك لإضافة هذا `C``lass` بشكل مباشر عند إنشاء مشروع `SpringBoot`.



        @GetMapping
        List<Coffee> getCoffees() {
            return coffeeService.getAllCoffees();
        }
        @GetMapping("/{id}")
        ResponseEntity<Optional<Coffee>> getCoffeeById(@PathVariable Long id) {
            Optional<Coffee> c = coffeeService.getCoffeeById(id);
            if (c.isPresent()) {
                return new ResponseEntity<>(c, HttpStatus.FOUND);
            }
            return new ResponseEntity<>(Optional.empty(), HttpStatus.NOT_FOUND);
        }
        @PostMapping()
        public ResponseEntity<Coffee> postNewCoffee(@RequestBody Coffee c) {
            Coffee newCoffee = coffeeService.addNewCoffees(c);
            return new ResponseEntity<>(newCoffee, HttpStatus.CREATED);
        }
        @PutMapping("/{id}")
        ResponseEntity<Optional<Coffee>> putCoffee(
                @PathVariable Long id,
                @RequestBody Coffee c) {
            Optional<Coffee> result = coffeeService.editCoffeeById(id, c);
            return new ResponseEntity<>(result, HttpStatus.NOT_FOUND);
        }
        @DeleteMapping("/{id}")
        ResponseEntity<Optional<String>> deleteCoffeeById(@PathVariable Long id) {
            if (coffeeService.removeCoffee(id)) {
                return new ResponseEntity<>(Optional.of("Deleted"), HttpStatus.OK);
            }
            return new ResponseEntity<>(Optional.of("Not Found"), HttpStatus.NOT_FOUND);
        }


- تعديل جميع الدوال الخاصة بهذا `C``lass` واستخدام `coffeeService` من أجل تحديث البيانات في قاعدة البيانات.




