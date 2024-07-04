# Употреба чланова изведене класе

На почетку овог поглавља научио си да се у изведеној класи наслеђују чланови
базне класе, да се у изведеној класи могу дефинисати и нови чланови и да се у
иведеној класи могу изменити изменити чланови који су наслеђени из базне класе.
Конфузија настаје када се каже да се у "изведеној класи наслеђују чланови базне
класе". У том тренутку треба прецизно дефинисати шта се тачно наслеђује из
базне класе, а шта не, као и шта јесте, а шта није из базне класе доступно у
изведеној класи.

Наслеђивање чланова базне класе у изведеној класи и ограничавање доступности
чланова базне класе у изведеној класи су две потпуно **различите** ствари! Неки
члан базне класе може да буде наслеђен у изведеној класи, али због модификатора
приступа недоступан у изведеној класи!

Из базне класе не наслеђују се конструктори за инстанцирање, статички
конструктори и финализатори. Сви остали чланови базне класе се наслеђују, што
не значи да су сви остали чланови базне класе увек доступни у изведеној класи.
Приватни чланови базне класе видљиви су у изведеној класи, само ако је изведена
класа угнежђена у базној класи - у осталим случајевима приватни чланови базне
класе нису видљиви у изведеној класи.

У следећем примеру изведена класа `IzvedenaKlasa` угнежђена је у базној класи
`BaznaKlasa`. Приватни члан `broj` базне класе наслеђује се и видљив је у
изведеној класи...

```cs
class BaznaKlasa
{
    private int broj = 10;
    public class IzvedenaKlasa : BaznaKlasa
    {
        public int VratiBroj()
        {
            return broj;
        }
    }
}
```

...па овај код неће изазвати грешку приликом компајлирања. У главном програму
можеш инстанцирати објекат изведене класе и приступити приватном члану базне
класе на следећи начин:

```cs
using System;

class BaznaKlasa
{
    private int broj = 10;
    public class IzvedenaKlasa : BaznaKlasa
    {
        public int VratiBroj()
        {
            return broj;
        }
    }
}

class Program
{
    static void Main()
    {
        BaznaKlasa.IzvedenaKlasa objekat = new BaznaKlasa.IzvedenaKlasa();
        Console.WriteLine(objekat.VratiBroj());
    }
}
```

Међутим, ако изведена класа није угнежђена у базној класи, приватни члан базне
класе биће наслеђен, али због модификатора приступа `private` неће бити
доступан у изведеној класи...

```cs
class BaznaKlasa
{
    private int broj = 10;
}

class IzvedenaKlasa : BaznaKlasa
{
    public int VratiBroj()
    {
        return broj;
    }
}
```

...па ће овај кôд проузроковати грешку:

```text
CS0122: 'BaznaKlasa.broj' is inaccessible due to its protection level
```

Сада, када је ти јасна разлика између наслеђивања и ограничавања доступности,
можеш да креираш објекте изведене класе и користиш чланове базне и изведене
класе кроз те објекте. На пример:

```cs
using System;

class BaznaKlasa
{
    public int x = 1;

    public void MetodaBazne()
    {
        Console.WriteLine("Pozdrav iz bazne klase!");
    }
}

class IzvedenaKlasa : BaznaKlasa
{
    public int y = 2;

    public void MetodaIzvedene()
    {
        Console.WriteLine("Pozdrav iz izvedene klase!");
    }
}

class Program
{
    static void Main()
    {
        IzvedenaKlasa izv = new IzvedenaKlasa();
        Console.WriteLine(izv.x);
        Console.WriteLine(izv.y);
        izv.MetodaBazne();
        izv.MetodaIzvedene();
    }
}
```

У конзоли ће се прво исписати вредност поља `x` дефинисана у базној класи и
вредност поља `y` дефинисана у изведеној класи, па ће се извршити методе
`MetodaBazne()` и `MetodaIzvedene()`:

```text
1
2
Pozdrav iz bazne klase!
Pozdrav iz izvedene klase!
```
