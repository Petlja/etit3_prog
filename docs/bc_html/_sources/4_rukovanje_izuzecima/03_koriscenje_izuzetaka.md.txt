# Коришћење изузетака

Једноставан пример рада са изузецима био би обрада корисничког уноса. Иако се
од корисника јасно тражи да унесе одређени тип податка, буди сигуран да ће
корисник погрешити, случајно или намерно.

На пример, нека је задатак да напишеш једноставан програм за унос броја година
корисника и испис тог броја у конзоли. Прилично једноставан задатак, зар не?

```cs
using System;

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        int god = int.Parse(Console.ReadLine());
        Console.WriteLine("Ti imas " + god + " godina.");
        Console.WriteLine("Kraj programa!");
    }
}
```

Ако корисник унесе цео број, на пример број `17`, извршавање програма у конзоли
изгледаће овако:

```text
Koliko imas godina (ceo broj): 17
Ti imas 17 godina.
Kraj programa!
```

Међутим, ако корисник унесе нешто друго, на пример текст `sedamnaest`, програм
ће се срушити:

```text
Koliko imas godina (ceo broj): sedamnaest

Unhandled Exception: System.FormatException: Input string was not in a correct format.
   at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 8
```

Можеш ли да замислиш какве катастрофалне последице може да изазове један обичан
кориснички унос целог броја који може да сруши апликацију у току извршавања, на
пример, апликацију која је повезана на неки медицински уређај или на производни
погон у фабрици? Да би се овакве појаве спречиле, неопходно је да предвидиш и
обрадиш грешке које се могу јавити у току извршавања програма, односно изузетке
у програму. Ако се грешка деси, треба да обавестиш корисника о грешци, а програм
мора наставити са радом.

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

Сада, ако корисник унесе стринг уместо целог броја, извршавање програма у
конзоли изгледаће овако...

```text
Koliko imas godina (ceo broj): sedamnaest
Desila se greska: Input string was not in a correct format.
Kraj programa!
```

...или ако унесе превелик цео број, извршавање програма у конзоли изгледаће
овако:

```text
Koliko imas godina (ceo broj): 11111177777
Desila se greska: Value was either too large or too small for an Int32.
Kraj programa!
```

Иако су у питању две различите грешке, систем за руковање изузецима је успешно
пронашао одређене типове изузетака, `FormatException` и `OverflowException`,
обрадио их и послао адекватне поруке, а програм није престао са радом.

Грешке се могу још детаљније приказати, ако се у конзоли испише вредност целог
објекта `e`, а не својства `e.Message`.

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
            Console.WriteLine("Desila se greska: " + e);
        }
        finally
        {
            Console.WriteLine("Kraj programa!");
        }
    }
}
```

Сада, ако корисник унесе стринг уместо целог броја, извршавање програма у
конзоли изгледаће овако...

```text
Koliko imas godina (ceo broj): sedamnaest
Desila se greska: System.FormatException: Input string was not in a correct format.
   at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 10
Kraj programa!
```

...или ако унесе превелик цео број, извршавање програма у конзоли изгледаће
овако:

```text
Koliko imas godina (ceo broj): 11111177777
Desila se greska: System.OverflowException: Value was either too large or too small for an Int32.
   at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
   at System.Int32.Parse(String s)
   at Program.Main() in C:\ConsoleApp\Program.cs:line 10
Kraj programa!
```

Уколико из неког разлога не желиш да приказујеш детаље грешке кориснику, већ
само своју поруку, немој да користиш објекат `e`:

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
        catch (Exception)
        {
            Console.WriteLine("Desila se greska!");
        }
        finally
        {
            Console.WriteLine("Kraj programa!");
        }
    }
}
```

Сада ће извршавање програма у конзоли изгледати исто и када корисник унесе
стринг уместо целог броја...

```text
Koliko imas godina (ceo broj): sedamnaest
Desila se greska!
Kraj programa!
```

...и када унесе превелик цео број:

```text
Koliko imas godina (ceo broj): 11111177777
Desila se greska!
Kraj programa!
```

Објекат `e`, поред својства `e.Message`, има и својства `StackTrace`, `Source`,
као и многа друга својства описана у
[документацији](https://learn.microsoft.com/en-us/dotnet/api/system.exception).

Значи, **основни облик** обраде изузетака садржи `try`, `catch` и `finally`
блокове. У `try` блоку наводи се кôд који може бацити изузетак, у `catch` блоку
наводи се кôд који прихвата бачени изузетак и обрађује га, а у `finally` блоку
наводи се кôд који се увек извршава - без обзира да ли је изузетак бачен или
не.
