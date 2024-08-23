# Прилагођени изузеци

Како би што боље прилагодио систем за обраду изузетака својим потребама, можеш
да креираш своје прилагођене изузетке наслеђивањем из `Exception` класе и
након тога користиш `throw` да их бацаш.

Нека је задатак да креираш изузетак `MissingUserInputException` који треба да
се баци када корисник не унесе број година ученика или унесе празнину
(*space*) у примеру из претходних лекција. Класа `MissingUserInputException` и
главни програм могу да изгледају овако:

```cs
using System;

class MissingUserInputException : Exception
{
    public MissingUserInputException(string poruka) : base(poruka) { }
}

class Program
{
    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            string num = Console.ReadLine();
            if (string.IsNullOrWhiteSpace(num))
            {
                throw new MissingUserInputException("Moras uneti broj godina!");
            }
            else
            {
                int god = int.Parse(num);
                Console.WriteLine("Ti imas " + god + " godina.");
            }
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
Komentar: u kodu se koristi base(), ali nema objasnjenja sta to radi

Када корисник не унесе број година ученика или унесе празнину, извршавање
програма у конзоли изгледаће овако:

```text
Koliko imas godina (ceo broj):
Desila se nepredvidjena greska.
Detalji greske: MissingUserInputException: Moras uneti broj godina!
   at Program.Main() in C:\ConsoleApp\Program.cs:line 18
```
