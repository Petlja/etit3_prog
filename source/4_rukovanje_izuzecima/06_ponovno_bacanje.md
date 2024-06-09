# Поновно бацање изузетка

Ако желиш да поново бациш изузетак који је већ ухваћен у `catch` блоку, можеш
да користиш `throw` без аргумената. Тиме се задржава оригинални стек трагова
изузетка, што може да ти олакша проналажење и отклањање грешака.

Нека је задатак да креираш методу која ће унети број година ученика у главном
програму додати у фајл. То најједноставније можеш постићи методом
`File.AppendAllText`. Ова метода додаје задати стринг у фајл, а ако фајл не
постоји, креира нови фајл. Неки од изузетака који се могу појавити приликом
уписа су:

* `ArgumentException`, `ArgumentNullException` и `PathTooLongException` ако
путања није добро дефинисана или ако је дужа од системски дефинисаног
максимума,
* `DirectoryNotFoundException` ако задати директоријум у путањи не постоји,
* `IOException` ако се деси грешка приликом отварања фајла,
* `UnauthorizedAccessException` ако корисник није ауторизован да приступи или
модификује фајл, итд.

Креирана метода и њен позив у главном програму може да изгледа овако:

```cs
using System;
using System.IO;

class Program
{
    static void UpisiGodine(string putanja, int god)
    {
        try
        {
            File.AppendAllText(putanja, god.ToString());
            Console.WriteLine("Uneti broj je upisan u fajl!");
        }
        catch (Exception)
        {
            Console.WriteLine("Desila se greska prilikom upisa u fajl!");
            throw;
        }
    }

    static void Main()
    {
        Console.Write("Koliko imas godina (ceo broj): ");
        try
        {
            int god = int.Parse(Console.ReadLine());
            UpisiGodine(@"C:\ConsoleApp\godine.txt", god);
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

Ако у блоку `try` у главном програму корисник позове дату методу и не деси се
грешка, метода ће у конзоли исписати текст `Uneti broj je upisan u fajl!`.

```text
Koliko imas godina (ceo broj): 16
Uneti broj je upisan u fajl!
Ti imas 16 godina.
Kraj programa!
```

Међутим, ако се деси грешка, нпр. због непостојећег директоријума, метода ће
исписати текст `Desila se greska prilikom upisa u fajl!`, изузетак ће поново
бити бачен и обрађен у трећем `catch` блоку у главном програму.

```text
Koliko imas godina (ceo broj): 16
Desila se greska prilikom upisa u fajl!
Desila se nepredvidjena greska.
Detalji greske: System.IO.DirectoryNotFoundException: Could not find a part of the path 'C:\Console\godine.txt'.
   at System.IO.__Error.WinIOError(Int32 errorCode, String maybeFullPath)
   at System.IO.FileStream.Init(String path, FileMode mode, FileAccess access, Int32 rights, Boolean useRights, FileShare share, Int32 bufferSize, FileOptions options, SECURITY_ATTRIBUTES secAttrs, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
   at System.IO.FileStream..ctor(String path, FileMode mode, FileAccess access, FileShare share, Int32 bufferSize, FileOptions options, String msgPath, Boolean bFromProxy, Boolean useLongPath, Boolean checkHost)
   at System.IO.StreamWriter.CreateFile(String path, Boolean append, Boolean checkHost)
   at System.IO.StreamWriter..ctor(String path, Boolean append, Encoding encoding, Int32 bufferSize, Boolean checkHost)
   at System.IO.StreamWriter..ctor(String path, Boolean append, Encoding encoding)
   at System.IO.File.InternalAppendAllText(String path, String contents, Encoding encoding)
   at System.IO.File.AppendAllText(String path, String contents)
   at Program.UpisiGodine(String putanja, Int32 god) in C:\Console\Program.cs:line 16
   at Program.Main() in C:\Console\Program.cs:line 26
Kraj programa!
```
