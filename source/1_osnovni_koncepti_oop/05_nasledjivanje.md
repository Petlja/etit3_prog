# Наслеђивање

Наслеђивање је основни концепт у објектно-оријентисаном програмирању којим се
омогућава креирање нових класа из постојећих класа. Класа из које се наслеђује
назива се **базна** класа (енгл. *base class*), а класа која се наслеђује из
базне класе назива се **изведена** класа (енгл. *derived class*). У изведеној
класи наслеђују се чланови базне класе, а могу се дефинисати и нови чланови или
променити постојећи. Наслеђивање омогућава поновну употребу кода и његову
организацију на логичан начин, на пример у виду хијерархиске структуре класа
тј. стабла класа. Овој теми биће посвећено једно цело поглавље.

Конфузија настаје када се каже да се у "изведеној класи наслеђују чланови базне
класе". У том тренутку треба прецизно дефинисати шта се тачно наслеђује из
базне класе, а шта не, као и шта јесте, а шта није из базне класе видљиво,
односно доступно у изведеној класи. Значи, наслеђивање чланова класа и
ограничавање доступности чланова класа нису синоними - неки члан базне класе
може да буде наслеђен у изведеној класи, али због модификатора приступа
потпуно невидиљив у изведеној класи!

Из базне класе не наслеђују се конструктори за инстанцирање и статички
конструктори, као ни финализатори. Сви остали чланови базне класе се наслеђују,
што не значи да су сви остали чланови базне класе видљиви у изведеној класи.
Приватни чланови базне класе видљиви су у изведеној класи, само ако је изведена
класа угнежђена у базној класи - у осталим случајевима приватни чланови базне
класе нису видљиви у изведеној класи.

У следећем примеру изведена класа `Izv` угнежђена је у базној класи `Baz`.
Приватни члан `broj` класе `Baz` наслеђује се и видљив је у класи `Izv`:

```cs
public class Baz
{
    private int broj = 10;

    public class Izv : Baz
    {
        public int VratiBroj()
        {
            return broj;
        }
    }
}
```

У главном програму можеш инстанцирати објекат изведене класе и приступити
приватном члану базне класе:

```cs
Baz.Izv i1 = new Baz.Izv();
Console.WriteLine(i1.VratiBroj());
```

Међутим, ако изведена класа није угнежђена, приватни члан базне класе биће
наслеђен, али неће бити видљив у изведеној класи:

```cs
public class Baz
{
    private int broj = 10;
}

public class Izv : Baz
{
    public int VratiBroj()
    {
        return broj;
    }
}
```

Овај кôд ће одмах проузроковати грешку
`Error CS0122: 'Baz.broj' is inaccessible due to its protection level`.

Сада када је ти јасна разлика између наслеђивања и видљивости чланова, можеш да
размислиш о хијерархији класа коју би креирао правећи софтве за неку компанију
или организацију.

Једноставан пример хијерархије класа за твоју школу могао би да изгледа овако:

<pre class="mermaid">
    classDiagram
    Osoba <|-- Učenik
    Osoba <|-- Zaposleni
    Zaposleni <| -- Nastavnik
    Zaposleni <| -- Osoblje
    Osoba : string ime
    Osoba : int gRodj
    Osoba : -void prikazImena()
    Osoba : -void prikazGodine()
    Osoba : void prikazPodataka()
    class Učenik{
        string odeljenje
        -void prikazOdeljenja()
        void prikazUcenika()
    }
    class Zaposleni{
        int staz
        string strucna
        -void prikazStaza()
        -void prikazStrucne()
        void prikazZaposlenog()
    }
    class Nastavnik{
        string predmet
        -void prikazPredmeta()
        void prikazNastavnika()
    }
    class Osoblje{
        string posao
        -void prikazPosla()
        void prikazOsoblja()
    }
</pre>
<script type="module">
    import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
    mermaid.initialize({ startOnLoad: true });
</script>

Школу похађају ученици, а у школи раде запослени. Запослени могу бити
наставници или ненаставно особље. Заједничко за све особе у школи је да имају
име и годину рођења. За ученике је битно навести у којем су одељењу. За све
запослене битно је навести године стажа и степен стручне спреме. За наставника
поред тога треба навести и предмет који предаје, а за ненаставно особље који
посао обављају. Посматрај сада једну изведену класу на дијаграму, на пример
класу `Nastavnik`. Она је изведена из класе `Zaposleni`, а класа `Zaposleni` из
класе `Osoba`.

У изведеној класи `Nastavnik`, наслеђени су чланови класа који се у хијерархији
наслеђивања налазе изнад ње, онако како је описано на почетку лекције. Због
модификатора приступа `private` неки наслеђени чланови неће бити доступни.
Програм којим се демонстрира наслеђивање за класу `Nastavnik` могао би да
изгледа овако:

```cs
using System;

class Osoba
{
    public string ime;
    public int gRodj;

    public Osoba(string Ime, int GRodj)
    {
        ime = Ime;
        gRodj = GRodj;
    }

    private void prikazImena()
    {
        Console.WriteLine("Ime i prezime: {0}.", ime);
    }

    private void prikazGodine()
    {
        Console.WriteLine("Godina rođenja: {0}.\n", gRodj);
    }

    public void prikazPodataka()
    {
        prikazImena();
        prikazGodine();
    }
}

class Zaposleni : Osoba
{
    public int staz;
    public string strucna;

    public Zaposleni(string Ime, int GRodj, int Staz, string Strucna) :
        base(Ime, GRodj)
    {
        staz = Staz;
        strucna = Strucna;
    }

    private void prikazStaza()
    {
        Console.WriteLine("Godine staza: {0}.", staz);
    }
    private void prikazStrucne()
    {
        Console.WriteLine("Strucna sprema: {0}.", strucna);
    }

    public void prikazZaposlenog()
    {
        prikazPodataka();
        prikazStaza();
        prikazStrucne();
    }
}

class Nastavnik : Zaposleni
{
    public string predmet;

    public Nastavnik(string Ime, int GRodj, int Staz, string Strucna, string Predmet) : 
        base(Ime, GRodj, Staz, Strucna)
    {
        predmet = Predmet;
    }

    private void prikazPredmeta()
    {
        Console.WriteLine("Predmet: {0}.", predmet);
    }

    public void prikazNastavnika()
    {
        prikazZaposlenog();
        prikazPredmeta();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Nastavnik n1 = new Nastavnik("Velimir Radlovacki", 1976, 23, "VII", "Programiranje");
        n1.prikazPodataka(); // javna metoda u klasi Osoba
        n1.prikazZaposlenog(); // javna metoda klasi Zaposleni
        n1.prikazNastavnika(); // javna metoda klasi Nastavnik
    }
}
```

Дефинисани су чланови класе `Osoba` као јавни или као приватни. Класа
`Zaposleni` наслеђена је из класе `Osoba`, што је приликом дефиниције класе
`Zaposleni` наведено овако: `Zaposleni : Osoba`. Пошто се конструктор не
наслеђује, у конструктору класе `Zaposleni` наведена је кључна реч `base` са
потребним параметрима конструктора базне класе `Osoba`. Исти је поступак
дефинисања класе `Nastavnik` из класе `Zaposleni`.
