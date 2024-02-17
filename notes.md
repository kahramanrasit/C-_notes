# C++

- C++ salt nesne yönelimli (Object-oriented programming language OOP) bir programlama dili değildir.
- C++ multi-paradigm bir programlama dilidir. Yani çok paradigmalıdır.
  - paradigma: programı oluştururken kullanılan genel yaklaşım, genel metodolojidir.
    
Örnek olarak C prosedürel paradigma kullanılan bir dildir.
  - Prosedürel paradigma: tipik olarak functional decomposition kullanılır. Yani yapılması gereken iş küçük küçük parçalara bölünüp
  o parçalar fonksiyonlar şeklinde ifade edilir ve veri de o fonksiyonlar kullanarak işlenir. Bu yöntem bir paradigmadır.
  Yani programlama yaparken kullandığımız genel yaklaşıma, metodolojiye programlama paradigması denir.

```
C++ multi-paradigm bir dildir.
    - prosedürel programlama
    - nesne yönelimli / nesne tabanlı
    - generic programlama (türden bağımsız programlama)
    - fonksiyonel programlama / functional programming
    - data abstraction
```

C ile C++ dili arasındaki farklılıkların hepsi olmasa da bir kısmı aşağıdaki nedenlerle ilgilidir. 
- C programlama dili küçük ve genel bir dildir. C dilinde derleme zamanında yapılan kontroller sınırlıdır.
Yani C ve C++ dilleri statik tür kavramına sahip olmasına rağmen C dilinde statik tür kontrolü daha gevşektir, zorlayıcı değildir.
Bu durum hata yapma riskini artırır. Örneğin C dilinde farklı türler arasındaki atama ve kopyalama durumlarının çoğu legaldir.
Günümüzde modern derleyiciler bu tip hatalara yönelik uyarı mesajları veriyor olsalar da dilin kurallarına göre farklı türler arasında çoğunlukla "type conversion"
söz konusudur. Fakat C++ dili tür kontrolü konusunda çok daha katı(strict)'dir.
```
    C    -> loose typing
    C++  -> strict typing 
```

- C ile C++ dili arasındaki farklılıkların önemli bir kısmı tür dönüşümleri konusuyla ilgilidir. Normal şarlarda
iyi bir C developer da bu dönüşümlere dikkat etmelidir.

Undefined Behavior: Yazılan kod, dilin kurallarına göre derleyicinin kontrolünden geçebilir. Yani derleyicinin gözlemleyebileceği
bir sentaks hatası olmayabilir. Fakat derlenip çalıştırıldıktan sonra nasıl bir durum oluşacağı konusunda hiçbir garanti yoktur. 
Türkçe "tanımsız davranış" olarak kullanılabilir.

Unspecified Behavior: Derleyiciye bağlı durum. Derleyiciden derleyice değişiklik gösterebilen durumlardır.

```
implicit type conversion - Bu tür dönüşümü compiler tarafından otomatik olarak yapılır.
explicit type conversion - Bu dönüşüm programcı tarafından manuel olarak yapılır.
```

- C++'da implicit int dönüşümü geçerli değildir.

```
Bir fonksiyon olarak düşünürsek;
func(int x)
{
//
}
Yukarıdaki fonksiyonun geri dönüş değeri belirtilmemiştir. C'de implicit bir şekilde int olarak dönüşüm gerçekleşirken C++'da
bu durum sentaks hatasıdır.
```

- Ayrıca bir fonksiyonun geri dönüş değeri var ise ve siz o fonksiyonu tanımlarken geri dönüş değeri vermediyseniz bu durum C'de Undefined Behavior oluştururken
C++'da sentaks hatasıdır.

- Aşağıdaki örnek için;
```
int func()
{
    bar();
}
```
Normalde bar ismi kullanıldığında name look up ile aranmak zorundadır. Aranan isim(identifier) olan bar, derleyici tarafından bulunamaz ise sentaks 
hatası olmalıdır. Ama böyle bir kodu bir C derleyicisinde derlediğiniz zaman geçerli olduğu görülür. C'de derleyici bar ismini arayıp bulamadığında
yani name look up başarısız olduğunda, fonksiyon çağrı operatörünün operantı bar olduğu görüldüğünde, bu fonksiyonun başka bir modülde tanımlanmış
external olan dışarıya açılmış geri dönüş değeri int olan ismi bar olan parametrik yapısı hakkında bilgi edinmediği bir fonksiyon olarak algılayacaktır.
Bu duruma implicit function declaration denir. Ancak bu durum C++'da sentaks hatasıdır.


- C dilinde 
```
int foo();
int bar(void);
```
Yukarıdaki iki fonksiyon aynı anlama gelmez. Yani foo fonksiyonunun parametrelerini boş bir şekilde çağırabiliriz. 
Bu bir sentaks hatası olmadığı gibi foo fonksiyonun parametresi de derleyici tarafından void algılanmaz.
Ancak C++ dilinde bir fonksiyon tanımlanırken parametre değişkeni yazılmadığında derleyici bunu void olarak algılar.

- C'de fonksiyonun tüm parametre değişkenlerine isim verilmek zorunda iken C++'da fonksiyonun parametre değişkenine isim
verilmek zorunda değildir. Bu durum C++'ın function over loading özelliğiyle alakalıdır.
```
void func(int)
{
}
```

- C'de aşağıdaki döngü için
```
#include  <stdio.h>
int main()
{
    for(int i = 0; i < 10; ++i) {
    int i = 99;
    printf("%d ", i);
    }
}
```

Bir ismin daha geniş kapsamdaki bir ismin görünmesini engellemisine name masking, name shadowing ya da name hiding denir. 
Bu durum C'de bir hata değilken C++'da sentaks hatası olarak görünür. 

# Türlere ve Tür dönüşümlerine ilişkin farklılıklar

- C'de
```
int isupper(int c);
```
Bu fonksiyon test fonksiyonu olmasına rağmen geri dönüş değeri int türdendir. Ancak C++'da bu tür  test fonksiyonları bool türünden olmalıdır.

Yani C'de false veya true bool türden sabitler değildir. C99 ile eklenen bir başlık dosyası vardır.
```
#include <stdbool.h>
```
true, false gibi tanımlanan makrolar içerir. 

Yani aşağıdaki gibi bir kod yazılırsa;
```
#include <stdbool.h>

int main()
{
    bool flag = true;
    flag = false;
}
```
Her ne kadar görüntüde sanki C++'da olduğu gibi bir lojik veri türü olan boolean veri türü kullanılmış gibi dursa da aslında burda true ve false birer makrodur.

Ancak C++'da durum böyle değildir. Herhangi bir  başlık dosyası eklemeden boolean veri türünü kullanabilirsiniz.

Uyarı: Test fonksiyonlarında asla geri dönüş değeri int türden yapılmaz. C++'ın semantik yapısında aykırıdır.

- C++'da bool bir anahtar sözcük(keywords)'dür. True ve false da aynı şekilde anahtar sözcüktür. bool türünün storage ihtiyacı 1 byte yani sizeof(bool) 1'dir ve
bitsel seviyede tutulma garantisi vardır. Yani ayrı bir memory location olma garantisi vardır.

- Eskiden C'de idiomatik bir yapı olan bool türünden bir değişkenin ++ ya da -- operatörünün operantı olması C++ dilinde geçerli değildir.
Yani C++'da bool türden değişkenler ++ veya -- operatörünün operantı olamazlar.

- C++ dilinde aritmatik türlerden bool türüne otomatik dönüşüm vardır.

Örnek olarak;
```
int x = 45;
bool b = x;
std::cout << std::boolalpha << b;
```
Yukarıdaki kod parçacığında bir sentaks hatası yoktur. non-zero değerler true, zero olan değerler ise false'a implicit olarak dönüştürülür. Ekrana true yazdırılır.

- Adres türlerinden boolean türüne doğrudan dönüşüm vardır. Bir adres türünden(pointer) bool türüne otomatik(implicit) dönüşüm yapmaya zorlarsanız, dönüşüm pointer'ın null pointer olup
olmamasıyla doğrudan ilişkilidir. null pointer ise false'a dönüşür. null pointer değil ise true olur. 

```
#include <iostream>

int* gp;

int main()
{
   int x  = 100;
   int* ptr = &x;

   bool b1 = ptr; // true
   bool b2 = gp;  // false
}
```
Yukarıdaki durumun tersi de geçerlidir.

```
bool flag = true;
bool is_on = false;

int x = flag;  // x'in değeri 1 olur
int y = is_on; // y'nin değer 0 olur
```

Uyarı: Boolean türünden pointer türüne aşağıdaki kod parçacığındaki gibi bir dönüşüm kesinlikle yoktur. 
```
bool is_on = false;
int *ptr = is_on;
```


- C dili ile C++ dili arasında user-defined type'lar arasında çok önemli bir fark vardır.

User-defined type C'de programcı tarafından oluşturulan türler olarak tanımlayabiliriz. Yani programcının bir bildirimle tür oluşturmasıdır.
Struct, enum ve union gibi anahtar sözcüklerinden birini kullanarak oluşturulan türlerdir.

C'de aşağıdaki gibi
```
struct Data {
    int a, b, c;
};
```
bir kod parçacığı yazdığınızda bu türün ismi Data değildir. Buradaki Data ismine "struct tag" denir. Aynı kullanım union ve enum için de geçerli. "union tag", "enum tag".
Yani bir typedef bildirimi olmadan bu tag'ler türün kendisini temsil etmiyor.

Örneğin C'de;
```
struct Data {
   int a, b, c;
};
int main()
{
    Data mydata; //Sentaks hatası olur.
    struct Data mydata; // doğru kullanımdır.
}
```
Yani tek başına tag olan isim; türü niteyen, türün yerine geçen isim değildir.
Dolayısıyla C'de bir ismi doğrudan bir yapı türünün ismi olarak kullanmak istiyorsak aşağıdaki gibi bir typedef (tür eş ismi) bildirimi zorunludur.

```
typedef struct Data{
   int a, b, c;
}Data;
int main()
{
    Data mydata;
}
```
- Ancak C++'da struct, union ve enum'da tag ismi doğrudan türü niteliyor. Yani C++'da typedef bildirimi olmadan doğrudan Data ismini tür ismi olarak
kullanabiliriz. class, struct, union ve enum için geçerlidir.

Aşağıdaki gibi;

```
struct Data{
   int a, b, c;
}
int main()
{
    Data mydata;
}
```

- C'de:
```
struct Data{

};
```
geçerli bir bildirim değildir. Yapı türleri söz konusu olduğunda yapının en az bir elemanı olması gerekiyor. C'de elemanı olmayan bir yapı geçerli bir bildirim oluşturmuyor.

Fakat C++'da bu şekilde oluşturulan sınıflar olabilir.

Dip not: C++'da struct, class diye bir ayrım yoktur. struct C++'da bir class'dır. Buna empty class denir ve C++'da önemli bir işlevi vardır.

 
 #### const anahtar sözcüğüne dair farklar

- C dilinde bir nesnenin const olması ve default initialize edilmesi geçerli bir durumdur.
```
const int x; // geçerli 
int main()
{
    //code
}
```
Ancak C++ dilinde const anahtar sözcüğüyle tanımlanan sözcükler initialize edilmek zorundadır. Yani default initialize edilmesi sentaks hatasıdır.


- C dilinde const olarak tanımlanmış nesnelerin oluşturulduğu ifadeler constant expression olarak değerlendirilmiyor!

Örneğin constant olarak tanımlanan bir identifier, array'ın boyutu olarak kullanılamaz.
```
const int x = 10;
int a[x] = {0}; // C'de geçersizdir.
```
Array'in boyutu constant expression olmalıdır. Bu sebeple const int bir değer C++'da kullanılabilir. Fakar C'de bir değeri sabit ifadesi olarak tanımlasanız da derleyici bu ifadeyi constant expression olarak algılamaz.

Uyarı: C++'da Const ifadelere sabit değer vermek mecburi değildir.
```
int get_size();
int main()
{
    const int size = 100;
    const int ds = get_size();

    int a1[size]; // ilk değeri sabit ifadesi ile aldığı için geçerlidir.
    int a2[ds];   // ilk değerini ds ifadesinden alıyor ve ds ifadesi değişken bir fonksiyona bağlı olduğu için geçerli değildir.
}

```

#### linkage

- C ve C++ dillerinde isimlerin bağlantı özellikleri vardır. Bağlantı(linkage), birden fazla kaynak dosyanın olması durumuyla ilgilidir.
Eğer bir isim birden fazla kaynak dosyada kulalnıldığında aynı varlığa ilişkin ise böyle isimlere "external linkage" adı verilir.
Ama aynı isim farklı kaynak dosyalarda kullanılırken her kaynak dosya için farklı bir varlığa ilişkin ise "internal linkage" adı verilir.

- C'de hatırlamak gerekirse globalde aşağıdaki kod parçacığında bir ifadenin external veya internal olmasının nasıl belirlendiğini hatırlayalım.
```
    int x; // external değişkendir.
    static int x; // internal değişkendir.
```

- C dilinde bir değişkenin const olması bağlantı özelliğini değiştirmez.
```
    const int x = 10; // C'de external linkage
```
C++'da global const isimler internal linkage olur.

- C dilinde const T* türünden T* türüne implicit dönüşüm vardır. Ancak C++'da bu durum sentaks hatasıdır.
```
    const int x = 10;
    int* p = &x; // C dilinde de doğru bir yazım olmamasına rağmen sentaks hatası değildir.
```
Ancak C++'da bu durum sentaks hatasıdır.


- Aşağıdaki kod parçacığı için;
```
    int y = 15;
    int x = 10;
    int* const ptr = &x;
```
const pointer to int kavramı kullanılır. Anlamı, ptr'nin kendisi const'tur. Yani ptr'nin tüm ömrü boyunca
x'i göstermesi istenir, ptr'nin başka bir nesneyi göstermesi lojik bir hata olacağından sentaks hatası olması da
const anahtar sözcüğü ile tanımlanır. C++'da top level const  terimi sıklıkla kullanılır.

- const pointer to int
- top-level const
- right const

kavramlarları kullanılır. 

Uyarı: Bu durumda x değişkeninin değer ptr üzerinden değiştirilebilir. ptr'nin gösterdiği nesne değiştirilemez. 

```
    *ptr = 45; // doğru bir kullanımdır. ptr'nin gösterdiği nesne değişmiyor. ptr hala x'i gösteriyor.
     ptr = &y; // kullanılamaz. Burada ptr'nin gösterdiği nesne değiştiriliyor.
```

- Bir de bu durumun tersi söz konusudur.
```
    int x = 10;
    const int* ptr = &x;
```
   - pointer to const
   - low level const
   - left const

Bu durumda ise ptr'nin gösterdiği nesne olan x, ptr yoluyla değiştirilemez. Yani x sadece salt okuma amaçlı kullanılabilir. 
```
    *ptr = 45; // yapılamaz. ptr ile sadece okuma yapılabilir.
```
Ancak unutulmamalıdır ki ptr const olmadığı için ptr'nin gösterdiği x nesnesi değiştirilip y yapılabilir.
```
    ptr = &y; // legaldir.
```
Özetle aşağıdaki gibi toplanabilir;
```
	 int x = 10;
	 int y = 5;

	 int* const ptr1 = &x;
	 // const pointer to int/top-level const/right const
	 //*ptr1 = 15; // legaldir
	 //ptr1 = &y; // illegaldir. 

	 const int* ptr2 = &y;
	 //pointer to const int/low level const/left const
	 //*ptr2 = 15; // illegaldir
	 //ptr2 =&x; // legaldir.
```

Kullanım örneği: T bir tür olmak üzere: 
```
    void func(T* p); // out-param 
```
Yukarıdaki fonksiyon mutator bir fonksiyondur. Değiştiricidir. Yani bu fonksiyona
bir nesnenin adresi gönderilirse bu nesnenin değerleri değiştirilebilir.

Not: Bir de C ve C++'da çok kullanılmasa da in-out param diye bir kavram vardır. Böyle bir fonksiyona 
bir nesnenin adresi gönderildiğinde o nesnenin verisi okunur, okunan bilgi üzerinden işlem yapılır ve yine 
aynı nesneye atamalar yapılır. 

```
    void foo(const T* p); // in-param
```
Yukarıdaki fonksiyon sadece p'nin gösterdiği nesnenin değerini okuyabilir. O nesneye herhangi bir şekilde yazma/değiştirme yapamaz.
Salt okuma amaçlı erişim.

Birde bu iki durumun aynı anda kullanılma hali vardır.
- const pointer to const int
```
    int x = 10;
    const int* const ptr = &x;
```
Bu durumda ptr'nin gösterdiği nesne değiştirilemez, ptr üzerinden nesnenin değeri de değiştirilemez.


Uyarı: C++'da hatırlandığı üzere const nesnelere ilk değer vermek mecburiydi. Ancak bu durum const pointer'lar için geçerli değildir.
```
    const int* p; // geçerlidir.
    int* const p; // geçersizdir.
```


#### Scope leakage (kapsam sızıntısı)

Bir değişken tanımlandığında, eğer o değişkeni kullanacağınız alan dışında da o değişkenin ömrü devam ediyorsa, bu duruma
kapsam sızıntısı denir.
```
    int i;
    for(i = 0; i < 10; ++i) {
    } 
```
Yukarıdaki örnekte eğer i sadece döngü değişkeni olarak kullanılması amaçlanmış ise döngüden sonraki satırlarda da o değişkenin ömrü 
devam ettiği için burada scope leakage vardır.

- C++ dilinde adresler ile aritmetik türler arasında örtülü dönüşüm yoktur. Ama C'de vardır.
Örnek olarak:
```
    int x = 35;
    int* p = x;
```
Burada amaç x'in adresi ile p pointer'ına ilk değer vermek olabilir. Ancak yukarıdaki şekilde yazıldığında,
p'ye c'in değeri ile ilk değer verilmiş oluyor. Eşittir'in sağ tarafındaki değişkenin türü int iken sol tarafındaki 
değişkenin türü int*'dır. C dilinde bu atama implicit olarak gerçekleşir. Doğru bir atama değildir. 

C++ dilinde aritmetik türler ile pointer türler rarasında dönüşüm söz konusu değildir.

Ayrıca C++ dilin de farklı türden değişkenler arasında da tür dönüşümü yoktur. 
```
    double dval = 45.12;
    char* p = &dval;
```
Yukarıdaki kod parçacığı C'de geçerli iken C++'da geçerli değildir.


- C'de yanlış olmamasına rağmen C++'da sentaks hatası olan bir örtülü(imlicit) dönüşüm örneği void* türünden diğer pointer türlerinedir.

Örnek olarak: 
```
    size_t n = 1000;
    int* p = malloc(n * sizeof(int));
```
malloc çağrı ifadesinin geri dönüş değeri void*'dır. Yukarıda p'ye int* türünden ilk değer veriliyor. Bu durum C'de legal bir durum iken yanlış bir kullanım da değildir.
Ancak C++'da tür dönüştürme operatörü kullanılması gerekir.


```
    enum Color { White, Gray, Brown, Black };
```
Yukarıdaki kod parçacığında Color ismini C'de başına enum yazmadan kullanabilmek için typedef'e ihtiyacınız vardır. C++'da böyle bir zorunluluk yoktur.

Underlying type: C'de numaralandırma türü bir tam sayı türüdür. Derleyici implementasyon tarafında numaralandırma türü olarak bir tam sayı türü olarak int kullanıyor. 
Yani C dilinde underlying type int'tir. Yani aşağıdaki assert her zaman doğrudur.
```
#include <stdio.h>
#include <assert.h>

enum Color { Blue, Black, Magenta };

int main()
{
    assert(sizeof(int) == sizeof(enum Color));
}
 
```

C++'da underlying type int olmak zorunda değildir. Eğer özel bir sentaks kullanarak underlying type belirtilmez ise numaralandırma sabitlerinin(enumaration constant, enumarator) değerleri söz konusudur.
Örneğin Brown enumaratör'ünü int sayı sınırlarına sığmayan bir tam sayı sabiti kullanılırsa derleyici C++'da underlying type'ı uygun şekilde değiştirir.


- C dilinde aritmetik türlerden enum türlerine otomatik (implicit) dönüşüm vardıır.
```
    enum Color { White, Gray, Brown, Black };

    int main()
    {
        enum Color mycolor;
        mycolor = 3; // implicit type conversion
    }

```
- C dilinde farklı enum türleri arasında (implicit) dönüşüm vardır.
```
    enum Color { White, Gray, Brown, Black };
    enum Pos { On, Off, Hold };

    int main()
    {
        enum Color mycolor = Brown;
        enum Pos mypos = Off;
        mycolor = mypos; // implicit type conversion
    }

```
Yukarıdaki örneklerde sentaks hatası yoktur. 

Ama C++ dilinde aritmetik türlerden numaralandırma türlerine ve farklı numaralandırma türleri arasında (implicit) örtülü tür dönüşümü kesinlikle yoktur. 



- C'de karakter sabitlerinin türü int'dir. Yani C'de 'A' ifadesinin türü char değil int'dir. C++ ise karakter sabitlerinin türü char türündendir.

```
#include <stdio.h>

int main()
{
	printf("%zu\n", sizeof('A'));
}
```
Yukarıdaki kod parçacığını C'de ve C++'da derlendiğimizde C'de int türü olduğu için 4 output'u görülür. C++'da görülen değer 1'dir. 
Yani özetle C++'da karakter sabitlerinin türü char türdendir.

Hatırlatma: array decay / array to pointer conversion, bir dizi ismini bir ifade içerisinde kullandığınız zaman iki istisna hariç dizi ismi dizinin ilk 
elemanının adresine dönüşür.

- String literal'leri C'de char dizi iken, C++'da const char dizidir.

C'de string literali bir ifade içinde kullanıldığında char* türüne dönüşürken, C++'da ise const char* türüne dönüşür.
 Her iki dilde de string literalini değiştirme girişimi tanımsız davranış (undefined behavior ub) olur.


Unevaluated context: Bir ifadenin karşılığında işlem kodu üretilmeyen durumlara "unevaluated context" adı verilir.

C'de array decay'e istisna olan bir durum dizi isminin sizeof operatörünün operantı olmasıdır. C'de unevaluated context sadece sizeof operatörü için geçerli iken
C++'da unevaluated context 8 tane vardır. 

Aşağıdaki kod parçacığı ile bu durum açıklanabilir:
```
int a[10] = { 1, 5, 7 };

printf("%zu\n", sizeof a); // burada array decay gerçekleşmediği için ekranda 4*10 'dan 40 değeri görülür.
printf("%zu\n", sizeof &a[0]); // Burada ise dizinin ilk elemanın size'ı olan 4 görülür.
```

Hatırlatma: C'de bir dizinin adres operatörüyle adresinin alınması durumunda elde edilen değerin türü, 10 elemanlı bir dizinin adres türüdür.
```
int a[10] = { 1, 5, 7 };
&a; // türü int (*)[10]'dur. 
```

- Aşağıdaki kod parçacığı C'de geçerli olmasına rağmen C++'da geçerli değildir.
```
    char* p = "batuhan";
```
C++'da doğrusu:
```
    const char* p = "batuhan";
```
Şeklindedir. "batuhan" bilgisi const char bir veridir. Array decay ile const char*'a dönüşür. C'de donst char*'dan char*'a implicit dönüşüm gerçekleşirken C++'da bu dönüşüm gerçekleşmez.


- Aşağıdaki kod parçacığı için;
```
char str[4]= "anil";
```
C'de geçerli ama tehlikeli bir yazım şeklidir. Tehlikeli olmasının sebebi bu yazı null terminated byte string değildir. Yani bu dizi
adresi null terminated byte string olarak kullanılırsa örneğin sonunda bir null karakter bekleyen bir fonksiyona argüman olarak gönderilirse, 
tanımsız davranış (undefined behavior ub) olur. Ancak null terminated byte string olarak kullanılma niyeti yoksa yani memset, memcpy gibi fonksiyonlarla
kullanılması planlanıyorsa herhangi bir problemle karşılaşılmaz. Ama C++'da bu durum sentaks hatasıdır.  C++'da null karakterinin de olduğu düşünüldüğü için array'in boyutu 5 olmalıdır.


- C'e hatırlatma:
```
short s1 = 5, s2 = 7;
s1 + s2; // integral promotion
```
C'de int altı türler işleme sokulduğunda int türüne dönüşüm (integral promotion) gerçekleşir.

integral promotion örneği:
```
char c = 'A';
c // türü char
+c // türü int
-c // türü int
```
C'de ve C++'da char türü ya da int altı türler işaret operatörü + veya -'nin operantı olduğunda, int'e tür dönüşümü gerçekleşir.

Hatırlatma:
```
int x = 10;
x > 5 ? 3 : 4.7;
```
Yukarıdaki ifadenin türü double olur çünkü koşul operatörünün 2. ve 3. operantları arasında yine implicit type conversion söz konusudur. 

- C'de hatırlatma olarak değer kategorisi (value category): C'de iki tane değer kategorisi vardır.
```
L value expression
R value expression
```
Bir ifadenin L value olması demek, C'de o ifadenin bellekte tutulan bir nesneye karşılık gelmesi demektir.
Bir ifadenin R value olması doğrudan bellekte kalıcı bir yeri olmayan ancak bir hesaplamaya yönelik bir ifade olması demektir.
örneğin bir değişkene ilk değer vermek için ya da bir operatör ile oluşturulan ifadenin değerinin 
hesaplanması için oluşturulan ifadelerdir.

C dili için bir ifadenin L veya R value olduğunu anlamanın bir yolu adres operatörünün operantı yapmaktır. 
Eğer derleyici bir sentaks hatası işaretler ise R value expression'dır.
Eğer derleyici bir sentaks hatası işaretlemez ise L value expreession'dır.

Bir not: x bir int değer ise +x ifadesi C ve C++ dillerinde R value expressiondur.

İşaret operatörü + son derece önemli bir operatördür. 
- Bir L value expression'u operant olarak aldığında elde ettiğiniz ifade R value expression olur.
- Eğer işaret operatörü +'nın operantı olan değişken int altı türlerden ise integral promotion olarak int türüne dönüşüm gerçekleşir.

C dilinde R value expression kategorisinde olan bazı ifadeler C++ dilinde L value expression olabiliyor.
- Örnek olarak ön ek olan ++, -- operatörleriyle oluşturulan ifadeler C dilinde R value expression iken C++ dilinde L value expression'dır.
```
x bir int değişken olarak tanımlandığı varsayılırsa;
++x; // C'de R value, C++'da L value
x = 5; // C'de R value expression iken C++'da L value olur
&(x = 5) // şeklinde derleyicinin sentaks hatası vermesi durumuna göre anlaşılabilir.
```
virgül operatöründe de aşağıdaki gibi bir farklılık söz konusudur.
```
int x = 10;
int y = 20;

(x, y) = 77; // C'de hata alınır çünkü (x, y) bir R value'dur.
// Ancak C++'da (x, y) ifadesi bir L value expression olduğu için
// virgül operatörünün ürettiği değer sağ operantın ürettiği değerdir. Bu sebeple y değişkenine 77 değeri atanmış olur.
```

C++'da value category:
- Primary value category
  - PR value (pure R value)
  - L value
  - X value (Ex-pired value)
- Combined value category
  - R value -> PR value ile X value'nın birleşimi.
  - GL value -> L value ile X value'nın birleşimi.




















































