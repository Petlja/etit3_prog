# Бацање изузетака

Када желиш да сигнализираш да је дошло до грешке или неочекиваног стања, можеш
користити `throw` за бацање новог изузетка. Најчешће ће то бити неки од
предефинисаних изузетака као што су `ArgumentException`,
`InvalidOperationException`, итд.

На пример, нека је задатак да креираш методу за проверу броја година ученика
у твом одељењу. Иако је у главном програму већ проверено да унети број година
није стринг и да не излази ван граница дефинисаних типом, ова метода треба да
провери да ли је унети број година прихватљив за ученика III разреда. Нека је
прихватљив број 16, 17, 18 или 19, а неприхватљив број мањи од 16 или већи од
19 и нека се метода позива у програму из претходне лекције:

```cs
using System;

class Program
{
    static void ValidacijaGodina(int god)
    {
        if (god < 16 || god > 19)
        {
            throw new ArgumentException("Broj mora biti u opsegu od 16 do 19.");
        }
        Console.WriteLine("Uneti broj godina je validan.");
    }

    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            ValidacijaGodina(god);
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
        finally
        {
            Console.WriteLine("Kraj programa!");
        }
    }
}
```

Ако корисник унесе неприхватљив број година за ученика III разреда, извршавање
програма у конзоли изгледаће овако:

```text
Koliko imas godina (ceo broj): 10
Desila se nepredvidjena greska.
Detalji greske: System.ArgumentException: Broj mora biti u opsegu od 16 do 19.
   at Program.ValidacijaGodina(Int32 god) in C:\ConsoleApp\Program.cs:line 10
   at Program.Main() in C:\ConsoleApp\Program.cs:line 20
Kraj programa!
```

Пошто бачени изузетак није `FormatException`, нити `OverflowException`, ухваћен
је и обрађен тек у трећем `catch` блоку.

Шта би се десило да у главном програму нису обрађени изузеци...

```cs
using System;

class Program
{
    static void ValidacijaGodina(int god)
    {
        if (god < 16 || god > 19)
        {
            throw new ArgumentException("Broj mora biti u opsegu od 16 do 19.");
        }
        Console.WriteLine("Uneti broj godina je validan.");
    }

    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        int god = int.Parse(Console.ReadLine());
        ValidacijaGodina(god);
        Console.WriteLine("Ti imas " + god + " godina.");
        Console.WriteLine("Kraj programa!");
    }
}
```

...и да корисник унесе неприхватљив број година за ученика III разреда:

```text
Koliko imas godina (ceo broj): 10

Unhandled Exception: System.ArgumentException: Broj mora biti u opsegu od 16 do 19.
   at Program.ValidacijaGodina(Int32 god) in C:\ConsoleApp\Program.cs:line 9
   at Program.Main() in C:\ConsoleApp\Program.cs:line 18
```

Програм се срушио! Изузетак јесте бачен, али није ухваћен и обрађен!
