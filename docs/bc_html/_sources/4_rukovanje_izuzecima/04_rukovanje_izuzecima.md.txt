# Руковање изузецима

У претходној лекцији упознао си се са основним обликом програма у којем се
обрађују изузеци, а који садржи `try`, `catch` и `finally` блокове. Међутим,
правило је да након дефинисаног блока `try` обавезно треба дефинисати један или
више `catch` блокова, или блок `finally`, или оба. То значи да један `try` блок
може имати:

* један `catch` блок и један `finally` блок,
* један `catch` блок и ниједан `finally` блок,
* више `catch` блокова и један `finally` блок,
* више `catch` блокова и ниједан `finally` блок и
* ниједан `catch` блок и један `finally` блок.

Коју ћеш комбинацију користити зависи од ситуације. Тако, пример из претходне
лекције за обраду корисничког уноса...

```cs
using System;

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            Console.WriteLine("Ti imas " + god + " godina.");
        }
        catch (Exception e)
        {
            Console.WriteLine("Desila se greska: " + e.Message);
        }
        finally
        {
            Console.WriteLine("Kraj programa!");
        }
    }
}
```

...можда желиш дефинисати без `finally` блока:

```cs
using System;

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            Console.WriteLine("Ti imas " + god + " godina.");
        }
        catch (Exception e)
        {
            Console.WriteLine("Desila se greska: " + e.Message);
        }
    }
}
```

Тестирајући овај кôд можеш да закључиш да су могуће грешке...

* унос податка у погрешном формату (`FormatException`), тј. погрешног типа, или
* унос податка који прелази границе задате типом (`OverflowException`)

...па сходно томе можеш да обрадиш сваки изузетак понаособ тако да се поруке о
грешкама приказују на српском, а не на енглеском језику. Узми у обзир да
просечном кориснику рачунара неће ништа значити порука
`Input string was not in a correct format.` или
`Value was either too large or too small for an Int32.`, па зато можеш да
користиш више `catch` блокова:

```cs
using System;

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            Console.WriteLine("Ti imas " + god + " godina.");
        }
        catch (FormatException e)
        {
            Console.WriteLine("Niste uneli ceo broj u ispravnom formatu!");
            Console.WriteLine("Primer ispravnog formata celog broja je: 17");
            Console.WriteLine("Detalji greske: " + e);
        }
        catch (OverflowException e)
        {
            Console.WriteLine("Ceo broj mora biti u opsegu od -2147483648 do 2147483647.");
            Console.WriteLine("Primer celog broja u dozvoljenim granicama je: 17");
            Console.WriteLine("Detalji greske: " + e);
        }
        catch (Exception e)
        {
            Console.WriteLine("Desila se nepredvidjena greska.");
            Console.WriteLine("Detalji greske: " + e);
        }
    }
}
```

У овом примеру посебно су обрађени изузеци из класа `FormatException` и
`OverflowException`, али је - за сваки случај - остала и обрада изузетака из
основне класе за све изузетке `Exception`, у случају да се деси изузетак који
није предвиђен.

Сада ће, уколико корисник унесе стринг уместо целог броја, извршавање програма
у конзоли изгледати овако...

```text
Koliko imas godina (ceo broj): sedamnaest
Niste uneli ceo broj u ispravnom formatu!
Primer ispravnog formata celog broja je: 17
Detalji greske: System.FormatException: Input string was not in a correct format.
   at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 10
```

...односно, уколико унесе број који превазилази границе дефинисане типом:

```text
Koliko imas godina (ceo broj): 11111777777
Ceo broj mora biti u opsegu od -2147483648 do 2147483647.
Primer celog broja u dozvoljenim granicama je: 17
Detalji greske: System.OverflowException: Value was either too large or too small for an Int32.
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 10
```

`catch` блокови се обрађују редом којим су написани, па распоред којим се они
наводе јесте битан! Важно је да најспецифичнији изузеци буду обрађени први, док
најопштији изузеци (као што је `Exception`) буду обрађени последњи. Ако наведеш
општији `catch` блок пре специфичнијег, специфичнији `catch` блок никада неће
бити извршен, јер ће општији блок обрадити све изузетке пре него што специфични
блок за то добије прилику.

Ако након `try` блока не наведеш `catch`, већ само `finally` блок, изузетак
ће се пропагирати ван `try` блока, систем ће исписати детаље изузетка у
конзоли и `finally` блок ће се извршити. Ако у следећем програму...

```cs
using System;

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            Console.WriteLine("Ti imas " + god + " godina.");
        }
        finally
        {
            Console.WriteLine("Kraj programa!");
        }
    }
}
```

...корисник унесе стринг уместо валидне целобројне вредности, систем ће
исписати детаље изузетка па након тога извршити `finally` блок - програм се
неће срушити!

```text
Koliko imas godina (ceo broj): sedamnaest

Unhandled Exception: System.FormatException: Input string was not in a correct format.
   at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 11
Kraj programa!
```
