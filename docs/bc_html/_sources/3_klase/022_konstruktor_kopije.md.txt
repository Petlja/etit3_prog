# Конструктор копије

Трећи тип конструктора о којем ћеш учити је конструктор копије. То је
специјални тип конструктора који се користи за стварање новог објекта који
представља копију постојећег објекта. Конструктор копије није унапред
дефинисан, што значи да га мораш експлицитно дефинисати унутар својих класа.

Нека је задатак да креираш класу `Osoba` за рад са подацима особа као што су
име и презиме и година рођења. Класа треба да обезбеди креирање објекта чија се
поља иницијализују помоћу конструктора са параметрима, као и креирање копија
постојећег објекта.

Креирање објекта чија се поља иницијализују помоћу конструктора са параметрима
обрађено је у претходној лекцији:

```cs
class Osoba
{
    public string imePrezime;
    public int godinaRodjenja;

    public Osoba(string ime, int god)
    {
        imePrezime = ime;
        godinaRodjenja = god;
    }
}
```

Креирање копија постојећег објекта могуће је коришћењем конструктора копије.
Конструктор копије има један параметар - објекат типа објекта којег желиш да
копираш. Позивом овог конструктора копирају се сви релевантни подаци из
постојећег у нови објекат. Конструктор копије можеш дефинисати и користити, на
пример овако:

```cs
using System;

class Osoba
{
    public string imePrezime;
    public int godinaRodjenja;

    public Osoba(string ime, int god)
    {
        imePrezime = ime;
        godinaRodjenja = god;
    }

    public Osoba(Osoba osobaZaKopiranje) // Konstruktor kopije
    {
        imePrezime = osobaZaKopiranje.imePrezime;
        godinaRodjenja = osobaZaKopiranje.godinaRodjenja;
    }
}

class Program
{
    static void Main()
    {
        Osoba o1 = new Osoba("Velimir Radlovacki", 1976);
        Osoba o2 = new Osoba(o1);
        Console.WriteLine(o1.imePrezime + ", " + o1.godinaRodjenja);
        Console.WriteLine(o2.imePrezime + ", " + o2.godinaRodjenja);
    }
}
```

Извршавањем програма инстанциран је објекат `o1` класе `Osoba`, чија су поља
иницијализована конструктором са параметрима. Након тога инстанциран је објекат
`o2` класе `Osoba`, чија су поља иницијализована конструктором копије (вредности
поља су копиране из објекта `o1`).

У примеру изнад, каже се да је конструктором копије направљена плитка копија
(енгл. *shallow copy*) објекта `o1`. Плитка копија подразумева копирање
вредности поља (примитивних типова и референци). Да су се у класи `Osoba`
налазиле референце на друге објекте, модификације у тим објектима утицале би
и на објекат `о1` и на објекат `о2`.

Ако се у класи налазе референце на друге објекте, потребно је да направиш
дубоку копију (енгл. *deep copy*). На пример, ако класа `Osoba` садржи и поље
`Adresa` типа објекта `Adresa`:

```cs
using System;

class Adresa
{
    public string ulicaBroj;
    public string mestoPttBroj;

    public Adresa(string ulbr, string mptt)
    {
        ulicaBroj = ulbr;
        mestoPttBroj = mptt;
    }

    public Adresa(Adresa adresaZaKopiranje)
    {
        ulicaBroj = adresaZaKopiranje.ulicaBroj;
        mestoPttBroj = adresaZaKopiranje.mestoPttBroj;
    }
}

class Osoba
{
    public string imePrezime;
    public int godinaRodjenja;
    public Adresa Adresa;

    public Osoba(string ime, int god, Adresa adr)
    {
        imePrezime = ime;
        godinaRodjenja = god;
        Adresa = adr;
    }

    public Osoba(Osoba osobaZaKopiranje)
    {
        imePrezime = osobaZaKopiranje.imePrezime;
        godinaRodjenja = osobaZaKopiranje.godinaRodjenja;
        Adresa = new Adresa(osobaZaKopiranje.Adresa);
    }
}

class Program
{
    static void Main()
    {
        Adresa a1 = new Adresa("Sterijina 40", "Vrsac 26300");
        Osoba o1 = new Osoba("Velimir Radlovacki", 1976, a1);
        Osoba o2 = new Osoba(o1);
        Console.WriteLine(o1.imePrezime + ", " + o1.godinaRodjenja +
            ", " + o1.Adresa.ulicaBroj + ", " + o1.Adresa.mestoPttBroj);
        Console.WriteLine(o2.imePrezime + ", " + o2.godinaRodjenja +
            ", " + o2.Adresa.ulicaBroj + ", " + o2.Adresa.mestoPttBroj);
    }
}
```

У овом случају, конструктор копије класе `Osoba` ствара нову копију `Adresa`
објекта, чиме се осигурава дубока копија објекта `о1`.
