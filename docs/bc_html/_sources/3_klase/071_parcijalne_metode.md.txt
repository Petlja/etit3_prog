# Парцијалне методе

Парцијалне методе представљају методе чије су декларације подељене на више
делова унутар парцијалних класа. Оваква декларација метода омогућава бољу
организацију кода и олакшава рад у тимовима, посебно када се ради о великом
аутоматски генерисаном коду.

Парцијалне методе могу имати само декларацију (без тела) или могу имати и
декларацију и имплементацију. Декларација и имплементација се могу налазити у
различитим деловима парцијалне класе.

Парцијалне методе су увек **приватне** и компајлер ће их увек тако третирати.
Оне не могу имати повратну вредност - увек су типа `void`. Не могу имати
модификаторе као што су `virtual`, `abstract`, `override` или `static`.
Параметри парцијалним метода не смеју да садрже модификатор `out`.

Имплементација парцијалних метода није обавезна. Ако имплементација није
написана, позиви парцијалне методе се уклањају током компилације.

У примеру из претходне лекције парцијалне методе могле би служити за испис
израчунатих вредности у конзоли. На пример, ти си могао да наведеш само
декларацију метода `StampajObim` и `StampajPovrsinu` у својој парцијалној
класи...

```cs
using System;

namespace Trouglovi
{
    public partial class Pravougli
    {
        private double a;
        private double b;
        private double c;

        public Pravougli(double a, double b)
        {
            this.a = a;
            this.b = b;
            this.c = Math.Sqrt(a * a + b * b);
        }

        partial void StampajObim(double O);
        partial void StampajPovrsinu(double P);
    }
}
```

а твој друг њихову дефиницију и имплементацију у његовој парцијалној класи:

```cs
using System;

namespace Trouglovi
{
    public partial class Pravougli
    {
        partial void StampajObim(double O)
        {
            Console.WriteLine(O);
        }

        partial void StampajPovrsinu(double P)
        {
            Console.WriteLine(P);
        }

        public void Obim()
        {
            double O = a + b + c;
            StampajObim(O);
        }

        public void Povrsina()
        {
            double P = (a * b) / 2;
            StampajPovrsinu(P);
        }
    }
}
```

Након прикључивања фајлова `Pravougli1.cs` и `Pravougli2.cs` у свом пројекту,
наставник је могао да тестира функционалност вашег кода на следећи начин:

```cs
using Trouglovi;

class Program
{
    static void Main()
    {
        Pravougli pt = new Pravougli(3.0, 4.0);
        pt.Obim();
        pt.Povrsina();
    }
}
```
