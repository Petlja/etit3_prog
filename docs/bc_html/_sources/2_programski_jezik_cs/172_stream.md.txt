# Рад са токовима

Поред класа `File` и `Directory` о којима си учио у претходној лекцији, за рад
са фајловима често се користе класе `StreamWriter` и `StreamReader` које су
такође дефинисане у именском простору `System.IO`, односно склопу
`mscorlib.dll`.

## Упис карактера у ток

Класа `StreamWriter` омогућава упис карактера, одређеног кодног стандарда, у
ток, обично у текстуални фајл, где је подразумевани кодни стандард `UTF-8`.

Нека је задатак да у нови фајл `imenik.txt` упишеш, у првој линији своје име и
презиме, у другој своју адресу електронске поште и у трећој свој број телефона:

```cs
using System.IO;

class Program
{
    static void Main()
    {
        string putanja = "imenik.txt";
        using (StreamWriter sw = new StreamWriter(putanja))
        {
            sw.WriteLine("Velimir Radlovacki");
            sw.WriteLine("velimir.radlovacki@teslavs.edu.rs");
            sw.WriteLine("+38113830668");
        }
    }
}
```

Нека је сада задатак да у исти фајл у првој линији додаш своју адресу, а у
другој место и ПТТ број:

```cs
using System.IO;

class Program
{
    static void Main()
    {
        string putanja = "imenik.txt";
        using (StreamWriter sw = new StreamWriter(putanja, true))
        {
            sw.WriteLine("Sterijina 40");
            sw.WriteLine("Vrsac 26300");
        }
    }
}
```

## Читање карактера из тока

Класа `StreamReader` омогућава читање карактера, одређеног кодног стандарда, из
тока, обично из текстуалног фајла, где је подразумевани кодни стандард `UTF-8`.

Нека је задатак да у конзоли испишеш садржај целог фајла `imenik.txt` којег си
креирао у претходном примеру:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string putanja = "imenik.txt";
        using (StreamReader sr = new StreamReader(putanja))
        {
            string sadrzaj = sr.ReadToEnd();
            Console.WriteLine(sadrzaj);
        }
    }
}
```

Нека је сада задатак да у конзоли испишеш садржај целог фајла `imenik.txt`, али
линију по линију:

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string putanja = "imenik.txt";
        using (StreamReader sr = new StreamReader(putanja))
        {
            string linija;
            while ((linija = sr.ReadLine()) != null)
            {
                Console.WriteLine(linija);
            }
        }
    }
}
```

У претходним примерима, `using` израз се користи за креирање објекта који ће
бити аутоматски ослобођен након што се заврши блок кода. Ово је важно, јер
осигурава да се ресурси као што су фајлови правилно затварају, чак и ако дође
до изузетка.

У примерима се користи релативна путања до фајла `imenik.txt`. У пракси, често
је потребно користити апсолутне путање или другачије механизме за проналажење
фајлова у систему, на пример помоћу метода класа `File`, `Directory` и
`DirectoryInfo`.

Поред `StreamWriter` и `StreamReader` класа, за рад са текстуалним фајловима
можеш користити и класе `StringWriter`, `StringReader`, `TextWriter` и
`TextReader` из истог именског простора `System.IO`. Детаљни описи свих
наведених класа дати су у званичној
[документацији](https://learn.microsoft.com/en-us/dotnet/api/system.io?view=netframework-4.8).
