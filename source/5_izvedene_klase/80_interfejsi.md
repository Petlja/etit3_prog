# Интерфејси

Интерфејси представљају један од важних концепата објектно-оријентисаног
програмирања. Можеш их посматрати као потпуно апстрактне класе чији су сви
чланови апстрактни и јавни. Интерфејси садрже дефиниције за групу повезаних
функционалности које класе морају да имплементирају. Каже се и да интерфејси
представљају "уговоре" које класе морају да имплементирају.

Интерфејси садрже само дефиниције својих чланова, а не и њихову имплементацију,
што је основни концепт рада са интерфејсима. Они не садрже никаква поља, па ни
статичка. Не садрже ни конструкторе, ни деструкторе тј. финализаторе. Пошто су
сви чланови интерфејса јавни, у интерфејсу не смеш користити модификаторе
приступа. На крају, у интерфејсу не смеш дефинисати никакве типове.

Назив интерфејса мора бити валидан идентификатор, а по конвенцији, треба да
почне великим словом `I`. Да би декларисао интерфејс, уместо кључне речи
`class`, треба да користиш кључну реч `interface`. На пример:

```cs
interface IOsoba
{
    string Ime(string ime);
}
```

У овом интерфејсу декларисана је метода `Ime()` без модификатора приступа, где
је тело методе замењено знаком `;`. Пошто интерфејси не садрже конструкторе, из
њих не можеш директно инстанцирати објекте! Интерфејсе можеш користити само за
извођење класа или других интерфејса. На пример, класа која наслеђује интерфејс
`IOsoba` може да изгледа овако:

```cs
class Osoba : IOsoba
{
    public string Ime(string ime)
    {
        return ime;
    }
}
```

Значи, класа `Osoba` има имплементиран интерфејс `IOsoba`, што значи да
наслеђује интерфејс `IOsoba` и имплементира све чланове интерфејса `IOsoba`.

Када креираш класу која имплементира интерфејс, у класи мораш креирати методе
које одговарају методама дефинисаним у интерфејсу, где: метода у класи мора
бити јавна, јер су све методе у интерфејсу имплицитно јавне; тип вредности коју
враћа метода мора одговарати типу методе у интерфејсу; назив методе мора
одговарати називу у интерфејсу; параметри у методи, ако постоје, морају
одговарати параметрима у методи у интерфејсу.

Поред метода, интерфејси могу да садрже и својства, индексере и догађаје. Ако
интерфејс садржи својство, класа мора реализовати бар једну од метода `get` или
`set`. Сви чланови интерфејса су имплицитно јавни, апстрактни и виртуелни.

Нека је задатак да креираш интерфејс `IOsoba` са методом `Ime()` и класе
`Nastavnik` и `Ucenik` које морају да имплементирају тај интерфејс. То може да
изгледа, на пример, овако:

```cs
using System;

interface IOsoba
{
    string Ime(string ime);
}

class Nastavnik : IOsoba
{
    public string Ime(string ime)
    {
        ime = "Ucenik: " + ime;
        return ime;
    }
}

class Ucenik: IOsoba
{
    public string Ime(string ime)
    {
        ime = "Nastavnik: " + ime;
        return ime;
    }
}

class Program
{
    static void Main()
    {
        Ucenik u = new Ucenik();
        Console.WriteLine(u.Ime("Petar Petrovic"));
        Nastavnik n = new Nastavnik();
        Console.WriteLine(n.Ime("Velimir Radlovacki"));
    }
}
```

У овом једноставном примеру обе класе имплементирале су интерфејс `IOsoba` према
наведеним правилима - метода `Ime()` јесте јавна, тип вредности `string` коју
враћа метода `Ime()` одговара типу методе у интерфејсу, име методе `Ime()`
одговара имену методе у интерфејсу и параметар у методи `string ime` одговара
параметру у методи у интерфејсу.

## Надјачавање имплементираних метода

Ако у изведеној класи треба да надјачаш методу базне класе, која је у базној
класи имплементирана интерфејсом, онда ту методу у базној класи требаш
прогласити виртуелном, а у изведеној класи надјачаном. На пример:

```cs
using System;

interface IOsoba
{
    string Ime(string ime);
}

class Osoba : IOsoba
{
    public virtual string Ime(string ime)
    {
        return ime;
    }
}

class Nastavnik : Osoba
{
    public override string Ime(string ime)
    {
        return "Nastavnik: " + ime;
    }
}

class Program
{
    static void Main()
    {
        Osoba o = new Osoba();
        Console.WriteLine(o.Ime("Velimir Radlovacki"));
        Nastavnik n = new Nastavnik();
        Console.WriteLine(n.Ime("Velimir Radlovacki"));
    }
}
```

У овом једноставном примеру, виртуелна метода `Ime()` објекта `o` вратиће само
вредност свог аргумента тј. `Velimir Radlovacki`, док ће метода `Ime()` објекта
`n`, којом је надјачана, вратити стринг `Nastavnik:` спојен са вредношћу свог
аргумента, тј. `Nastavnik: Velimir Radlovacki`.

## Наслеђивање са имплементацијом интерфејса

Ако класу изводиш из друге класе уз имплементацију интерфејса, након двотачке
треба да наведеш базну класу, па запету, па базни интерфејс.

Нека класа `Osoba` имплементира интерфејс `IOsoba` и нека класа `Nastavnik`
наслеђује класу `Osoba` са имплементираним интерфејсом `IOsoba`. На пример,
овако:

```cs
using System;

interface IOsoba
{
    string Ime(string ime);
}

class Osoba : IOsoba
{
    public string Ime(string ime)
    {
        return ime;
    }
}

class Nastavnik : Osoba, IOsoba
{
    public void ImeNastavnika(string imeNastavnika)
    {
        Console.WriteLine("Nastavnik: " + imeNastavnika);
    }
}

class Program
{
    static void Main()
    {
        Nastavnik n = new Nastavnik();
        Console.WriteLine(n.Ime("Velimir Radlovacki"));
        n.ImeNastavnika("Velimir Radlovacki");
    }
}
```

Приликом дефиниције класе `Nastavnik`, прво је наведен назив класе `Nastavnik`,
па двотачка, па базна класа `Osoba`, па запета, па базни интерфејс `IOsoba`.
Објекат `n` класе `Nastavnik` може да користи јавну методу `Ime()` која је
наслеђена из класе `Osoba`, а имплементирана на основу дефиниције у интерфејсу
`IOsoba` (komentar: da li je neophodno navoditi ovde oba ili bi bilo dovoljno staviti samo klasu iz koje je navedena?).

## Наслеђивање међу интерфејсима

Интерфејси могу наслеђивати друге интерфејсе. У следећем примеру...

```cs
interface IJmbg
{
    string Jmbg(string jmbg);
}

interface IOsoba : IJmbg
{
    string Ime(string ime);
}

class Osoba : IOsoba
{
    public string Jmbg(string jmbg)
    {
        return jmbg;
    }

    public string Ime(string ime)
    {
        return ime;
    }
}
```

...класа `Osoba` имплементира интерфејс `IOsoba` који наслеђује интерфејс
`IJmbg`. То значи да у класи `Osoba` мораш имплементирати све што је дефинисано
интерфејсом `IOsoba` и све што је дефинисано интерфејсом `IJmbg`.

## Вишеструка имплементација интерфејса

У ранијим лекцијама напоменуто је да програмски језик C# не подржава вишеструко
наслеђивање, што је тачно када се говори о наслеђивању класа. Међутим,
програмски језик C# подржава вишеструко наслеђивање интерфејса, што значи да у
једној класи можеш имплементирати више интерфејса.

На пример, за наставнике су битни подаци име и ЈМБГ, а за ученике име, ЈМБГ и
ЈОБ (јединствени образовни број). Наставници немају додељен ЈОБ, али ученици
морају да имају додељен ЈОБ. У оваквој ситуацији могу се дефинисати три
интерфејса `IIme`, `IJmbg` и `IJob`. Прва два ће се имплементирати у класи
`Nastavnik`, односно сва три ће се имплементирати у класи `Ucenik`:

```cs
interface IIme
{
    string Ime(string ime);
}

interface IJmbg
{
    string Jmbg(string jmbg);
}

interface IJob
{
    string Job(string job);
}

class Nastavnik : IIme, IJmbg
{
    public string Ime(string ime)
    {
        return ime;
    }

    public string Jmbg(string jmbg)
    {
        return jmbg;
    }
}

class Ucenik : IIme, IJmbg, IJob
{
    public string Ime(string ime)
    {
        return ime;
    }

    public string Jmbg(string jmbg)
    {
        return jmbg;
    }

    public string Job(string job)
    {
        return job;
    }
}
```

Из свега наученог у овој лекцији можеш закључити да су интерфејси у програмском
језику C# одличан алат за стварање добро структурираног и одрживог кода. Они
омогућавају одвајање дефиниције од имплементације, што доприноси бољој
модуларности и поновној употреби кода.
