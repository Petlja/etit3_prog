# Апстрактне класе

Апстрактне класе су класе које не могу бити инстанциране. Њихова сврха је да
обезбеде дефиницију класе које се из њих изводе. Може се рећи да се апстрактним
класама дефинише "понашање" које њихове изведене класе морају да
имплементирају.

Апстрактну класу декларишеш навођењем кључне речи `abstract` пре њене
дефиниције. На пример:

```cs
abstract class Osoba
{
    // clanovi apstraktne klase
}
```

## Апстрактни чланови апстрактних класа

У апстрактним класама декларишу се апстрактни методи (то је уједно и једино
место где се могу декларисати). Да би неку методу прогласио апстрактном,
потребно је да наведеш кључну реч `abstract` пре него што наведеш њен тип, па
затим, не имплементираш њено тело већ наведеш `;`. На пример:

```cs
abstract class Osoba
{
    public abstract string Ime(string ime);
}
```

Пошто апстрактне методе нису имплементиране у апстрактним класама, логично је
да морају да буду јавне и да се морају имплементирати у изведеним класама. На
пример:

```cs
using System;

abstract class Osoba
{
    public abstract string Ime(string ime);
}

class Nastavnik : Osoba
{
    public override string Ime(string ime)
    {
        ime = "Nastavnik: " + ime;
        return ime;
    }
}

class Ucenik : Osoba
{
    public override string Ime(string ime)
    {
        ime = "Ucenik: " + ime;
        return ime;
    }
}

class Program
{
    static void Main()
    {
        Nastavnik n = new Nastavnik();
        Console.WriteLine(n.Ime("Velimir Radlovacki"));
        Console.WriteLine();
        Ucenik u = new Ucenik();
        Console.WriteLine(u.Ime("Petar Petrovic"));
    }
}
```

У овом примеру, из апстрактне класе `Osoba` изведене су класе `Nastavnik` и
`Ucenik`. Пошто је у класи `Osoba` дефинисана јавна апстрактна метода `Ime()`,
имплементација те методе се мора дефинисати и у класама `Nastavnik` и `Ucenik`.
Приликом имплементације методе `Ime()` у изведенима класама, потребно је да
наведеш кључну реч `override` пре него што наведеш тип методе.

Извршавањем овог програма креираће се објекти `n` класе `Nastavnik` и `u` класе
`Ucenik`, где су класе `Nastavnik` и `Ucenik` изведене из апстрактне класе
`Osoba`. Потом ће се позивати методе `n.Ime` и `u.Ime` које су имплементиране у
класама `Nastavnik` и `Ucenik`, па ће се конзоли исписати:

```text
Nastavnik: Velimir Radlovacki

Ucenik: Petar Petrovic
```

## Неапстрактни чланови апстрактних класа

Апстрактне класе могу да садрже и неапстрактне чланове, односно методе са
имплементацијом, које се могу користити директно од стране изведених класа.
Заправо, апстрактна класа не мора да има ниједан апстрактни метод. Може да
садржи само неапстрактне методе, поља, својства и догађаје. Циљ апстрактне
класе је да не може бити инстанцирана и да служи као основа за друге класе.
Значи, у апстрактним класама могу се наћи и апстрактни и неапстрактни чланови.
На пример:

```cs
using System;

abstract class Osoba
{
    public abstract string Ime(string ime);
    
    public void Skola()
    {
        Console.WriteLine("Skolski centar \"Nikola Tesla\"");
        Console.WriteLine("Vrsac");
    }
}

class Nastavnik : Osoba
{
    public override string Ime(string ime)
    {
        ime = "Nastavnik: " + ime;
        return ime;
    }
}

class Ucenik : Osoba
{
    public override string Ime(string ime)
    {
        ime = "Ucenik: " + ime;
        return ime;
    }
}

class Program
{
    static void Main()
    {
        Nastavnik n = new Nastavnik();
        Ucenik u = new Ucenik();
        Console.WriteLine(n.Ime("Velimir Radlovacki"));
        n.Skola();
        Console.WriteLine();
        Console.WriteLine(u.Ime("Petar Petrovic"));
        u.Skola();
    }
}
```

Извршавањем овог програма креираће се објекти `n` класе `Nastavnik` и `u` класе
`Ucenik`, где су класе `Nastavnik` и `Ucenik` изведене из апстрактне класе
`Osoba`. Потом ће се позивати методе `n.Ime` и `u.Ime` које су имплементиране у
класама `Nastavnik` и `Ucenik`, као и методе `n.Skola()` и `u.Skola()` чија је
имплементација наведена у апстрактној класи `Osoba`. У конзоли ће се исписати:

```text
Nastavnik: Velimir Radlovacki
Skolski centar "Nikola Tesla"
Vrsac

Ucenik: Petar Petrovic
Skolski centar "Nikola Tesla"
Vrsac
```

Апстрактне класе могу бити изведене из других класа, укључујући и друге
апстрактне класе. Ово омогућава креирање сложених хијерархија класа где свака
апстрактна класа може додати додатне апстрактне или неапстрактне чланове.
