# Рад са текстуалним фајловима

Oсновне операције за рад са текстуалним фајловима могу се реализовати помоћу
метода из класе `File` из именског простора `System.IO`.

Метода `WriteAllText` креира нови фајл, уписује задати текст у фајл и затвара
фајл. Ако фајл већ постоји, онда ће се његов садржај обрисати, а уписаће се
задати текст. Метода `ReadAllText` отвара фајл, учитава цео текст из фајла у
стринг и затвара фајл.

Нека је задатак да се упише текст `Hello, World!` у фајл `MojFajl.txt` који се
налази у истом директоријуму где се налази и извршни фајл апликације, па након
тога из фајла `MojFajl.txt` прочита уписани текст и испише у конзоли:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string tekstZaUpis = "Hello, World!";
        File.WriteAllText("MojFajl.txt", tekstZaUpis);
        string procitanTekst = File.ReadAllText("MojFajl.txt");
        Console.WriteLine(procitanTekst);
    }
}
```

Метода `WriteAllLines` креира нови фајл, уписује низ стрингова у фајл и затвара
фајл. Сваки елемент низа стрингова уписује се у нову линију фајла, тј. нови
ред. Метода `ReadAllLines` отвара фајл, учитава све линије (редове) у елементе
низа стрингова и затвара фајл.

Нека је сада задатак да се у првој линији фајла `Podaci.txt` упише твоје име и
презиме, у другој адреса твоје електронске поште и у трећој твој број телефона.
Фајл треба да буде у претходно креираном директоријуму `C:\Imenik\`. Након тога
све уписане линије треба да се испишу у конзоли:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string[] linijeZaUpis = { "Velimir Radlovacki",
            "velimir.radlovacki@teslavs.edu.rs",
            "+38113830668" };
        File.WriteAllLines(@"C:\Imenik\Podaci.txt", linijeZaUpis);
        string[] procitaneLinije = File.ReadAllLines(@"C:\Imenik\Podaci.txt");
        foreach (string linija in procitaneLinije)
            Console.WriteLine(linija);
    }
}
```

У овом задатку, приликом навођења апсолутне путање, испред наводника користи се
карактер `@`, јер се у свакој апсолутној путањи налази бар један карактер `\`.
Такође, требаш водити рачуна да методе за рад са фајловима неће креирати
директоријуме. На пример, да директоријум `C:\Imenik\` није претходно креиран,
јавила би се грешка:

```text
Unhandled Exception: System.IO.DirectoryNotFoundException: Could not find a part of the path 'C:\Imenik\Podaci.txt'.
```

Интересантне методе из класе `File` су и метода `AppendAllText` која додаје
текст у фајл и затвара фајл и метода `AppendAllLines` која додаје низ стрингова
у фајл и затвара фајл. Ако фајл не постоји биће креиран.

Нека је сада задатак да се у фајл `C:\Imenik\Podaci.txt` дода и твоја адреса
становања, па у конзоли испишу све уписане линије:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string adresaStana = "Sterijina 40, Vrsac 26300";
        File.AppendAllText(@"C:\Imenik\Podaci.txt", adresaStana);
        string[] procitaneLinije = File.ReadAllLines(@"C:\Imenik\Podaci.txt");
        foreach (string linija in procitaneLinije)
            Console.WriteLine(linija);
    }
}
```

До сада си научио да користиш свега неколико од мноштва метода из класе `File`.
Доступне су и методе за креирање, брисање и померање фајлова, методе за
шифровање и дешифровање фајлова и методе за рад са атрибутима и осталим
метаподацима фајлова у фајл систему.

Комплетан списак свих типова који омогућавају читање и писање у фајлове и
токове података и типове који пружају основну подршку за фајлове и
директоријуме можеш пронаћи у званичној
[документацији](https://learn.microsoft.com/en-us/dotnet/api/system.io?view=netframework-4.8).

## Основне операције за рад са директоријумима

Неке основне операције за рад са директоријумима могу се реализовати помоћу
метода из класа `File`, `Directory` и `DirectoryInfo` из именског простора
`System.IO`.

Метода `EnumerateFiles` враћа имена фајлова са путањом која одговарају
критеријуму за претрагу.

На пример, нека је потребно да се у конзоли испишу путање до свих фајлова са
екстензијом `txt` који се налазе у директоријуму `C:\Imenik` креираном у
претходном задатку:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        var txtEkstenzije = Directory.EnumerateFiles(@"C:\Imenik", "*.txt");
        foreach (string putanja in txtEkstenzije)
            Console.WriteLine(putanja);
    }
}
```

Метода `EnumerateDirectories` враћа имена директоријума са путањом која
одговарају критеријуму за претрагу.

Нека је задатак исписати све директоријуме који се налазе у кореном
директоријуму `C:\`.

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        var direktorijumiC= Directory.EnumerateDirectories(@"C:\");
        foreach (string direktorijum in direktorijumiC)
            Console.WriteLine(direktorijum);
    }
}
```

Интересантне су и методе `Exists`, која одређује да ли задати директоријум
постоји и `CreateDirectory`, која креира задати директоријум.

У другом примеру у овој лекцији упозорен си да методе за рад са фајловима неће
креирати наведене директоријуме у путањи до фајла, већ да ће доћи до грешке ако
директоријуми не постоје. То значи да би била добра пракса да се прво провери
да ли директоријуми постоје, па ако не постоје да се креирају. Нека је задатак
да се провери да ли постоји директоријум `C:\Imenik`, па ако не постоји да се
креира и у оба случаја да се пошаљу поруке у конзоли.

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        if (Directory.Exists(@"C:\Imenik"))
        {
            Console.WriteLine(@"Direktorijum C:\Imenik vec postoji!");
        }
        else
        {
            Directory.CreateDirectory(@"C:\Imenik");
            Console.WriteLine(@"Direktorijum C:\Imenik je uspesno kreiran!");
        }
    }
}
```

Овај задатак може се решити и помоћу метода `Exists` и `Create` из класе
`DirectoryInfo`.

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        DirectoryInfo direktorijum = new DirectoryInfo(@"c:\Imenik");
        if (direktorijum.Exists)
        {
            Console.WriteLine(@"Direktorijum C:\Imenik vec postoji!");
        }
        else
        {
            direktorijum.Create();
            Console.WriteLine(@"Direktorijum C:\Imenik je uspesno kreiran!");
        }
    }
}
```
