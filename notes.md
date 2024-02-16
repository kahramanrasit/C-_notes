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
    - fonksiyone programlama / functional programming
    - data abstraction
```

C ile C++ dili arasındaki farklılıkların hepsi olmasa da bir kısmı aşağıdaki nedenlerle ilgilidir. 
- C küçük ve genel bir dildir. C dilinde derleme zamanında yapılan kontroller sınırlıdır.
Yani C ve C++ dilleri statik tür kavramına sahip olmasına rağmen C dilinde statik tür kontrolü daha gevşektir, zorlayıcı değildir.
Bu durum da hata yapma riskini artırır. Örneğin C dilinde farklı türler arasındaki atama ve kopyalama durumlarının çoğu legaldir.
Günümüzde moderin derleyiciler bu tip hatalara yönelik uyarı mesajları veriyor olsalar da dilin kurallarına göre farklı türler arasında çoğunlukla "type conversion"
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
hatası olmalıdır. Ama böyle bir kodu bir C derleyicisinde derlediniz zaman kodun geçerli olduğu görülür. C'de derleyici bar ismini arayıp bulamadığında
yani name look up başarısız olduğunda, fonksiyon çağrı operatörünün operantının bar olduğu görüldüğünde, bu fonksiyonun başka bir modülde tanımlanmış
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
void func(void)
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

Yani C'de //false veya //true bool türden sabitler değildir. C99 ile eklenen bir başlık dosyası vardır.
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

int x = flag;  //true
int y = is_on; //false
```

Uyarı: Boolean türünden pointer türüne aşağıdaki kod parçacığındaki gibi bir dönüşüm kesinlikle yoktur. 
```
bool is_on = false;
int *ptr = is_on
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
Yani tek başına tag olan isim türü niteyen, türün yerine geçen isim değildir.
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





















