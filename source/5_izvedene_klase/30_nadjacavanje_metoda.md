# Надјачавање метода

Појам "најдачавање метода" (енгл. *Method Overriding*) односи се на могућност
надјачавања или преовладавања метода базне класе у изведеним класама. Тиме се
омогућава да се у изведеним класама дефинишу специфичне имплементацију метода
дефинисаних у базним класама.

Да би имплементирао механизам надјачавања метода потребно је да користиш
кључну реч `virtual` приликом дефиниције методе у базној класи и кључну реч
`override` приликом дефиниције методе у изведеној класи. На пример:

```cs
using System;

class BaznaKlasa
{
    public virtual void Metoda()
    {
        Console.WriteLine("Pozdrav iz bazne klase!");
    }
}

class IzvedenaKlasa1 : BaznaKlasa
{
    public override void Metoda()
    {
        Console.WriteLine("Pozdrav iz izvedene klase 1!");
    }
}

class IzvedenaKlasa2 : BaznaKlasa
{
    public override void Metoda()
    {
        Console.WriteLine("Pozdrav iz izvedene klase 2!");
    }
}

class Program
{
    static void Main()
    {
        BaznaKlasa baz = new BaznaKlasa();
        IzvedenaKlasa1 izv1 = new IzvedenaKlasa1();
        IzvedenaKlasa2 izv2 = new IzvedenaKlasa2();
        baz.Metoda();
        izv1.Metoda();
        izv2.Metoda();
    }
}
```

У конзоли ће се исписати...

```text
Pozdrav iz bazne klase!
Pozdrav iz izvedene klase 1!
Pozdrav iz izvedene klase 2!
```

...јер је виртуелна метода `Metoda()` базне класе надјачана у изведеним класама
под истим именом.

Иако у изведеној класи надјачаваш виртуелну методу базне класе, у изведеној
класи можеш приступити виртуелној методи базне класе користећи кључну реч
`base`. На пример:

```cs
using System;

class BaznaKlasa
{
    public virtual void Metoda()
    {
        Console.WriteLine("Pozdrav iz bazne klase!");
    }
}

class IzvedenaKlasa : BaznaKlasa
{
    public override void Metoda()
    {
        base.Metoda();
        Console.WriteLine("Pozdrav iz izvedene klase!");
    }
}

class Program
{
    static void Main()
    {
        IzvedenaKlasa izv = new IzvedenaKlasa();
        izv.Metoda();
    }
}
```

Сада ће се у конзоли исписати...

```text
Pozdrav iz bazne klase!
Pozdrav iz izvedene klase!
```

...јер је у надјачаној методи изведене класе прво позвана виртуелна метода
базне класе.

Такође, базна класа може поставити референце на објекат изведена класе:

```cs
using System;

class BaznaKlasa
{
    public virtual void Metoda()
    {
        Console.WriteLine("Pozdrav iz bazne klase!");
    }
}

class IzvedenaKlasa : BaznaKlasa
{
    public override void Metoda()
    {
        Console.WriteLine("Pozdrav iz izvedene klase!");
    }
}

class Program
{
    static void Main()
    {
        BaznaKlasa baz = new IzvedenaKlasa();
        baz.Metoda();
    }
}
```

У конзоли ће се исписати текст који исписује надјачана метода:

```text
Pozdrav iz izvedene klase!
```

Иако изгледа прилично једноставно, могућност надјавачавања метода базне класе у
изведеним класама даје ти могућност да третираш различите објекте на унифициран
начин, али са специфичним понашањем, односно, даје ти могућност да
имплементираш полиморфно понашање објеката. Кôд у којем је имплементирано
надјачавање метода је свакако флексибилнији и модуларнији јер логику специфичну
за одређењу класу можеш да прикажеш у методама те класе.
