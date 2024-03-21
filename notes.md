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
- Bir örnek: typedef ismi bir pointer türünün eş ismi olduğunda const anahtar sözcüğü her zaman top-level constluk yapar. low-level constluk olmaz.
```
#include <stdio.h>

typedef int* iptr;

int main()
{
	int x = 5;
	int y = 45;

	const iptr p = &x;
	p = &y; // sentaks hatası
	*p = 30; // geçerli
}

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


- C++'da bir ifadenin primary value categorisi sorgulanmak istenirse aşağıdaki fonksiyonel makro kullanılabilir.

```
#include <iostream>

template<typename T>
struct ValCat {
	static constexpr  const char* p = "PR value";
};

template <typename T>
struct ValCat <T&> {
	static constexpr const char* p = "L value";
};

template <typename T>
struct ValCat <T&&> {
	static constexpr const char* p = "X value";
};

#include <iostream>

#define print_val_cat(expr)    std::cout << "value category of expr '" #expr "' is: " << ValCat<decltype((expr))>::p << '\n'

int main()
{
	int x = 10;
	print_val_cat(x);
}
```


- C ve C++ dillerinde neden undefined behavior vardır:
C ve C++ derleyicileri optimizing compilers'dır. Yani kod yeniden düzenleniyor. Zaten C ve C++ dillerinin bu kadar
verimli olmasındaki temel faktör optimizing compiler olmasıdır. Derleyicinin etkin bir optimizasyon yapabilmesi için sizin kodunuzda
tanımsız davranış olmadığını temin etmeniz gerekiyor. Derleyici tarafından Undefined behavior'un olup olmadığını kontrol etmek karmaşık ve optimizasyon işlemini
uzatan bir durumdur. Siz undefined behavior'un olmadığını temin ettiğinizde bu karmaşık işlemlerden uzak bir optimizasyon yapılıyor ve bu da programınızın
performansını artırıyor.

- Unspecified behavior: Derleyicinin nasıl bir kod üreteceği konusunda herhangi bir şekilde bağlayıcılığının olmaması durumudur.
Yazılan kodda unspecified behavior olması yanlış bir durum değildir. Ancak unspecified behavior olduğunu bilmeden buna güvenerek kod yazmak ciddi
problemlere yol açabilir.
Örnek olarak:
```
    x = f1() + (f2() * 5);
``` 
Yukarıdaki kod parçacığında * operatörü, + operatöründen daha önceliklidir ama bu operant olan ifadelerin zamansal olarak daha önce ya da
daha sonra yapılacağı anlamına gelmez. Burada hangi fonksiyonun daha önce çağırılacağı unspecified behavior'dur.

Örnek bir unspecified behavior:
```
	const char* p1 = "aytun";
	const char* p2 = "aytun";

	if (p1 == p2)
		std::cout << "dogru" << std::endl;
	else
		std::cout << "yanlis" << std::endl;
```
Yukarıdaki kod parçacığında if'in doğru kısmına girer mi girmez mi konusu unspecified behavior'dur. Bunun sebebi derleyicinin nasıl bir kod optimizasyonu yapacağını
bilemiyoruz. Yani derleyici "aytun" olan const char* sabitini ikinci kez gördüğünde bu bilgi ömrü boyunca değişmeyeceği için ve hali hazırda bu bilgiyi bir
adrese atadığı için bu bilgiyi aynı adreste tutabilir. Bu durumda if'in doğru kısmına girilecektir, yani p1'in adresi ile p2'nin adresi aynıdır. 
Ancak derleyici her ihtimale karşı bu bilgiyi farklı bir adresde de tutabilir. Bu durumda else kısmına girecektir. Ayrıca aynı kodu her çalıştırdığınızda
aynı şekilde tepki alacağınızın da garantisi yoktur. Bir optimizasyonda if'in doğru kısmına girerken diğer bir optimizasyonda else kısmına girebilir. 

Ayrıca yukarıdaki örneği aşağıdaki dizide olduğuyla karıştırmamak gerekiyor. Çünkü aşağıda iki farklı const dizi tanımlanıyor. Aşağıda bir unspecified 
behavior yoktur. Aşağıdaki iki farklı const char dizi tanımlanmıştır.


```


	const char a[6] = "aytun";
	const char b[6] = "aytun";

	if (a == b)
		std::cout << "dogru" << std::endl;
	else
		std::cout << "yanlis" << std::endl;
```


- implementation defined: Derleyiciye bağlı denebilir. İmplementation defined, unspecified behavior'un bir alt kategorisidir. Farkı ise
derleyici üzerinden bu durum dökümante edilmiş olmasıdır. Derleyici bu durumda hep aynı yolu seçerek kod üretecektir.
Mesela int türünün storage ihtiyacı 2, 4, 8 byte olabilir. Bu derleyiciye bağlı ve dökümante edilmiş olmalıdır.


- C'nin standart kütüphanesi C++'ın standart kütüphanesinin bir bileşenidir. C++'da C'nin standart kütüphanelerini include ederken
başına c harfi eklenir ve .h kısmı yazılmaz.
```
#include <stdio.h> // C'de
#include <cstdio> // C++'da
```


Default initialization: Değişkene tanımlama yapılırken ilk değer vermeden yapılmasıdır. 

Eğer bir değişken statik ömürlü olarak (global değişken, statik anahtar kelimesi ile tanımlanmış veya string literalleri karşılığı ile oluşturulan char dizi)
initialize edildiğinde ilk aşama olarak derleyici zero initialization denen süreci tamamlar.

Zero initialization: 
- aritmetik türler için 0
- bool için false
- pointerlar için ise nullptr olur.

copy initialization:
```
int main() { int x = 10; }
```

- C'de olmayan C++'da olan tanımlama şekilleri:

```
int x(98); // direct init
int y{38}; // uniform, brace init
```

- Brace init'in diğer initialization şekillerinden bir farkı vardır. Narrowing conversion'a izin vermez.
```
double y = 5.6;
int x = y; // burada y sayısının ondalık kısmı direk kaybolur ve x'e 5 sayısı atanır.
```
Ama eğer initialization brace init şeklinde olursa sentaks hatası olur.
```
double y = 5.6;
int x{y}; // sentaks hatasıdır. 
```

Ayrıca brace init ile bir değişkeni initialize ettiğinizde o değer zero init olur.
```
int x; // garbage value'dur
int y{}; // zero init olduğu için y = 0 olur.
```

- C++ diziler için aşağıdaki initialization şekillerinin hepsi zero init'dir
```
int a1[4] = {0};
int a2[4] = {};
int a3[4]{}; 
```

# Referance Semantiği (references)

- C'de sadece pointer semantiği var iken C++'da pointer semantiğine alternatif olarak reference semantiği vardır.
C++'da reference semantiğine ihtiyaç duyulmasının sebebi; pointerlar C++'ın bazı araçları ile iyi bir uyum sağlamıyor.
Yani öyle araçlar var ki orada pointerın kullanılması o aracın implementasyonunu zorlaştırıyor. Dilin kuralları arasında uyum sağlanmıyor.
Bunun en başında operator overloading dediğimiz konu başlığı geliyor. Eğer sadece pointer semantiği kullanılsaydı, operatör overloading
özelliği tamamen legal bir şekilde implemente edilemezdi.

- Reference semantiği pointerlara alternatiftir ama sadece dil katmanında bir alternatifdir. Yani yazılan kod assembly formatına dönüştürüldüğünde
aslında bir fark olmadığı görülür.

- Modern C++'da reference semantiği denildiğinde 3 ayrı reference kategorisi vardır.
	- L value reference (sol taraf reference)
        - R value reference (sağ taraf reference)
        - Forwarding reference (universal reference)
  

```
int x = 10;
int& r = x; // L value reference
int&& rr = 35; // R value reference
auto&& y = 35; // forwarding/universal reference
```

### L Value Reference

- Bir L value reference ismi (identifier), bir nesnenin yerine geçiyor, yani bir reference kullanıldığında aslında o reference'ın yerine geçtiği nesne kullanılıyor.
- Reference'ların bildiriminde & declaratörü kullanılır.
```
int x = 10;
int& r = x; 
```
- Reference'lar default initialize edilemezler.
- L reference'lar ilk değerini L value expression ile almalıdır.
- Reference'ları initialize etme şekli bir değişkene değer verme şekilleriyle aynıdır.
```
int x = 10;
int& r = x;
int& r(x);
int& r{x};  
```

- Reference'lar pointer'ı da reference olarak gösterebilir:
```
int *p = nullptr;
int*& r = p;
```

- Reference olarak bir ismi tanımladığınızda artık reference demek o değişken demektir.
```
#include <iostream>

int main()
{
	int x{ 3 };
	int& r{ x };
	int y = 99;

	std::cout << "x = " << x << std::endl;

	r = 67; // burada 'nin değeri yani artık x'in değeri değişiyor ve 67 oluyor.
	std::cout << "x = " << x << std::endl;

	++r; // burada x bir artırılmış oluyor.
	std::cout << "x = " << x << std::endl;

	r = y; // !burada r artık y'yi gösteriyor gibi bir yanılgıya düşmemek gerek!!
	// r = y demek aslında x = y demek, yani x'e y'nin değeri atanmış demektir.
	std::cout << "x = " << x << std::endl;
}
```

- Bir reference'ı tanımlıyoruz ve bir nesnenin yerine geçmesini sağlıyoruz. Yani reference olarak tanımlanan ismi, tanımladığımız nesneye bağlamış oluyoruz.
Bu duruma teknik ingilizce olarak "bind" denir.

!!! reference'lar rebind edilemezler. Yani ömürleri boyunca sadece tek bir nesneyi gösterirler.

- Pointerlarda bir pointer başka bir pointer'ın adresini gösterebilir. (pointer to pointer) Ancak referance başka bir referance'ı gösteremez, eğer öyle tanımlanırsa
artık iki reference nesne si de aynı reference edilen nesneye bind edilmiş olur.

```
#include <iostream>

int main()
{
	int x = 10;
	int* p = &x;
	int** ptr = &p; // pointer to pointer

	int y = 5;
	int& r = y;
	int& rr = r;

	std::cout << y << " " << r << " " << rr << " " << std::endl;
	r = 99;
	std::cout << y << " " << r << " " << rr << " " << std::endl;
	rr = 150;
	std::cout << y << " " << r << " " << rr << " " << std::endl;

}
```

- reference'ların pointer'ı göstermesi durumuna dair örnek:
```
#include <iostream>

int main()
{
	int ival = 35;
	int* p = &ival;

	int*& rp = p; // rp reference olarak p'ye bind

	*rp = 99; // burada ival'in değeri değiştirildi.
	std::cout << ival << std::endl;

	int x = 15;
	rp = &x; // burada artık p pointer'ı ival'i değil x'i gösteriyor.

}
```

- Bir reference isim bir dizinin yerine geçebilir.
```
#include <iostream>

int main()
{
	int a[]{ 1, 3, 5, 7, 9 };
	int(*pa)[5] = &a; // diziyi gösteren pointer
	int* p = a; // pointer dizinin ilk elemanını gösterir(array-decay)

	int(&ra)[5] = a; // a dizisini gösteren ref ifade.
	
	for (int i = 0; i < 5; ++i)
		std::cout << ra[i] << " " << a[i] << " " << *(p + i) << std::endl;
}
```


- Bir diziye bağlı olan reference'ı pointer'ı initialize ederken kullanırsanız array decay yine görülür.
```
#include <iostream>

int main()
{
	int a[]{ 1, 3, 5, 7, 9 };
	int(&ra)[5] = a;

	int* p = ra; // burada array-decay uygulanır ve p pointer'ı a array'inin ilk elemanının adresini gösterir.
	
}
```

- Reference semantiğinin struct'larda kullanımı:
```
#include <iostream>

struct Data {
	int a, b, c;
};

int main()
{
	Data myData = { 3, 5, 7 };
	Data& rx = myData;
	rx.a = 10;
}
```


- Reference semantiğinde türe ilişkin not:
```
#include <iostream>


int main()
{
	int x = 10;
	int& r{ x };

	r; // r ifadesinin türü int
	r = 15; // r değişkeninin türü int&'dır

}
```

- Reference'lar iki şekilde çok sık kullanılıyor.
	- Bir nesneyi bir fonksiyone gönderirken. (call by reference)
 	- Bir fonksiyonun kendisini çağıran koda bir nesnenin kendisini göndermesi/iletmesi.

- Call by reference için pointer ve reference kullanımı:
```
#include <iostream>

void func_pointer(int* p)
{
	*p = 20;
}

void func_ref(int& r)
{
	r = 15;
}

int main()
{
	int x = 1;

	func_pointer(&x);
	std::cout << x << std::endl;

	func_ref(x); 
	std::cout << x << std::endl;
}
```

- Call by reference durumu için C ile C++ arasındaki farkı anlamak için bir örnek:
```
int main()
{
	int x = 45;
	//func(x); 
}
```
Yukarıda kod parçacığı için x'in değeri sorulursa, eğer C dili üzerinden konuşuluyorsa, x'in değeri kesinlikle değişmez. 
C'de call by reference kavramı sadece adresler ile yapılabilir. 
Ancak C++ için konuşuluyorsa x değerinin değişme olasılığı vardır. func tanımı görülmeden yorum yapılamaz.


- L value reference'a, R value expression ile ilk değer veremeyiz. L value expression olmalıdır.
```
	int& r = 10; // geçersizdir.
```

- Pointer semantiğinde olduğu gibi referance semantiğinde de referance'ın türü ile ona ilk değer verecek ifadenin türü uyumlu olmalıdır.
```
	unsigned int uval {56u};
	int& r = uval; // sentaks hatasıdır.  
```


- Reference semantiğine göre bir reference'i tanımlarken ilk değer veren ifade bir değişken ismi olmak zorunda değildir. Bir L value expression olmak zorundadır.
```
#include <iostream>

int main()
{
	int a[5]{ 1, 2, 3, 4, 5 };
	int* p = a; // array-decay
	int& r = *p; // r artık dizinin ilk elemanını her zaman gösteriyor.

	std::cout << r << std::endl;
}
```

# L value reference ve const semantiği

Reference değerler zaten ömrü boyunca sadece bir değişkeni gösterecektir. Yani pointer'lardaki top-level const semantiği otomatik
olarak zaten reference'larda geçerli oluyor. Ancak low-level const pointer karşılığı olarak const anahtar sözcüğü kullanılıyor.
```
#include <iostream>

int main()
{
	int x = 45;
	const int& r = x; // yani r üzerinden x sadece okuma işlemi yapılabilir.
	r++; // sentaks hatasıdır.
}
```

- Fonksiyonlarda kullanım şekli olarak:
```
void func(T&);  // setter-mutator
void func(const T&) //getter - accessor
```

- Ayrıca const bir nesneyi const olmayan bir reference'a tanımlamak sentaks hatasıdır.
```
#include <iostream>

int main()
{
	const int x = 10;
	int& r = x; // sentaks hatasıdır.
	const int& r = x; // doğru kullanımdır.
	
}
```


- const reference'lara, farklı türden nesnelerle ilk değer verildiğinde görüntüde yanıltabilir. Çünkü reference o nesnenin yerinde geçmez. Reference bu durumda derleyicinin oluşturduğu
geçici nesneye bind oluyor.
```
#include <iostream>

int main()
{
	int x = 10;
	const double& dr = x;

	std::cout << x << " " << dr << std::endl;

	x = 15; // x nesnesi değişirken dr reference'ı aynı kalır.
	std::cout << x << " " << dr << std::endl;
}
```

- Benzer şekilde const reference'a R value bir değer verilebilir.
```
#include <iostream>

int main()
{
	const int& r = 15; // sentaks hatası olmuyor
}
```

- Fonksiyonlar için incelediğimizde;
```
void func(T&); // sadece L value ile çağırılabilir.
void func(const T&); // R value ile de çağırılabilir.
```


# type deduction (tür çıkarımı)

run-time ile hiçbir alakası yoktur. Tamamen compile-time'a ilişkin bir senaryodur. Kodda bir bilgi belirtilmemesine rağmen derleyici, 
kullanılan context'e bakarak hangi türün kastedildiğini tanımlıyor.
- auto
- decltype
- decltype(auto)
- template


Sentaks'ı:
```
auto x = expr;
```
Yukarıdaki tanımlamada çıkarım auto kısmı için yapılır.
```
int y = 45;
auto y = 45; // iki ifade birbiriyle aynıdır. int y = 45 olur.
```


Uyarı: const bir nesne ile auto kullanıldığında const'luk düşer.
```
#include <iostream>

int main()
{
	const int cx = 5;
	auto y = cx; //y'nin türü const int değildir. int'tir.
}
```

Eğer ilk değer veren ifade bir reference değişkenin oluşturduğu ifade ise reference'lik de düşüyor.
```
#include <iostream>

int main()
{
	int x = 19;
	int& r = x;

	auto y = r; // y'nin türü int'tir.
}
```

- Dizilerde auto kullanıldığında array-decay kuralı geçerli olur.
```
#include <iostream>

int main()
{
	int a[] = { 1, 3, 5 };
	auto aa = a; // aa'nın türü int*'dır.
}
```

- Normal bir const int değişken için auto kullanıldığında const'luk düşüyor demiştik. Diziler
söz konusu olunca const'luk düşmez!
```
#include <iostream>

int main()
{
	const int y[5] = { 2, 4, 6 };

	auto x = y; // x'in türü const int* olur.
}
```

- type deduction da pointer'lar için const anahtar sözcüğü kullanıldığında;
  	- top-level const kullanıldığı ise const düşer.
  	- low-level const kullanıldığı ise const korunur.
```
#include <iostream>

int main()
{
	int x = 10;

	const int* lowp = &x;
	int* const topp = &x;
	
	auto p = lowp; // türü const int*'dır.
	auto ptr = topp; // türü int*'dır, constluk düştü.

}
```

- Fonksiyonlar için auto:
```
#include <iostream>

int foo(int);

int main()
{
	auto fp = foo;
	auto fp1 = &foo;
	int (*fp2)(int) = foo;

}
```

- reference declaratörü kullanıldığında const'luk düşmez.
```
#include <iostream>

int main()
{
	const int x = 10;
	auto& r = x; // türü const int& olur.

}
```
- Diziler için kullanım şekli:
```
#include <iostream>

int main()
{
	int a[3] = { 1, 4, 5 };
	auto& r = a; // array decay gerçekleşmez. r'nin türü int(&r)[3] olur
}
```

- const char* diziler için:
```
#include <iostream>

int main()
{
	auto x = "batuhan"; // const char* türündendir.
	auto& y = "selim"; // const char(&)[6] türünden olur.
}
```
- Fonksiyonlar için auto kullanımı:
```
#include <iostream>

int foo(int);

int main()
{
	auto f1 = foo; // int (*f1)(int) = foo ile aynıdır.

	auto f2 = &foo; // int (*f2)(int) = &foo ile aynıdır.

	auto& f3 = foo; // int (&f3)(int) = foo ile aynıdır.

}
```

Bir örnek:
```
#include <iostream>

int foo(int);

int main()
{
	auto& x = &foo;  // sentaks hatasıdır. Sebebi ise &foo ifadesinin R value expression olmasıdır.
}
```

- auto'da const kullanımı aşağıdaki gibidir:
```
const auto x = 10; // x'in türü const int olur. 
```

- auto, static anahtar sözcüğü ile de kullanılıyor.
```
#include <iostream>

int main()
{
	for (int i = 0; i < 10; ++i)
	{
		static auto x = 5; //türü static int oluyor.
		std::cout << x++ << "\n";
	}
}
```

Reference collapsing: Aslında C++ dilinin kurallarında reference to reference yoktur. Fakat öyle bağlamlar var ki reference to reference oluşturuyor.
Reference to reference oluştuğunda dilin reference collapsing denilen kuralları devreye giriyor. Aslında reference to reference olması gereken türün yerine ya 
L value reference türü ya da R value reference türü kullanılıyor. Ama R value mu L value reference olduğu aşağıdaki kurallara göre belirleniyor.
```
T&  ile &&   --- >   T&
T&& ile &    --- >   T&
T&  ile &    --- >   T&
T&& ile &&   --- >   T&& 
```

Örnek olarak;
```
#include <iostream>

int main()
{
	int x = 10;
	auto&& r1 = 20; //r1'in türü int&&
	auto&& r2 = x; //r2'nin türü int& --> reference collapsing oluştu. 
	// yukarıda r2 için auto kısmında && kullanıldı, r2'ye x ataması yaparak int& türü elde edildi. 
	//reference collapsing kurallarına göre de int& oldu.
}
```

Bir örnek:
```
#include <iostream>

using mytype = int&&;

int main()
{
	int y = 5;
	mytype&& x = 10; // burada x'in türü ref collapsing kuralına göre int&&
	mytype& z = y; // burada z'nin türü int& olur.
}
```


decltype: Bir anahtar sözcüktür. Böyle anahtar sözcüklere specifier da deniyor. Ancak decltype'a bir operatör de denebilir.

Derleyici decltype'ı bir tür bilgisi olarak görüyor. Yani ortada bir decltype kullanımı var ise burada bir tür bilgisi vardır. int, double vs gibi.
decltype ile elde edilen türü, tür kullanabileceğiniz herhangi bir yerde kullanabilirsiniz. Yani bu değişken tanımıyla sınırlı değildir. 

Yani auto ile farkı incelenirse;
- auto için bir değişken tanımlanmak zorundadır. Ancak ilk değerden hareketle tür çıkarımı yapılıyor.
- decltype için bir  değişken tanımlamanıza gerek yoktur. decltype ile elde edilen tür örneğin bir fonksiyonun parametre değişkeninin
türü, bir fonksiyonun geri dönüş değeri türü olabilir.

decltype'ın iki farklı kural seti vardır.
- decltype'ın operantının bir değişken olmasına göre,
- decltype'ın operantının bir expression olmasına göre.

ilk olarak decltype'ın operantının bir değişken olduğu kural setine göre örnekler:

```
#include <iostream>

int main()
{
	int x = 1;
	decltype(x) y; // int y demek ile aynı anlama gelir.
}
```
=======
```
#include <iostream>

int x = 1;
using mytype = decltype(x); // bu şekilde kullanılabilir sentaks hatası yoktur.

int main()
{
	//code
}
```
=======
```
#include <iostream>

int x = 1;
decltype(x) foo();

int main()
{
	//code
}
```
=======
```
#include <iostream>

int main()
{
	const int x = 1;
	decltype(x) y = 56; // y'nin türü const int olur.

}
```
=======
```
#include <iostream>

int main()
{
	int x{};
	auto& r = x;

	decltype(r); // r'nin türü int& olur.
}
```
=======
```
#include <iostream>

int main()
{
	int x{};
	const auto& r1 = x;
	decltype(r1) r2; // r2'nin türü const int& olur. 
	// ama yukarıda sentaks hatası olur çünkü r2 hem const yani salt okuma amaclı hem de ref aldığı bir değer yok!

}
```
=======
```
#include <iostream>

struct Nec { int a; };

int main()
{
	Nec mynec{};
	decltype(mynec.a) n; // burada n'nin türü int olur.
}
```

- decltype'ın bir expression formunda olduğunda, hangi türün elde edileceği, expression ifadesinin primary value kategorisine göre belirlenir.
```
	expr    -->     tür

        PR value  	T
	L value 	T&
	X value 	T&&
```
Örnekler:

```
decltype(10) x; // x'in türü int olur.
```
========
```
#include <iostream>


int main()
{
	int x = 10;
	int* ptr = &x;

	decltype(*ptr); // L value olduğu için buranın türü int& olur.
}
```
========
```
#include <iostream>


int main()
{
	int x = 10;

	decltype(x) y = 10; // x bir identifier olduğu için direk x'in türü kullanılır.
	decltype((x)) r = y; // (x) bir expression olduğu ve L value olduğu için burada tür int& olur.
}
```
========
```
#include <iostream>


int main()
{
	int x = 5;

	decltype(x++) y = 10; // x++ bir R value değerdir. tür int olur.
	decltype(++x) r = y; // ++x bir L value değerdir. tür int& olur.
}
```
=========
```
#include <iostream>

int main()
{
	int a[5]{};
	decltype(a) b; // a bir identifier olduğu için türü int[5]olur. array-decay uygulanmaz.
	decltype(a[0]) c; // burada bir expression kullanılmıştır ve L value. tür int& olur.
}
```
=========
```
#include <iostream>

int f1();
int& f2();
int&& f3();

int main()
{
	//f1() PR value
	//f2() L value
	//f3() X value

	decltype(f1()) x = 5; // int
	decltype(f2()) y = x; // int&
	decltype(f3()) z = 5; // int&&
}
```

Uyarı: decltype'da unevaluated context vardır.
```
#include <iostream>


int main()
{
	int x = 10;

	decltype(x++) a = 10;
	decltype(++x) y = a;

	std::cout << "x = " << x << "\n"; // x'in değeri 10 dur değişmez.
}
```
===========
```
#include <iostream>


int main()
{
	int* p{ nullptr };
	int y{};
	int a[10]{};

	decltype(*p) x = y; // normalde null pointer'ı dereference etmek normalde ub iken burada değildir.
	decltype(a[30]); // dizinin sınırı dışında bir değere erişmek normalde ub iken burada değildir. 
	// çünkü decltype'da unevaluated context vardır.
}
```

# Fonksiyonların Varsayılan Argüman Alması

argüman: fonksiyon çağrısında kullanılan ifadeye deniyor.
parametre: fonksiyon parametre değişkenine verilen isimdir.

default argüman: Bir fonksiyona argüman gönderilmediğinde kullanılan değerdir. Fonksiyon bildirilirken veya fonksiyon tanımlanırken belirtilmek zorundadır.

Bir fonksiyonun varsayılan argüman alması ya da birden fazla parametreye açıkca değer gönderilmemesini mümkün kılar. Varsayılan argüman tipik olarak fonksiyonun bildiriminde belirtilir.
Ama öyle durumlar vardır ki bazen fonksiyonların bildirimi ayrıca yoktur. Sadece fonksiyonun tanımı vardır. Örneğin inline function. Dolayısıyla fonksiyonun tanımında da kullanılabilir.
Ama derleyici hem fonksiyonun bildirimini hem de tanımını görüyorsa o zaman her ikisinde de varsayılan argümanın gösterilmesi bir sentaks hatasıdır. 
```
void func(int, int, int = 10);
void func2(int x, int y, int z = 5);
```
Yukarıdaki fonksiyonun anlamı 3. parametresine argüman gönderilmez ise 3. parametreye 10 değeri gönderildiği kabul edilir. 

Kural: Eğer fonksiyonun bir parametresi varsayılan argüman almışsa onun sağındaki tüm parametrelerinde varsayılan argüman alması gerekiyor. Varsayılan argümanlar son parametre
değişkenleri için geçerlidir.
```
void f1(int, int = 3, int) // sentaks hatası olur.
```
Varsayılan argüman olarak pointer da kullanılabilir:
```
void func(int* ptr = nullptr);
```

Bir örnek: 
```
#include <iostream>

int g = 20; 

void func(int x = g++);

int main()
{
	func();
	func();
	func();

	std::cout << "g = " << g << "\n";
}

void func(int x)
{
	std::cout << "x = " << x << "\n";
}
```

Başka bir modulden edinilen bildirime, varsayılan argüman eklenebilir.

aşağıda emrah.h adında bir modul olsun. 
```
void func(int, int, int);
```
aşağıda redeclaration kullanımı gösterilmiştir.
```
#include <iostream>

#include <emrah.h>

void func(int, int, int = 10); // redeclaration yapılmıştır.

int main()
{
	func(1, 5); // func(1, 5, 10) şeklinde çağırılmış olur.
}
```

Eğer bir fonksiyon bir modulde sadece son parametresi default arguman geçilmişse ve programcı bir önceki parametreyi de default arguman yapmak istiyorsa;

```
//emrah.h
void fund(int, int, int = 10);
```

```
#include <iostream>

#include <emrah.h>

void func(int, int = 20, int); // redeclaration yapılmıştır.

int main()
{
	func(1);.//func(1, 20, 10) şeklinde çağırılmış olur.
}
```

Uyarı: daha önceki parametreler varsayılan arguman olan ifadelerde yer alamaz.
```
void func(int x, int y = x); // sentaks hatasıdır.
```

Bir örnek: 
```
#define _CRT_SECURE_NO_WARNINGS

#include <iostream>
#include <ctime>

void process_date(int day = -1, int mon = -1, int year = -1)
{
	if (year == -1) {
		std::time_t timer;
		std::time(&timer);
		auto tp = std::localtime(&timer);
		year = tp->tm_year + 1900;
		if (mon == -1) {
			mon = tp->tm_mon + 1;
			if (day == -1)
				day = tp->tm_mday;
		}
	}

	std::cout << day << '/' << mon << '/' << year << "\n";
}


int main()
{
	process_date(10, 5, 1993);
	process_date(10, 5);
	process_date(10);
	process_date();
}
```


# Kapsamlandırılmış Numaralandırma (enumaration) Türleri

scoped enum / enum class

```
enum class Color {
	white, 
	gray,
	black, 
	green
};
```
İstenirse underlying type belirlenebilir.
```
enum class Color :unsigned char {
	white,
	gray,
	black,
	green
};
```
- enum class, normal enum kapsamında (scope)'unda değildir. enum class ayrı bir kapsama sahiptir. Bu sabitleri kullanabilmek için
sınıflardaki gibi scope resolution operatörü aşağıdaki gibi kullanılmalıdır.
```
#include <iostream>

enum class Color  {
	white,
	gray,
	black,
	green
};

int main() 
{
	Color myColor = Color::white;
	auto c1 = Color::gray;
}
```
- enum class'lardan aritmetik türlere örtülü(implicit) dönüşüm yoktur.
```
enum class Color  {
	white,
	gray,
	black,
	green
};

int main() 
{
	int x;
	Color c{ Color::black };
	x = c;//sentaks hatası
}
```
- C++ 20 için using enum declaration özelliği geldi.
```
#include <iostream>


enum class Color  {
	white,
	gray,
	black,
	green
};

void func()
{
    using enum Color; // Color enum class'ın tamamı using ile declare edildi.
    auto c1 = white; // geçerli
}
void func1()
{
    using enum Color::gray; // Color enum class'dan sadece gray declare edildi.
    auto c2 = green;// geçersiz.
}

```

# C++'da tür dönüştürme operatörleri

C++'da tür dönüştürme operatörleri ayrıca anahtar sözcüklerdir(keywords).
- static_cast
- const_cast
- reinterpret_cast
- dynamic_cast

static_cast: Tam sayı, gerçek sayı türleri arasındaki dönüşümleri ve enum türleriyle, tam sayı türleri arasındaki dönüşümleri static cast operatörü ile
yapılır. Farklı enum türleri arasındaki dönüşümü, void* türünden int*, double* gibi türe yapılan dönüşümde de static_cast kullanılır.

const_cast: C'de const cast'e dair bir hatırlatma:
```
	int x = 10;
	const int* ptr = &x;
	int* p = (int*)ptr; (const cast);
```
const cast; const T* türünden T* türüne veya T* türünden const T* türüne yapılan dönüşümlerdir.

reinterpret_cast: Bir nesneyi başka bir türden nesneymiş gibi kullanılan senaryolarda kullanılır. 

dynamic_cast: inheritence ile alakalıdır.

static_cast için örnek:
```
#include <iostream>

enum class Pos { off, on, hold };

int main() 
{
	int x = 10;
	int y = 3;
	Pos mypos;

	double dval = static_cast<double>(x) / y;
	int ival = static_cast<int>(dval);
	ival = static_cast<int>(mypos);
}
```

const_cast için bir örnek:
```
char* mystrchr(const char* p, int c)
{
	while (*p) {
		if (*p == c) {
			return const_cast<char*>(p);
		}
		++p;
	}
	if (*p == '\0')
		return const_cast<char*>(p);

	return nullptr;
}
```
reinterpret_cast için bir örnek:
```
	double dval = 4.56;
	char* p = reinterpret_cast<char*>(&dval);
```
====
```
const unsigned int uval{ 436 };

	int* p1 = const_cast<int*>(reinterpret_cast<const int*>(&uval));
	int* p2 = reinterpret_cast<int*>(const_cast<unsigned int*>(&uval));
```

# Function overloading (Fonksiyonun Aşırı Yüklenmesi)
- Özünde abstraction(soyutlama) yapıldığında aynı işi gerçekleştiren fonksiyonların kodları (implementasyonları) farklı olsa da aynı ismi alabilmelerine yönelik özelliktir.
Yani fonksiyonların kodları farklı ama isimleri aynıdır.

Mesela bir değeri yazıya dönüştüren n tane fonksiyonun isminin 'tostring' olması gibi. int'i yazıya dönüştüren fonksiyonun kodu ayrı, double'ı yazıya dönüştüren fonksiyonun
kodu ayrı ama bu iki fonksiyonun ismi aynıdır.

- Funcion overloading mekanizması derleme (build time) zamanına yönelik bir mekanizmadır. Run-time'a ait değildir.

static binding(early binding): Eğer fonksiyon çağrısı derleme zamanında bir fonksiyonla bağlanıyorsa programlamada buna static binding denir.

dynamic binding(late binding): Hangi fonksiyonun çağırıldığı, programın çalışma zamanında anlaşılıyorsa buna dynamic binding denir.

Funcion overload resolution: Bir fonksiyon çağrısı yapıldığında ve ortada function overloading varsa hangi fonksiyonun çağırılacağını belirleyen kurallar bütünüdür.

Function overloading oluşması için;
- İki ya da daha fazla fonksiyonun aynı isimde olması gerekli.
- Kapsamları, scope'ları aynı olmalıdır.
- function signature'ları farklı olmalıdır.

C++'da bir identifier aşağıdaki scope'lardan birine sahip olabilir.
- namespace scope
- class scope
- block scope
- function prototype scope
- function scope

Örneğin iki aynı isimli fonksiyon, biri class scope'da iken diğeri block scope'da ise overloading olma ihtimali yoktur çünkü scope'lar farklıdır.

Eğer aynı isimli fonksiyonlar farklı scope'larda ise "name hiding, name shadowing" olur. Aynı isimler kullanıldığı için birbirini gizleyebilirler.

- Function signature: Fonksiyon imzası, fonksiyonun parametre değişkenlerinin sayısı ve türü ile alakalıdır. Geri dönüş değeri function signature'a dahil değildir.

```
func(int, double);
func(double, int); // fonksiyon imzaları farklıdır.

int foo(int, int);
double func(int, int); // imzaları aynı, fonksiyon isimleri farklıdır.
```

- İki fonksiyonun isimleri ve imzaları aynı, geri dönüş değerleri farklı olarak bildirilirse bu dilin sentaksına aykırı olur. Ayrıca overloading de olmaz.
```
int foo(int);
double foo(int); // sentaks hatası


int foo(int);
double foo(int, int); // overloading olur.
//scope'lar aynı
//fonksiyon isimleri aynı
//imzaları farklı
```

- Default argument için aşağıdaki durumda
```
int foo(int);
int foo(int, int = 0); // overloading olur.
```
fonksiyonların parametre değişken sayısı farklı, dolayısıyla overloading vardır.



- Parametrelerin kendisinin const olması bir imza farklılığı olarak kabul edilmez. (adres-pointer olmadığı sürece)
```
int foo(int);
int foo(const int); // bu bir redeclaration'dur. function overloading oluşturmaz.

int foo(int*);
int foo(const int*); // const overloading olarak özel bir ismi vardır.
```
Ancak const overloading yalnızca low-level const için geçerlidir.
```
void f(double* const p);
void f(double* p); // function redeclaration olur. Function overloading olmaz.
```

- Bir türe ait onu temsil eden bir eş isim oluşturmak (type alias) kesinlikle farklı bir tür anlamına gelmez.
```
typedef double flt_type;

void f(double);
void f(flt_type); // function overloading değildir. Redeclaration olur.
```

- char, signed char ve unsigned char türleri distinct(ayrı) olarak derleyici tarafından değerlendirilir.
```
void f(char);
void f(signed char);
void f(unsigned char); // burada 3 tane overloading vardır.
```

- pointer türleri farklı tür olarak değerlendirilir.
```
void f(int*);
void f(int**);
void f(int***); // 3 tane overload vardır.
```
===
```
void f(int&);
void f(int&&); // overloading olur.
```
===
```
#include <iostream>
#include <cstdint>

void f(std::int32_t); 
void f(int); // implementation define'dır
```
===
```
#include <iostream>
#include <cstdint>

void f(std::int32_t); 
void f(std::int16_t); // overloading olur.
```
===
```
void f(int);
void f(int*); // overload olur.
```
===
```
void f(int);
void f(int&); // overload olur.
```

Bir fonksiyonun bildiriminde dizi notasyonu ([]) kullanılırsa, derleyici; fonksiyonu parametresi 
dizi olmayacağı için burda array_decay uygular ve fonksiyon parametresi pointer demektir.
```
void foo(int p[]);
void foo(int p[20]);
void foo(int* p); // parametrelerin hepsi int* türündendir.
// redeclaration olur.
```

===
```
int(int) -> function type
int (*)(int) -> function pointer type 
```

- Fonksiyonların geri dönüş değeri ve parametre türü dizi ve fonksiyon türü olamaz. Dizi veya fonksiyon türü yapıldığında pointer haline dönüştürülür.
```
void foo(int(int));
void foo(int(*)(int)); // redeclaration olur
// derleyici function type'ı decay ederek function pointer olarak görür.
```

```
void foo(int (*)[5]);
void foo(int (*)[6]); // overloading vardır. 
```

# Function Overload Resolution

Overload resolution, derleyici tarafından 3 kademeli bir şekilde ele alınıyor.
- Birinci aşamada derleyici fonksiyon çağrısının yapıldığı noktada fonksiyona gönderilen argüman ya da argümanlara bakmaksızın bu noktada visible
olan bütün fonksiyonları kayda alır. Bu fonksiyonlara candidate function denir.
- İkinci aşamada derleyici aday fonksiyonların her biri için fonksiyon çağrısındaki argümanlarla çağırılması legal olur muydu değerlendirilmesi yapılıyor.
Legal olan fonksiyonlara "viable function" denir.

Fonksiyon çağrısındaki argüman sayısı ile fonksiyonun parametre sayısı arasında uyumsuzluk varsa (variadic fonksiyonlar ve varsayılan argüman mekanizması hariç)
viable olma ihtimali yoktur.

Bunun dışında fonksiyon çağırısında kullanılan argümandan, ilgili parametre değişkenine dilin kurallarınca izin verilen bir conversion olması gerekir. (implicit)

- Örneklerle legal olan, olmayan tür dönüşümlerini function call üzerinden hatırlayalım.
```
#include <iostream>

void func(double*);

int main() 
{
	func(2); // viable değil
}
```
===
```
#include <iostream>

void func(double*);

int main() 
{
	func(0); // viable olur. Çünkü null pointer to conversion vardır.
}

```
===
```
#include <iostream>

void func(double*);

int main() 
{
	func(nullptr);// nullptr_t türünden pointer türlere implicit dönüşüm vardır. 
}
```
====
```
#include <iostream>

void func(int);

int main() 
{
	func(nullptr);//nullptr_t türünden tam sayı türlerine implicit type conversion yoktur. 
}
```

===
```
#include <iostream>

void func(bool);

int main() 
{
	int x{};
	func(nullptr); // nullptr_t türünden bool türüne dönüşüm yoktur. 
	func(&x); // unutulmamalıdır ki adres türlerinden bool türüne implicit dönüşüm vardır.
}
```
===
```
#include <iostream>

void func(void*);

int main() 
{
	int x{};
	double f{};

	func(&x); // geçerli
	func(&f); // geçerlidir. Pointer türlerden void* türüne implicit dönüşüm var.
}
```
===
- Önemli bir not: pointer türlerden void* türüne implicit dönüşüm vardır ancak void* türünden pointer türlere örtülü dönüşüm yoktur.
```
T* -> void* ---------- legal
void* -> T* ---------- illegal
```
===
```
#include <iostream>

void func(int*);

int main() 
{
	int x{};
	double f{};
	void* vp{};

	func(&x); // viable olur.
	func(&f); // geçerli değil
	func(vp); // void* türünden pointer türlerine dönüşüm yoktur. (c'de vardı malloc fonksiyonu hatırlanmalı)
}
```
===
```
#include <iostream>

void f1(int*);
void f2(const int*);

int main() 
{
	const int x = 10;
	int y = 20;
	f1(&x); // const int* dan int* a implicit dönüşüm yoktur.
	f2(&y); // int* dan const int* a implicit dönüşüm vardır.
}
```
===
```
#include <iostream>

void func(char*);

int main() 
{
	func("const char*"); // const char* dan char* a dönüşüm geçersizdir.
}
```

Aritmetik türlerden enum türlerine dönüşüm geçersizdir.
```
#include <iostream>

enum pos { on, off, hold };
enum class color { yellow, dark_blue };

void f(pos);
void g(color);

int main() 
{
	f(1); //geçersizdir
	g(1); //geçersizdir
	f(color::yellow); //geçersizdir
	g(off); //geçersizdir
}
```
enum türlerden aritmetik türlere implicit dönüşüm geçerli iken enum class türlerinden aritmetik türlere dönüşüm geçerli değildir.
```
#include <iostream>

enum pos { on, off, hold };
enum class color { yellow, dark_blue };

void f(int);

int main() 
{
	f(off); // geçerlidir. 
	f(color::yellow); // geçersizdir
}
```

===
```
#include <iostream>

void f1(int*);
void f2(const int*);
void f3(void*);
void f4(bool); // pointer türlerden bool türüne dönüşüm vardır (nullptr_t türü hariç)

int main() 
{
	int x = 5;

	f1(&x); // legal
	f2(&x); // legal
	f3(&x); // legal
	f4(&x); // legal
}
```


int*& türüne sadece L value atama yapılabilir. &x ifadesi PR value bir ifadedir.
```
#include <iostream>

void f(int*&);

int main() 
{
	int x = 10;
	f(&x); //geçersizdir.
}
```

Birden fazla overload olduğunda bu isimle yapılan bir çağrının geçerli olma garantisi yoktur. İki nedenle yapılan çağrı geçersiz olabilir.
- no match (overload olan fonksiyonların viable olmama durumu)
- ambiguity (overload olan fonksiyonların viable ve sentaks olarak birbirine eşit olduğu için belirsizlik oluşması)

no match için bir örnek:
```
#include <iostream>

void f(int*);
void f(int, int);
void f(int);
void f(double);

int main() 
{
	double d{};
	f(); // no match çünkü fonksiyon parametresi olmayan bir fonksiyon yoktur.
	f(&d); // no match çünkü double* türünden parametresi olan e legal olarak dönüşüm yapılabilecek fonksiyon yoktur.

}
```

ambiguity durumu için bir örnek:
```
#include <iostream>

void f(int);
void f(double);

int main() 
{
	f(2u); // ambiguity olur çünkü iki fonksiyon parametresine de implicit dönüşüm legaldir.
}
```


İki ya da daha fazla viable fonksiyon olması durumunda derleyici ya bu fonksiyonlardan birini seçer, seçilen fonksiyona best viable (best match) denir. 
Ya da bu fonksiyonlardan biri diğerinden daha iyi bir seçim yapılamadığı için ambiguity hatası oluşur.

Argümandan parametre değişkenine aktarım legal olduğuna göre uygun bir dönüşüm vardır. Dilin kuralları argümandan parametre değişkenine yapılan bu legal dönüşümü 
kategorize ediyor. Bu kategorileri birbirine göre üstün ya da daha az üstün kılıyor.

- Üstünlüğü en az dönüşüm 'variadic conversion' dır.
```
#include <iostream>

void func(int, ...);

int main() 
{
	func(1, 1.2); // burada ikinci parametre olan değer 1.2'dir ve variadic conversion oluşur.
}
```
Yani derleyicinin compile time'da variadic parametreye gönderilen argümanın türünün ne olduğunu kontrol etme yükümlülüğü yoktur. Hangi değer gönderilirse gönderilsin
doğru olur denemez ancak legal olur. Bu dönüşüme variadic conversion denir.


- Öncelik sıralamasına göre variadic conversion'un bir üstünde 'user-defined conversion yer alır.

User-defined conversion: Dilin kurallarına göre bir  türden diğer bir türe dönüşüm yoktur. Örneğin struct data bir class türü ise
int türünden struct data türüne dönüşüm yoktur. Ya da farklı sınıflar arasında tür dönüşümü yoktur. Ama programcı uygun bir fonksiyon bildirdiğinde dilin kurallarına göre
derleyici o fonksiyonu çağırarak bir dönüşüm gerçekleştiriyor. Yani normalde olmayan bir tür dönüşümü programcının bildirdiği bir fonksiyon sayesinde legal hale geliyor. Eğer
dönüşüm bu şekilde ise normalde sentaks hatası iken artık programcı olarak bir fonksiyon bildirildiği için dilin kuralları gereği o fonksiyona çağrı yapılarak derleyici bu dönüşümü gerçekleştirebildiği
için o dönüşüm var ise böyle dönüşümlere user-defined type conversion denir. 

- Öncelik sıralamasının bir kademe üzerinde 'standard conversion' yer alır. Yani dilin kurallarına göre legal olan dönüşümlerdir. (int'den double'a gibi)

Peki birden fazla standard conversion olan viable fonksiyon olursa; derleyici açısından 3 alt kategoride değerlendirilir.
- exact match (tam uyum)
- promotion (integral promotion veya float to double promotion)
- only conversion
 
```
#include <iostream>

void f(long double);
void f(char);

int main() 
{
	f(3.4); // ambiguous call
}
```

Exact match durumu olabilmesi için;
- argüman ile parametre türünün aynı olması
- T* türünden const T* türüne dönüşüm olması
- Eğer conversion array decay veya fonksiyon decay oluyorsa

```
void f(int*);

int main() 
{
	int a[] = { 3, 5, 7 };
	f(a); // a'nın türü array decay'den dolayı int* olarak fonksiyona gönderilir.
}
```
===
```
void f(int (*)(int));
int bar(int);

int main() 
{
	f(bar); // function to pointer conversion. 
	//decay ile fonsiyonun ismi fonksiyonun adresine dönüştürülmüş olur.
	// bar ismi int(int) iken decay ile int(*)(int) olur.
}
```

promotion: 
- integral promotion; int altı türlerin ifade içerisinde kullanılınca int'e yükseltilmesi.
- float to double promotion(floating-point promotion)

```
#include <iostream>

void f(double);
void f(char);

int main() 
{
	f(1.5f);//floating-point promotion
}
```
===
```
#include <iostream>

void f(int);
void f(double);
void f(long);

int main() 
{
	f(3.4); // exact match for f(double);
}
```
===
```
#include <iostream>

void f(int);
void f(double);
void f(long);

int main() 
{
	f(12u); // ambiguity olur. 3'ü de only conversion
}
```
===
```
#include <iostream>

void f(int);
void f(double);
void f(long);

int main() 
{
	f(true); //integral promotion. bool to int
}
```
===
```
#include <iostream>

void f(int);
void f(double);
void f(long);

int main() 
{
	f(2.3L);// long double'dır ve hepsine only conversion olur. Yani ambiguity.
}
```
===
```
#include <iostream>

void f(int);
void f(double);
void f(long);

int main() 
{
	f('A');// integral promotion olur. f(int) çağırılır.
}
```

Özel durumlar:

const overloading: 
```
#include <iostream>

void func(int*);
void func(const int*);

int main() 
{
	int x = 5;
	const int y = 15;
	f(&x); //func(int*) çağırılır.
	f(&y);  // func(const int*) çağırılır.
}
```

Default argument:
```
#include <iostream>

void func(int x, int y = 0);
void func(int x);

int main() 
{
	func(12); // ambiguity olur.
}
```
===
```
#include <iostream>

void func(int& x);
void func(int x);

int main() 
{
	int ival{};
	func(ival); // ambiguity
	func(10); // 10 bir R value olduğu için int x olan fonksiyon çağırılır
				// R value expression int& türü ile uyumsuzdur.
}
```
===
```
#include <iostream>

void func(const int& x);
void func(int x);

int main() 
{
	int ival{};
	func(10); // ambiguity
	// const int& türüne R value değer atanabiliyor. 
}
```

nullptr'ın C++ diline eklenmesinin sebeplerinden birini açıklayabilen bir örnek:
```
#include <iostream>

void func(double*)
void func(int);

int main() 
{
	func(0); // func(int) için exact match olur.
	func(nullptr); // func(double*) için exact match olur.
}
```

nullptr'ın türü nullptr_t'dir ve bu türden sadece pointer türlerine dönüşüm olur.
```
#include <iostream>

void func(double*)
void func(int*);

int main() 
{
	func(nullptr); //ambiguity olur.
}
```



- Burada bir istisna vardır. bool - void* overloadında nesne adresiyle çağrı yapıldığında aslında her ikisi de viable ve her ikisi  de only conversion olmasına rağmen burada
void*'a dönüşüm olur.
```
#include <iostream>

void func(bool);
void func(void*);

int main() 
{
	int x{};
	func(&x); //ambiguity yoktur. func(void*) çağırılır.
}
```
===
```
#include <iostream>

void func(int&); //viable değil
void func(int&&); //viable

int main() 
{
	func(10); //R value olduğu için func(int&&) çağırılır.
}
```
===
```
#include <iostream>

void func(int&); //viable 
void func(int&&); //viable değil

int main() 
{
	int x{};
	func(x); //func(int&) çağırılır.
}
```
===
```
#include <iostream>

void func(const int&); //viable ama çağırılmaz
void func(int&&); // viable ve çağırılır

int main() 
{
	func(10); // Burada exact match func(int&&) ile sağlanır.
	 // ancak unutulmamalıdır ki func(const int&) ile de only conversion durumu sağlanır.
	//ambiguity olmaz!
}

```
===
```
#include <iostream>

void func(int&);
void func(const int&);
void func(int&&);

int main() 
{
	int x = 10;
	const int cx{ 45 };

	func(10); // exact match den dolayı func(int&&) seçilir
	func(x); // exact match den dolayı func(int&) seçilir. ama func(const int&) de viabledır.
	func(cx); //exact match den dolayı func(const int&) seçilir. 
	//const overloading.
}

```
===
```
void bar(int& x)
{
	std::cout << "3 ";
}
void bar(int&& x)
{
	std::cout << "4 ";
}
void func(int& x)
{
	std::cout << "1 ";
	bar(x);
}
void func(int&& x)
{
	std::cout << "2 ";
	bar(x);
}

int main() 
{
	func(10); //ekran çıktısı "2 3" olur.
}

```

- Önemli bir hatırlatma: tür eş ismi bir pointer'a karşılık geliyorsa ve bu tür eş ismi const ile birlikte kullanılıyorsa
ifade her zaman top-level const olur.
```
#include <iostream>

typedef int* iptr;

int main() 
{
	int x = 10;
	int y = 20;

	const iptr p = &x; // p'nin türü int* const olur.
	p = &y;// p top-level olduğu için geçersiz.
	*p = 56; // p low-level const olmadığı için geçerlidir.
}

```

Aşağıdaki örnekte int türünden bir x değerinin adresine bir referans bağlanmak istenirse üç farklı çözüm yolu gösterilmiştir.
```
#include <iostream>

typedef int* iptr;

int main() 
{
	int x = 10;
	
	int*&& r1 = &x;
	int* const& r2 = &x;
	const iptr& r3 = &x;
}

```




Eğer fonksiyon overloading olan fonksiyonların birden daha fazla parametresi varsa;
- en az bir parametre ile diğer fonksiyonlara üstün gelmeli ve diğer parametrelerde de daha az üstün olduğu bir durum olmamalı(aynı olabilir).
```
#include <iostream>

void f(int, double, long); //1.function
void f(char, int, double); //2. function
void f(long, unsigned int, float); //3. function

int main() 
{
	f(12, 4L, 1); // 1. fonksiyon çağırılır.
	f(2.3, true, 12); // 2.fonksiyon çağırılır. integral promotion
	f(34L, 3.5L, 12); // 3. fonksiyon çağırılır. 
}

```  


Bir çok C++ projesinde C kütüphaneleri de kullanılıyor. Yani C dilinin kurallarına göre yazılmış ve C derleyicisi tarafından derlenmiş fonksiyonları C++ kodundan çağırmak çok sık karşılaşılan bir durum.

Bir örnek yaparak bu durumu açıklayalım.

cnec.h isimli bir baslık dosyası 
```
int func(int);
```

cnec.c isimli kaynak dosya.
```
#include "cnec.h"

int func(int x)
{
	return x * x + 1;
}
```

cpp kaynak dosyası olarak da main.cpp dosyasında bu fonksiyon kullanılsın.

main.cpp
```
#include <iostream>
#include "cnec.h"

int main()
{
	auto x = func(20);

	std::cout << "x = " << x << "\n";
}
```

Derlediğimizde bir hata görmeyiz ama build ettiğimizde linker hatası ile karşılaşırız.

Hatanın nedeni: Hem C hem C++ için bir fonksiyon çağrısı yapıldığında inline expansion(inline function) değilse yani derleyici bu kodun kaynak kodunu zaten görmüyorsa,
derleyici programın akışının fonksiyona geçmesini sağlayan fonksiyona giriş kodlarını ve fonksiyonun çalışması bittikten sonra programın akışının tekrar kaldığı yere dönmesini sağlayan
fonksiyondan çıkış kodlarını üretiyor. Derleyici fonksiyon inline değilse, fonksiyonun kodunu bilmiyor, sadece bildirimine göre işlem yapıyor. Çağıran fonksiyonun objesiyle(derlenmiş haliyle)
çağırılan fonksiyonun objesini birleştirmek linker'ın görevidir. bağlayıcı program link aşamasında yapılır. Derleyiciler linkerın fonksiyon çağrısındaki fonksiyonun objesiyle, bu çağıran kodun objesini 
birleştirebilmesi için derleyiciler obje koda bir referans yazarlar linker'a yönelik, yani linker bu referans ile bağlama işlemini yapar. Linker ile compiler arasında bu isimlendirmenin ne şekilde 
yapılacağı konusunda bir notasyon vardır. Derleyiciler bir nevi fonksiyonun ismini decore ederek referans oluşturuyorlar.
- decorated / name mangling

Derleyicilerin linker'a ithafen obje koda yazdığı bu isimlere external reference deniyor. Problem bu noktada başlıyor. C derleyicilerinin linker'a hitaben yazdığı external referece olarak
kullanılacak olan ismin decorate edilmesi ile C++ derleyicilerinin linker'a hitaben oluşturduğu ismin decore edilmesi arasında ciddi bir farklılık vardır. Farklılığın nedeni; C'de function overloading 
olmadığı için external fonksiyonlar aynı isimli bir tane olabileceği için C derleyicileri linker'a hitaben bu ismi oluştururken sadece fonksiyonun isminden faydalanıyorlar. Ancak C++'da 
function overloading olduğu için aynı isimli fonksiyonları ayırt etmek için fonksiyonların parametrelerine dair de bir notasyon giriyor. 

Yukarıdaki örnekdeki problem ise C++ derleyicisi çağırılan fonksiyonun C'de derlenmiş bir fonksiyon olduğunu bilmediği için linker'a yazdığı ismi C tarzı değil C++ tarzında decore etti. Fakat 
sıra linker'a geldiğinde linker bu fonksiyon için decore edilmiş ismi aradı ve bulamadı. Çünkü linker C++'a göre decore edilmiş bir isim arıyor. Doğal olarak C'ye göre decore edilmiş bir 
ismi tanıyamıyor. 

Bu problemin çözümü için derleyiciye bu fonksiyonun bir C fonksiyonu olduğunu bildirmemiz gerek ve derleyici bu fonksiyona çağrı yapıldığında C'ye göre decore edebilsin. Derleyiciye
bu bildirmeyi extern 'C' bildirimi ile yapılabilir. Eğer fonksiyon bildiriminin başında (header dosyaya) extern "C" eklerseniz C++ derleyicisi bu bildirimi gördüğünde fonksiyonun artık C'de derlenmiş bir fonksiyon
olduğunu anlar. Ancak unutulmamalıdır ki extern "C", C'de geçerli olmaz. Bu sebeple bir başlık dosyası hem C'de hem de C++'da derlenecek ise conditional compiling kullanılarak yapılabilir.

predefined symbolic constants
```
__cplusplus makrosu C++ için bir predefined makrodur. Ancak C için değildir.
```

Dolayısıyla cnec.h dosyasını aşağıdaki gibi

```
#ifdef __cplusplus
	extern "C"
#endif

int func(int);
```
Olarak veya çoklu fonksiyon bildirimleri için;
```
#ifdef __cplusplus
	extern "C" {
#endif

	int func(int);
	int func2(int);

#ifdef __cplusplus
}
#endif

```


# ODR (One Definition Rule)

ODR bir C++ acronym'idir. Yazılımsal varlıkların (fonksiyon, değişken, template, sınıf gibi) birden fazla bildirimi olabilir fakat
tüm proje içinde bir tane tanımı olmak zorundadır. Eğer bir yazılımsal varlığın tanımını birden fazla kaynak dosyada oluşturursanız 
ill-formed olur. Ayrıca ill-formed yapı no diognostic required'dır. Yani derleyici bir diognostic vermek zorunda değildir. Çünkü 
derleyicinin çalışma birimi kaynak dosyadır. Ama aynı kaynak dosyada bir varlığın birden fazla tanımı yapılırsa derleyici sentaks hatası verir.

ODR'ı ne şekilde ihlal ettiğinize bağlı olarak ve sizin kullandığınız linker programının ne olduğuna ve özelliklerine bağlı olarak en iyi ihtimal ile link 
zamanında hata alırsınız. 

Bir C++ programının ill-formed olmaması için ODR'ı ihlal etmemesi gerekiyor. 

Bir başlık dosyası olsun.

hakan.h
```
int x = 10;
```

Bu kaynak dosya eğer birden fazla kaynak dosya tarafından include edilirse ODR ihlal edilmiş olur. Çünkü
her include'da bu tanım tekrar yapılmış oluyor.

Aynı durum fonksiyonlar için de geçerli. Eğer siz bir fonksiyonu olduğu gibi hakan.h'e de tanımlayıp, 
birden fazla kaynak dosyada hakan.h'yi birden fazla kaynak dosyada include ederseniz, ODR ihlal edilmiş olur.

Ancak siz bu fonksiyonu veya değişkeni static anahtar kelimesi ile tanımlarsanız, o zaman ODR ihlal edilmiş olmaz. 
Unutulmamalıdır ki bu durum external linkage'da değildir. Yani dolayısıyla static anahtar sözcüğünden dolayı 
her kaynak dosyada ayrı bir varlık oluşturulur.

Ayrıca const anahtar sözcüğü de internal linkage oluşturur. Yani ODR ihlal edilmez.

hakan.h
```
static void func()
{
	//code
}
static  int x = 10; // ODR ihlal edilmez.
const int y = 20; // ODR ihlal edilmez.
```


- C++'da bazı varlıkların birden fazla kaynak dosyada tanımlarının bulunması ODR'ı ihlal etmez.

! Ancak token by token tanımlarının aynı olması gerekir. Yani implementasyonları arasında bir farklılık olmamalı.

Yani bu tanıma göre bu varlıkların tanımı başlık dosyalarında yer alabilir, kullanılabilir ve kullanılıyor.

- class definition
- inline function
- inline variable definition
- constexpr function
- constexpr variable
- class templates
- function templates

Özetle bir header file'a ODR'ı ihlal edebilecek hiç bir tanım konulmamalıdır.


inline expansion: Derleyicilerin en sık kullandığı bir optimizasyon tekniğidir. Bir compiler optimizasyonudur.

not: inline fonksiyonlarda inline anahtar sözcüğü kullanılıyor diye derleyici inline expansion yapmak zorunda değildir.

inline function: Bir fonksiyon inline anahtar sözcüğü ile tanımlanırsa ODR ihlal edilmeyecek anlamına gelir. Yani bu fonksiyonun tanımı
birden fazla kaynak dosyada token by token aynı yapılırsa ODR ihlal edilmez. Bu tanıma göre de bir inline fonksiyonun tanımı başlık dosyasına konulabilir.

İnline fonksiyonların kullanılmasının en önemli nedenlerinden biri derleyiciye inline expansion olanağı sağalamaktır, çünkü 
ancak bu şekilde external bir fonksiyonun tanımının derleyicinin görme şansı vardır. 

Header only library: Sadece başlık dosyası olan yani o başlık dosyasına eşlik eden bir cpp kaynak dosyası yoktur. 

- inline yerine static anahtar kelimesi kullanıldığında internal linkage olacağı için başlık dosyası her çağırıldığında bu fonksiyonlar farklı adreslerde tutulur, çünkü
farklı varlıklardır.

Not: Yapılan tanımlanın bu modülden hizmet alan programcı tarafından görülmesi istenmiyorsa inline fonksiyon kullanılamaz. Çünkü inline fonksiyon tanımları header file'larda
yapılır ve header file'lar programcılar ile paylaşılmak zorundadır.

incomplete type: Derleyici o türden haberdardır ama o türün tüm bilgilerini bilmiyordur. Yani o türün bildirimini biliyor ama definition'ununu bilmiyordur. 
```
class Neco;

int main()
{
	//Neco burada incomplete type olur.
}
```
complete type: O türün tüm bilgilerinin derleyici tarafından bilinmesi demektir. 

Yani bir türün kullanıldığı kodlar söz konusu olduğunda bazı kodlar için türün incomplete type olması o kodun derlenmesi için yeterlidir. Ama bazı kodlar açısından 
bakıldığında da türün complete type olması gerekiyor.

- incomplete type örnekleri:
```
struct Neco;

Neco f1(Neco);
Neco* f2(Neco&);

typedef Neco* Necoptr;
using Necoref = Neco&;

extern Neco Necox;

struct X {
	Neco* m_ptr;
};
```

- İncomplete type bir tür ile nesne oluşturulamaz!
```
#include <iostream>

struct Nec;

int main()
{
	Nec mynec; // hata
}
```

Bir örnek:
```
#include <iostream>

struct Nec;

Nec* foo();

int main()
{
	Nec* p = foo(); // hata olmaz
	auto x = *p; // hata olur.
}	
```

- struct tanımlarında incomplete type bir türü pointer veri elemanı olarak kullanılabilir ancak veri elemanı olarak kullanılamaz.
```
struct Nec;

struct Data {
	Nec* m_ptr;// hata değildir 
	Nec x; //incomplete type hata
};
```


Uyarı: Bir modül içerisinde tanımlanmış bir tür kaynak kodda kullanıldığı anda başlık dosyası include edilmemelidir.
Eğer incomplete type olarak kullanılabiliyorsa forward declaration yapılır. Yani sadece kullanılacak olan türün bildirimi yapılır.

- C++'da sınıfın içinde bildirilen araçlara sınıfın üye fonksiyonları deniyor. "member function"

Eğer bir member function'ı, class definition içerisinde tanımlarsanız inline anahtar sözcüğü kullanılmasa dahi bu fonksiyon inline kabul edilir.
Dolayısıyla bir fonksiyonu inline fonksiyon yapmanın başka bir yolu bir sınıfın üye fonksiyonu olarak tanımlamaktır. 

inline variables: Herhangi bir başlık dosyasında inline anahtar sözcüğü ile tanımlanan değişkenler de ODR'ı ihlal etmez.


const anahtar sözcüğü ile tanımlanan bir nesneye constant expression ile ilk değer verilirse değişkenin kendisinin oluşturduğu ifade de bir constant expression olur. 
Yani dizi boyutu gibi constant expression gereken yerlerde kullanılabilir. 
```
	const int x = 10;
	int a[x]{}; // geçerlidir.
```

const bir ifadeye ilk değer verirken değişken bir ifade kullanılabilir ama değer atanan nesne, constant expression oluşturmaz. 
```
#include <iostream>

int foo();

int main()
{
	const int x = foo(); // değişken bir ifadeyle const bir değişkene ilk değer verildi ama sentaks hatası olmaz.
	int a[x]{}; // sentaks hatası olur.
}	
```

constexpr anahtar sözcüğüyle bir nesne tanımlandığında bu nesneye constant expression ile ilk değer verme zorunluluğu vardır.
```
#include <iostream>

int foo();

int main()
{
	const int x = foo();  // sentaks hatası değildir
	constexpr int y = foo(); // sentaks hatası olur.
}	
```

Uyarı: constexpr bir tür değildir. Tür yine const olur. 
```
#include <iostream>

int main()
{
	const int x = 10;
	constexpr int y = 20;

	decltype(x) a = 22; // a'nın türü const int
	decltype(y) b = 25; // b'nin türü de const int olur.
}	
```

Uyarı: pointerlar için constexpr anahtar sözcüğü nesneye constluk verir yani top-level const olur.
```
#include <iostream>

int g = 10;
constexpr int* p = &g; 

int main()
{
	decltype(p) ptr = nullptr; // ptr'ın türü int* const olur.
}	
```

Aynı zamanda low level const'da kullanılmak istenirse;
```
#include <iostream>

int g = 10;
constexpr const int* p = &g;

int main()
{
	decltype(p) ptr = nullptr; // ptr'nin türü const int* const olur.
}	
```

Not: Derleyici const ve constexpr nesneler için yer ayırmak zorunda değildir. Optimizasyon sırasında direk constant expression olan sabiti kullanabilir. Ama o nesnenin
adresi bir yerde kullanılırsa o zaman o nesne için adresleme yapılmak zorundadır.

constexpr function: Belirli koşullar sağlandığında geri dönüş değerinin derleme zamanında elde edilebilen fonksiyonlardır. Run-time'da değil.
- constexpr function'un geri dönüş değeri türü void olamaz.
- fonksiyon içerisinde static anahtar sözcüğü ile nesne tanımlanamaz.

Yani geri dönüş değeri türü, parametre türleri ve yerel değişken türleri "literal type" olmalıdır.

constexpr fonksiyonun parametreleri const expression olmak zorunda değildir. Değişken ifadeler de gönderilebilir ancak bu durumda geri dönüş değeri run-time'da elde edilebilir.
Yani constexpr fonksiyonların geri dönüş değeri derleme zamanında elde edilme garantisi olan fonksiyonlar değildir. Tüm parametrelere gönderilen argümanlar sabit ifadesi olduğunda derleme 
zamanında geri dönüş değeri elde edilebilir. 

```
#include <iostream>

constexpr int sum_square(int a, int b)
{
	return a * a + b * b;
}

int main()
{
	int a[sum_square(10, 20)]{};// geçerlidir.

	constexpr auto val = sum_square(10, 20);

}	
```

Not: constexpr fonksiyonlar aynı zamanda implicit bir şekilde inline fonksiyonlardır ve başlık dosyasında kullanılmaları ODR'ı ihlal etmez. 




# Classess (sınıflar)

- C'de struct, union ve enum bir user-defined type'dı.
- C++'da class ile de user-defined type tür oluşturabiliyor.
- C'de kullanılan struct bir sınıf değilken C++'da kullanılan struct'lar artık bir sınıf olarak değerlendiriliyor.

Class, C++'da data abstraction konusundaki temel araçtır. Problem veya çözüm domain'indeki bir varlığın yazılımsal olarak temsilidir.

class declaration - forward declaration
```
class Nec; // class bildirimi
```

class definition:
```
class Myclass {
	//class member	
};
//Yukarıda Myclass bir class tag'dir.
```

class member 3 kategoriden oluşabilir.
- data member -> static data member / non-static data member
- member function -> static member function / non-static member function
- type member / member type / nested type


Derleyici class tanımı gördüğünde bir storage allocation'a neden olmaz. class definition sadece tür hakkında bilgi verir. Bu türden bir nesnenin oluşturulması
durumunda o nesne için yer ayrılır.

Sınıfın static elemanları olabilir ancak bir sınıf static anahtar sözcüğü ile tanımlanamaz.


Sınıflar erişim kontrolüne sahiptir. "access kontrol"

C++'da erişiminize izin verilmeyen bir isim kullanıldığında o isim aranır, bulunur ama derleyici sizin kullanımıza kapalı olduğunu görünce sentaks hatası olarak değerlendirilir.


Bir sınıfın elemanı üzerinde kimlerin kullanma hakkının olduğunu belirleyen 3 kategori vardır. (access specifiers)
- public
- private
- protected

C++'de access specifiers'lar anahtar sözcüklerdir.

public: sınıfın public ögeleri herkese açık ögelerdir. Yani sınıfın sadece kendisi değil client'ların da kullanmaya yetkisi vardır.

private: Sadece sınıfın kendi kodlarına açık ama dışarıdan kullanılması yasak olan isimlerin tanıtıldığı bölümdür. Sadece sınıfın kendi kodları kullanabilir. 

protected: inheritence (kalıtım/miras) ile alakalıdır.

Eğer sınıf tanımında access specifiers kullanılmaz ise default olarak private kabul edilir. Struct anahtar kelimesiyle sınıf tanımlandığında default olarak member'lar public olur.
```
class Myclass {
	int a, b; // private olur
};

struct Myclass {
	int a, b; // public olur
};
```

Sınıfların içerisinde ne kadar fazla non-static veri elemanı varsa sınıf nesnelerinin storage ihtiyacı o denli artar(sizeof).

Bir sınıf türünden nesneye verilen isim "object, instance" denir.
```
#include <iostream>

class Myclass {
	int x, y;
};

int main()
{
	Myclass m1; // instance (object)
}
```

Aynı sınıfın instance(object) leri aynı tanıma uyarlar, belirli özellikleri farklı ama aynı tanıma sahiptir. 


class scope:
- member selection (dot operator) "." 
- arrow operator "->"
- scope resolution operator "::"

Yukarıdaki operatörlerin sağındaki isim, class'ın tanımı içinde aranabilir. 

Bir isim kullanıldığında derleyici, aşağıdaki sıralama ile arama yapılır.

- name look up
- context control
- access control



Aşağıdaki örnekte hatanın sebebi access control olur.
```
#include <iostream>

class Myclass {
	int x;
};

int main()
{
	Myclass mx;
	mx.x; // access control
}
```
Yani derleyici önce name look up ile ismin tanımını class içinde bulmuştur. Sonrasında contex kullanımını tür uygunluğuna göre kontrol etmiştir. 
En son access control kısmında hata alır çünkü class member private'dır.



Aşağıdaki örnekde de bir değişken tanımı, bir fonksiyon gibi kullanılmaya çalışıldığı için context control hatası görülür.
```
#include <iostream>

class Myclass {
public:
	int x;
};

int main()
{
	Myclass mx;
	mx.x(); //context control hatası
}
```


Uyarı: Sınıfın public, private ve protected bölümleri sınıf içindeki ayrı scope'lar değildir. 

```
class Myclass {
public:
	void x();
private:
	int x; // sentaks hatası olur
};
```


- Function overloading kuralları class'lar içerisinde geçerlidir.
```
#include <iostream>

class Myclass {
public:
	void f(int);
private:
	void f(double);
};

int main()
{
	Myclass m;
	m.f(1.2); // access control hatası
}
```


member function:
```
#include <iostream>

void f1(int); // global function - free function - stand alone function

class Myclass {
public:
	void f2(int); // member function - non-static member function
private:
	int mx, my; // non-static data member
};
```

- Sınıfların non-static öğe fonksiyonlarının aslında gizli bir pointer parametre değişkenine sahip ama o parametre değişkeni yazılmaz. Yani bildirimde kaç parametre değişkeni var ise aslında o
sayının bir fazlası adedinde parametreye sahiptir. Bir parametre değişkeni sınıf türünden pointer olur. Bu pointer değişken de sınıfın kendisini gösterir.

- C++ dilinde class fonksiyonlarının definition'u yapılırken public/private kelimeleri kullanılmaz ama projeye göre programcıların görebilmesi için ön işlemci komutları kullanılabilir.


```
//myclass.h
class Myclass{
public:
	void foo();
};

//myclass.cpp

#include "myclass.h"
#define PUBLIC
#define PRIVATE
#define PROTECTED

PUBLIC void Myclass::foo();
{
}

```



- classların içerisinde fonksiyon tanımı yapıldığında o fonksiyon otomatik olarak inline fonksiyon olur.
- Bir header dosyada bir fonksiyonun bildirimi class içerisinde yapılırsa ve class'ın dışında o fonksiyonun tanımı yapılırsa ODR ihlal edilmiş olur.
```
//myclass.h

class Myclass {
public:
	void foo();
};

void Myclass::foo();
{
	// Eğer bu header file birden fazla kez include edilirse ODR ihlal edilmiş olur.
	// ODR'ın ihlal edilmemesi için inline anahtar kelimesi ile definition yapılmalıdır.
}
```

Eğer bir isim sınıfın üye fonksiyonu içinde nitelenmeden (unqualified name) kullanılmış ise aşağıdaki sıralamada arama gerçekleşir.
- Kullanılan block içerisinde
- Onu kapsayan block ve blocklar içerisinde (enclosing block)
- class scope'da (class definition) içerisinde
- namespace'de aranır.

```
#include <iostream>

class Myclass {
public:
	void foo();
private:
	int x;
};

Myclass g;

void Myclass::foo()
{
	g.x = 10; // geçerli bir kod olur.
}

```

name look up'ın anlaşılması için bir örnek:
```
#include <iostream>

class Myclass {
public:
	void foo();
private:
	int x = 10;
};

int x = 15;

int main()
{
	Myclass c;
	c.foo();
}

void Myclass::foo()
{
	int x = 20;

	int result = ::x + x + Myclass::x; // 15 + 20 + 10 işleme alınır.
	std::cout << "result = " << result;
}
```

Bir örnek:
```
#include <iostream>

class Myclass {
public:
	void func(int);
};

void func(int, int);


void Myclass::func()
{
	func(10, 20); // class scope'daki func ismi görülür ve hata olur. 
}
```


this: 

Bu anahtar sözcük yalnızca sınıfın non-static üye fonksiyonları içinde kullanılabilir. Global fonksiyon içerisinde veya sınıfın static bir üye fonksiyonu
içerisinde bu anahtar sözcüğün kullanımı sentaks hatasıdır.

this bir pointer'dır "this pointer" olarak da sıkça kullanılır. 

Örnek olarak:

```
#include <iostream>

class Myclass {
public:
	void foo()
	{
		std::cout << "this = " << this << "\n";
	}
};

int main()
{
	Myclass m;

	std::cout << "&m = " << &m << "\n";
	m.foo();
}
```
Yukarıdaki örnekte this pointer'ı m nesnesinin adresini gösterir.

- this yalnız başına bir ifadedir ve değer kategorisi PR value'dır. 
```
class Myclass {
public:
	void foo()
	{
		mx = 20;
		Myclass::mx = 20;
		this->mx = 20; // son üç satırdaki mx aynı nesneyi ifade eder.
	}
private:
	int mx;
};
```

- this anahtar sözcüğünün varlık sebebi için bir örnek:
```
class Myclass {
public:
	void f();
};

void f1(Myclass*);
void f2(Myclass);
void f3(Myclass&);

void Myclass::f()
{
	f1(this);
	f2(*this);
	f3(*this);
}
```
===
```
class Myclass {
public:
	Myclass* f1()
	{
		return this;
	}
	Myclass f2()
	{
		return *this;
	}
	Myclass& f3()
	{
		return *this;
	}
};
```


Bir chaining-fluent API örneği:
```
#include <iostream>

class Myclass {
public:
	Myclass& f1()
	{
		std::cout << "Myclass::f1() this = " << this << "\n";
		return *this;
	}
	Myclass* f2()
	{
		std::cout << "Myclass::f2() this = " << this << "\n";
		return this;
	}
	Myclass* f3()
	{
		std::cout << "Myclass::f3() this = " << this << "\n";
		return this;
	}
	Myclass* f4()
	{
		std::cout << "Myclass::f4() this = " << this << "\n";
		return this;
	}
};

int main()
{
	Myclass m;

	m.f1().f2()->f3()->f4(); //chaining-fluent API
}

```


const member function: Fonksiyonlar söz konusu olduğunda ister global fonksiyon olsun (free, non-member function) ister sınıfların member function'u olsun, bir fonksiyon
bir şekilde bir sınıf nesnesini referans semantiği veya pointer semantiği ile alıyorsa şunlardan biri olmak zorundadır.
- accessor function -> salt okuma immutable
- mutator function -> değiştirmeye yönelik mutable

Sınıfların non-static üye fonksiyonuları:
- const member function
- non-const member function

```
class Myclass {
public:
	int set(); //mutator
	int get()const; //accessor, buradaki const fonksiyonun ilk parametresindeki gizli pointer'ın const'u dur.
};
```


const üye fonksiyonlar sınıfların non-static veri elemanlarını değiştiremezler.
```
class Myclass {
public:
	void func()const
	{
		mx = 10; // hata olur. (const Myclass*).mx 
	}
private:
	int mx;
};
```

const bir sınıf nesnesi için sınıfın yalnızca const üye fonksiyonları çağırılabilir.
```
#include <iostream>

class Myclass {
public:
	void foo()
	{
		func(); // legal -> T* türünden const T* türüne dönüşüm vardır.
	}
	void func()const
	{
		auto x = mx; // legaldir. mx nesnesi değiştirilmiyor.
		foo(); // illegaldir. const T* dan T* a dönüşüm var. 
	}
private:
	int mx;
};

int main()
{
	Myclass m;

	m.foo(); // legal
	m.func(); // legal'dir çünkü T*'dan const T*a dönüşüm vardır.

	const Myclass c;

	c.foo(); // illegal çünkü const T*'dan T* a çağrı
	c.func(); //legal'dir const T*'dan const T* a çağrı
	
}
```
Yukarıdaki örnekte görüldüğü üzere sınıfın const üye fonksiyonları, sınıfın non-const üye fonksiyonlarını çağıramaz. Ama sınıfın non-const üye fonksiyonları, sınıfın const 
üye fonksiyonlarını çağırabilir.




- Sınıfın const üye fonksiyonları, sınıfın const üye fonksiyonlarını çağırabilir.
```
class Myclass {
public:
	void foo()const
	{

	}
	void func()const
	{
		foo(); // legal olur.
	}
};
```
====
```
class Myclass {
public:
	Myclass* foo()const
	{
		return this; // illegal olur. const T* türünden T* türüne dönüşüm vardır.
	}

};
```
====
```
class Myclass {
public:
	void foo()const
	{
		Myclass m;
		int mx;
		m.mx = 10;// legaldir. buradaki mx block scope içindeki mx olur.
	}

private: 
	int mx;
};
```
====
```
class Myclass {
public:
	void foo()const;
};

Myclass g;

void Myclass::foo()const
{
	*this = g; // illegal olur çünkü const T* türünden bir nesne değiştirilmeye çalışılıyor.
}
```
====
```
class Myclass {
public:
	void foo();
	void foo()const;
};


int main()
{
	Myclass m;
	m.foo(); // foo() çağırılır.

	const Myclass k;
	k.foo(); // foo()const çağırılır.
	
}
```

Uyarı: Sınıfın tüm (non-static) veri elemanları, sınıf nesnesinin observable state'i ile doğrudan ilişkili olmayabilir. 

Mutable: mutable anahtar sözcüğü, derleyiciye const üye fonksiyonlar içinde bu veri elemanının değerinin değişmesini legal olarak
kabul et denilmiş oluyor. 
Ayrıca semantik olarak mutable değişkenler, sınıf nesnesinin problem domainindeki anlamından bağımsız olarak onun değerine bir katkıda bulunmuyor.

Aşağıda görüldüğü üzere m_debug_count problem domaininden farklı bir amaçla tanımlanmıştır.
```
class Date {
public:
	void print()const
	{
		++m_debug_count;
	}
private:
	int md, mm, my;
	mutable int m_debug_count;
};
```

Aşağıda görüldüğü gibi sınıfdaki mx veri elemanı mutable olduğu için sınıf const olarak tanımlanmasına rağmen mx üzerinde değişiklik yapılabildi. Derleyici const controlü yapmadı.
```
#include <iostream>

class Nec {
public:
	mutable int mx{};
};

int main()
{
	const Nec mynec;
	mynec.mx = 5; 
}
```

# Sınıfların contructor ve destructor üyeleri


Bir sınıf nesnesini hayata getiren anlamında constructor, nesnenin hayatını bitiren anlamında destructor kullanılır.

- Constructor'ın ismi sınıfın ismi ile aynı olmak zorundadır.
```
class Myclass {
public:
	Myclass(); // constructor
	Myclass(int); // constructor'larda overloading vardır.
};
```

Bir sınıfın birden fazla constructor'ı olabilir. 

Uyarı: Ctor'ların geri dönüş değeri kavramı yoktur. Void anahtar sözcüğü kullanımı illegaldir. void anahtar sözcüğü ile kullanılamaz.

- Ctors sınıfın (non-static) üye fonksiyonudur. (yani this pointer kullanılabiliyor)
- Ctors, sınıfın static üye fonksiyonu olamaz, const üye fonksiyonu olamaz.
- Ctors, sınıfın public üye fonksiyonu olmak zorunda değildir. (private ya da protected da olabilir)
- Ctors ismi ile (nokta ya da ok operatörü ile) çağırılamaz.

```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		mx = 4; 
		this->mx = 5;
		Myclass::mx = 6; 
	}
private:
	int mx, my;
};
```


Destructor: Ctors'dan farklı olarak yine sınıf ismi ile aynı olmalı fakat başında tilde(~) karakteri olmak zorundadır. 

- Bir sınıfın destructor'ının parametre değişkeni olamaz!
- Dolayısıyla Dtor'lar overload edilemezler.
```
class Myclass {
public:
	Myclass(){} //Ctor
	~Myclass(){}//Dtor
};
```

Default Constructor (varsayılan constructor): 
- Bir sınıfın varsayılan constructor'ı olması için bu contructor'ın parametre değişkeni olmamalıdır ya da tüm parametre değişkenleri varsayılan argüman olmalıdır.
```
class Myclass {
public:
	Myclasss(int = 10);
};
```

Yani pratik olarak default constructor argüman gönderilmeden çağırılan constructor'dır. 

- Special Member Function (sıfın özel üye fonksiyonları)

Bu fonksiyonların kodları(tanımları) belirli koşullar sağlandığında derleyici tarafından yazılabiliyor. 
- Dilin kurallarına göre (implicitly) bu fonksiyonları bildirebilir ve bizim için bu fonksiyonların kodlarını yazabilir.
> Programcı tarafından derleyiciden bu fonksiyonların kodu yazmasını talep edebilir.


6 tane special member function vardır. 
- Default constructor (default olmayanlar değildir)
- Destructor
- copy ctor (copy member)
- copy assignment (copy member)
- move ctor (move member)
- move assignment(move member)

Global sınıf nesnesi: Bir global sınıf nesnesi için Ctor, main fonksiyonunun çağırılmasından önce çağırılır çünkü global nesneler hayata main fonksiyonu çağırılmadan giriyorlar. Destructor da main fonksiyonu
çağırıldıktan sonra çağırılır. 

```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this: " << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this: " << this << "\n";
	}
};

Myclass g;

int main()
{
	std::cout << "main basladi\n";
	std::cout << "&g = " << &g << "\n";
	std::cout << "main sona eriyor\n";
}
```
Eğer 3 tane global nesne olursa g1, g2, g3 gibi. Bu durumda sıralamaya göre ctor'lar çağırılır ancak dtor'lar ters sıraya göre çağırılır Yani ilk definition'u yapılan nesnenin ömrü en uzun olur.
```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this: " << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this: " << this << "\n";
	}
};

Myclass g1;
Myclass g2;
Myclass g3;


int main()
{
	std::cout << "main basladi\n";
	std::cout << "main sona eriyor\n";
}
```

Uyarı: Farklı kaynak dosyalarda tanımlanmış global sınıf nesnelerinin hayata gelme sırası belirli değildir. (static initialization fiasco)

> static (yerel) sınıf nesneleri için:
static anahtar sözcüğü ile oluşturulan yerel değişkenler eğer onların oluşturuldukları fonksiyon çağırılmaz ise zaten hayata gelmeyecektir. Static nesneler bir kere çağırıldığında ömrü programın sonuna kadar devam eder.

```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this: " << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this: " << this << "\n";
	}
};

void foo()
{
	std::cout << "foo cagirildi\n";
	static Myclass m;
}

int main()
{
	std::cout << "main basladi\n";
	foo();
	foo();
	foo();
	std::cout << "main bitiyor\n";
}
```
Yukarıdaki foo fonksiyonu her çağırıldığında ctor çağırılmıyor, bir kere ctor çağırılıyor ve main biterken dtor çağırılır. 


Otomatik ömürlü sınıf nesleri için: Constructor programın akışı o nesnenin oluşturulduğu noktaya geldiğinde constructor çağırılır. O nesnenin hayatının sonunu belirleyen closing brace'e geldiğinde
yani scope'unun sonunda destructor çağırılır.

```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this: " << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this: " << this << "\n";
	}
};

void foo()
{
	std::cout << "foo cagirildi\n";
	Myclass m; // otmatik ömürlü Myclass nesnesi
}

int main()
{
	std::cout << "main basladi\n";
	foo();
	foo();
	foo();
	std::cout << "main bitiyor\n";
}
```

> Dinamik ömürlü nesneler C++'da "new" operatörü ile hayata geritilir. Delete operatörü de nesnelerin hayatını bitirir.
- new expression
- delete expression

Uyarı: new, malloc'un karşılığı değildir. New, dinamik ömürlü bir nesne oluşturmanın karşılığıdır. delete, free'nin karşılığı değildir. free, memory allocation yapar. delete expression ise bir nesnenin
hayatını sonlanmasını sağlar. 

```
new Fighter;
```
yazılarak bir nesne dinamik ömürlü oluşturulduğunda, derleyici tarafından operator new fonksiyonu kullanılır. 
```
void * operator new(std::size_t);
//tıpkı malloc fonksiyonu gibidir.
void* malloc(std::std_t);
```
Aralarındaki fark malloc başarısız olduğunda null pointer döndürüyor, başarılı olduğunda allocate edilmiş bellek bloğunu döndürür. Operator new başarısız olduğunda "exception throw" verir.
```
#include <iostream>

class Myclass {
public:
	Myclass()
	{
		std::cout << "default ctor this: " << this << "\n";
	}
	~Myclass()
	{
		std::cout << "destructor this: " << this << "\n";
	}
	void func()
	{
		std::cout << "Nec::func()\n";
	}
};



int main()
{
	std::cout << "main basladi\n";
	auto p = new Myclass; // auto Myclass* türünden olur.
	p->func();

	delete p; //dtor çağırılıyor.
}
```

- Dinamik bir nesne için delete çağırılmaz ise memory sızıntısı olur ama sadece memory sızıntısı ile kalmaz. Destructor fonksiyonunun çağırılmaması çok daha farklı problemlere yol açabilir.
> RAII -> resource acquisition is initialization

Constructor bir çok sınıf türünün bir nesnenin kullanabilmesi için o nesne hayata getirildiğinde bir ya da birden fazla kaynağın o nesneye bağlanması o nesnenin o kaynağı ya da kaynakları kullanıyor durumuna getirilmesi sağlanıyor.
Bu kaynak ya da kaynaklara terimsel olarak resources diyoruz. Bu resource bir bellek alanı olabilir, bir dosya olabilir, bir veri tabanı olabilir, bir mutex olabilir. Bir network bağlantısı olabilir. Nesnenin Destructor'ı çağırıldığında
destructor bu kaynakları tipik olarak geri veriyor. Eğer destructor çağırılmaz ise bu durumda resource leak oluşur. Memory leak de bir resource leak sayılabilir. 


> Default contructor aşağıdaki durumlarda çağırılı.
```
Nec n1; // default init
Nec n2{}; // value init
Nec a[10]; // dizinin her elemanı için default ctor çağırılır.

Nec x(); //!! function declaration olur.
```


Bir sınıfın default contructor'ı olmak zorunda değildir. "not - declared"

User-declared bir special member function'un bildirimini kendimiz yaparsak user-declared olarak adlandırılır. 
User-declared alt kategorilere ayrılıyor:
- user declared define: tanımı da bildirimi de programcı tarafından yapılan
- user declared defaulted: programcı bildirimi yapar ama tanımının yazılması derleyiciden talep edilir.
- user declared deleted


```
class Nec {
public:
	Nec() = default;
};
```

- to delete a function: fonksiyon vardır ama bu fonksiyona çağrı sentaks hatası oluşturur.
```
void func(int) = delete;
```
Uyarı: delete edilmiş bir fonksiyon, function overload resolution'da viable olur ve seçilebilir ama delete edildiği için sentaks hatası olur.

```
class Nec {
public:
	Nec() = delete;
};
```

> implicitly declared: Aslında siz direk olarak bi class tanımladığınızda, special member funciton'larda 6'dsı da implicitly olarak tanımlanır. (defaulted, deleted olarak)


Yani özetle sınıfın special member function'ları aşağıdakilerden birine ilişkin olur:
- not declared
- user-declared //programcı tarafından
> user declared defined
> user declared defaulted
> user declared deleted
- implicitly declared
> defaulted
> deleted


```
#include <iostream>

class Myclass {
public:
	Myclass(int x)
	{
		std::cout << "Myclass(int x) x = " << x << "\n";
	}
	Myclass(int x, int y)
	{
		std::cout << "Myclass(int x, int y) x = " << x << "y = " << y << "\n";
	}
};



int main()
{
	Myclass x1(10); // direct init
	Myclass x2{ 25 }; //direct list init
	Myclass x3 = 59; //copy init

	Myclass x4(1, 5);// overload
	Myclass x5{ 5,6 };
	Myclass x6 = { 7,8 };
}
```


Ctor initializer list / member initializer list:
Hayata getireceği sınıf nesnesinin veri elemanlarını initialize eder. Non-static veri elemanlarını initialize etmek için ctor'ların kullandığı sentaksa ctor initializer list denir. Bu sentaks sadece ctor'lar için geçerlidir.
```
class Myclass {
public:
	Myclass() : mx{ 10 }, my{ 20 }, md{ 4.6 }
	{

	}
private:
	int mx, my;
	double md;
};
```
Tüm veri elemanları ctor initializer list ile initialize etmek zorunda değilsiniz. Ama initialize edilmeyen veri elemanları default initialize edilmiş olur. Bu durum primitive türden öğelerin çöp değerde kalması demektir. 
Bu sebeple 1. tercihimiz veri elemanlarını ctor init list'te initialize etmek olmalıdır. Ctor fonksiyonu içinde atama(assignment) da yapılabilir ama tercih edilemez. 

Her zaman veri elemanlarının hayata gelme sırası, class definition'daki sıradır. 
```
class Myclass {
public:
	Myclass() : m_b{ 10 }, m_a{m_b * 20}
	{

	}
private:
	int m_a, m_b;
};
```
- class definition'da m_a ilk init edildiği için ctor'da da ilk olarak m_a init edilir ve m_b çöp değerde kalır.

```
#include <iostream>

class Date {
public:
	Date(int day, int mon, int year);
private:
	int m_day, m_mon, m_year;
};

//date.cpp
Date::Date(int day, int mon, int year) : m_day{ day }, m_mon{ mon }, m_year{ year }{}

int main()
{
	Date today{ 24, 9, 2022 };
}
```

Bir class'ın reference veri elemanları ve const veri elemanları ctor init listte initialize edilmez ise default init olur ve bu da sentaks hatası olur. 
```
#include <iostream>

class Nec {
public:
	Nec() : mx{ 0 }
	{

	}
private:
	int mx;
	int& r; // init edilmedi
	const int c; // init edilmedi
};

```






































