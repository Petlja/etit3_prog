# Рад са бинарним фајловима

Класе `BinaryWriter` и `BinaryReader` омогућавају уписивање бинарних података у,
односно читање бинарних података из фајлова. Подржан је рад са подацима
различитих типова (`int`, `double`, `bool`, `string`) у бинарном формату.

Као и класе из претходних лекција, ове класе су такође дефинисане у именском
простору `System.IO`, односно склопу `mscorlib.dll`.

Нека је задатак да напишеш методу за упис следећих података у нови бинарни фајл
`fajl.bin`...

* име и презиме (`string`),
* да ли си редован ученик (`bool`),
* колико имаш година (`int`) и
* твој просек оцена на крају II разреда (`double`).

...и методу за читање уписаних података из истог фајла:

```cs
using System;
using System.IO;
using System.Text;

class Program
{
    const string putanja = "fajl.bin";
    public static void Upis()
    {
        using (var tok = File.Open(putanja, FileMode.Create))
        {
            using (var writer = new BinaryWriter(tok, Encoding.UTF8, false))
            {
                writer.Write(@"Velimir Radlovački");
                writer.Write(true);
                writer.Write(17);
                writer.Write(4.56);
            }
        }
    }

    public static void Prikaz()
    {
        string ime;
        bool redovan;
        int godine;
        double prosek;

        if (File.Exists(putanja))
        {
            using (var tok = File.Open(putanja, FileMode.Open))
            {
                using (var reader = new BinaryReader(tok, Encoding.UTF8, false))
                {
                    ime = reader.ReadString();
                    redovan = reader.ReadBoolean();
                    godine = reader.ReadInt32();
                    prosek = reader.ReadDouble();
                }
            }
            Console.WriteLine($"{ime}\r\n{redovan}\r\n{godine}\r\n{prosek}");
        }
    }

    static void Main()
    {
        Upis();
        Prikaz();
    }
}
```

Параметри `Encoding.UTF8` и `false` конструктора `BinaryWriter` и `BinaryReader`
су опциони. Ако се у конструктору наведе само ток, креираће се инстанце
наведене класе са UTF-8 кодним стандардом и на крају, ток ће се затворити.
