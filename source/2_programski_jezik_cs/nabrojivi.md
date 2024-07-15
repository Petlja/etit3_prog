# Набројиви тип

Набројиви тип (енгл. *enumeration type*, *enum type*) је тип дефинисан скупом
именованих константи основног интегралног нумеричког типа. Слично као у
програмском језику C, за дефинисање набројивог типа користићеш кључну реч
`enum` и имена чланова:

```cs
enum GodisnjeDoba
{
    Prolece,
    Leto,
    Jesen,
    Zima
}
```

Подразумевана нумеричке вредности константи су типа `int`, `0` за `Prolece`,
`1` за `Leto`, `2` за `Jesen` и `3` за `Zima`. Тип и вредности можеш и сам да
наведеш, ако не желиш да то буду подразумеване вредности типа `int`. На пример:

```cs
enum GodisnjeDoba : ushort
{
    Prolece = 10,
    Leto = 20,
    Jesen = 30,
    Zima = 40
}
```

Иницијализацију може бити и делимична. У следећем примеру...

```cs
enum Nastava { sep = 9, okt, nov, dec, jan = 1, feb, mar, apr, maj, jun };
```

…елемент `sep` иницијализован је са `9`, потом је елементу `okt` додељено `10`,
елементу `nov` `11`, елементу `dec` `12`, па је елемент `jan` иницијализован
са `1`, елементу `feb` додељено је `2`, елементу `mar` `3` итд.

Дозвољено је и да различити елементи набројивог типа имају исту вредност. У
следећем примеру:

```cs
enum StanjeServera { ukljucen = 1, onlajn = 1, iskljucen = 0, oflajn = 0, greska = 0 };
```

...јединицама су дефинисана стања сервера `ukljucen` и `onlajn`, а нулама стања
`iskljucen`, `oflajn` и `greska`.

## Конверзије набројивих типова

За било који дефинисан набројив тип могућа је експлицитна конверзија у његов
основни интегрални нумерички тип. На пример:

```cs
enum GodisnjeDoba
{
    Prolece,
    Leto,
    Jesen,
    Zima
}

static void Main()
{
    GodisnjeDoba g = GodisnjeDoba.Zima;
    Console.WriteLine(g);         // Zima
    Console.WriteLine((int)g);    // 3
}
```

## Операције над вредностима набројивог типа

Над вредностима набројивог типа можеш да користиш следеће операторе:

* операторе једнакости и поређења `==`, `!=`, `<`, `>`, `<=`, `>=`,
* бинарне операторе `+` и `-`,
* енумерацијске логичке операторе `^`, `&`, `|`,
* битски оператор за израчунавање комплемента `~`,
* операторе за инкремент `++` и декремент `--` и
* оператор `sizeof`.

```cs
enum GodisnjeDoba
{
    Prolece,
    Leto,
    Jesen,
    Zima
}

static void Main()
{
    GodisnjeDoba a = GodisnjeDoba.Prolece;
    Console.WriteLine(a);   // Prolece
    a++;
    Console.WriteLine(a);   // Leto
    
    GodisnjeDoba b = a + 2;
    Console.WriteLine(b);   // Zima
    
    Console.WriteLine(b > a ? "Vece" : "Nije vece");    // Vece
}
```
