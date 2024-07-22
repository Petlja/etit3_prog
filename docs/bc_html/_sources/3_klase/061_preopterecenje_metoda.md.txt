# Преоптерећење метода у класи

У литератури о програмском језику C# наићићеш на изразе преклапање метода и
преоптерећење метода - у питању су само различити преводи енглеског израза
*method overloading*. Ове изразе не требаш мешати са надјачавањем тј.
превладањем метода (енгл. *method overriding*) - у питању је потпуно различита
техника која се тиче наслеђивања и полиморфизна и која ће бити тема у поглављу
[Изведене класе](../5_izvedene_klase/index.md).

О преоптерећењу метода унутар једне класе учио си у претходном поглављу.
Наравно, преоптерећене методе се могу налазити и у засебној класи, а концепт
преоптерећења је исти - методе са истим именом које имају:

* различите типове параметара,
* различит број параметара,
* различит редослед параметара и
* комбинације различитих типова, броја и редоследа параметара.

## Преоптерећене методе са различитим типовима параметара

Једноставан пример метода са истим именом које имају различите типове
параметара могу бити методе за испис прослеђеног аргумента у конзоли:

```cs
using System;

public class Stampanje
{ 
    public void Stampaj(int broj)
    {
        Console.WriteLine("Broj: " + broj);
    }

    public void Stampaj(string poruka)
    {
        Console.WriteLine("Poruka: " + poruka);
    }
}

class Program
{
    static void Main()
    {
        Stampanje s = new Stampanje();
        s.Stampaj(5);                   // Broj: 5
        s.Stampaj("Hello, World!");     // Poruka: Hello, World!
    }
}
```

У овом примеру, у класи `Stampanje` дефинисане су две јавне методе са истим
именом `Stampaj`. У класи `Program` креиран је објекат `s` класе `Stampanje`.
Ако се из класе `Program` позове метода `s.Stampaj` са аргументом типа `int`,
онда ће извршити метода која има параметар типа `int`, односно, ако се позове
метода `s.Stampaj` са аргументом типа `string`, онда ће се извршити метода која
има параметар типа `string`.

## Преоптерећене методе са различитим бројем параметара

Једноставан пример метода са истим именом које имају различит број
параметара могу бити методе за испис прослеђеног аргумента у конзоли једанпут
или `n` број пута, где је `n` прослеђен као други аргумент:

```cs
using System;

public class Stampanje
{ 
    public void Stampaj(string poruka)
    {
        Console.WriteLine("Poruka: " + poruka);
    }

    public void Stampaj(string poruka, int n)
    {
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine("Poruka: " + poruka);
        }
    }
}

class Program
{
    static void Main()
    {
        Stampanje s = new Stampanje();
        s.Stampaj("Hello, World!");    // Poruka: Hello, World!
        s.Stampaj("Hello!", 3);    // Poruka: Hello!
                                   // Poruka: Hello!
                                   // Poruka: Hello!
    }
}
```

И у овом примеру, у класи `Stampanje` дефинисане су две јавне методе са истим
именом `Stampaj`. У класи `Program` креиран је објекат `s` класе `Stampanje`.
Ако се из класе `Program` позове метода `s.Stampaj` са једним аргументом
извршиће се метода која има један параметар, односно, ако се позове метода
`s.Stampaj` са два аргумента, извршиће се метода која има два параметра.

## Преоптерећене методе са различитим редоследом параметара

Једноставан пример метода са истим именом које имају различит редослед
параметара могу бити функције за испис различитих порука на основу редоследа
прослеђених аргумената:

```cs
using System;

public class Stampanje
{ 
    public void Stampaj(int n, string ime)
    {
        Console.WriteLine("Takmicar broj " + n + " zove se " + ime + ".");
    }

    public void Stampaj(string ime, int n)
    {
        Console.WriteLine("Takmicar " + ime + " osvojio je " + n + " poena.");
    }
}

class Program
{
    static void Main()
    {
        Stampanje s = new Stampanje();
        s.Stampaj(1, "Velimir Radlovacki");  // Takmicar broj 1 zove se Velimir Radlovacki.
        s.Stampaj("Velimir Radlovacki", 80); // Takmicar Velimir Radlovacki osvojio je 80 poena.
    }
}
```

И у овом примеру, у класи `Stampanje` дефинисане су две јавне методе са истим
именом `Stampaj`. У класи `Program` креиран је објекат `s` класе `Stampanje`.
Ако се из класе `Program` позове метода `s.Stampaj` са аргументима `int` и
`string` извршиће се прва метода, односно, ако се позове метода `s.Stampaj` са
аргументима `string` и `int` извршиће се друга метода.

## Преоптерећене методе са различитим типовима, бројем и/или редоследом параметара

Ради веће флексибилности, по потреби, можеш и комбиновати технике преоптерећења
метода из претходна три примера.

```cs
using System;

public class Stampanje
{ 
    public void Stampaj(string ime)
    {
        Console.WriteLine("Na takmicenju ucestvuje takmicar " + ime + ".");
    }

    public void Stampaj(int n)
    {
        Console.WriteLine("Na takmicenju ucestvuje " + n + " takmicara.");
    }

    public void Stampaj(int n, string ime)
    {
        Console.WriteLine("Takmicar broj " + n + " zove se " + ime + ".");
    }

    public void Stampaj(string ime, int n)
    {
        Console.WriteLine("Takmicar " + ime + " osvojio je " + n + " poena.");
    }
}

class Program
{
    static void Main()
    {
        Stampanje s = new Stampanje();
        s.Stampaj("Velimir Radlovacki");     // Na takmicenju ucestvuje takmicar Velimir Radlovacki.
        s.Stampaj(20);                       // Na takmicenju ucestvuje 20 takmicara.
        s.Stampaj(1, "Velimir Radlovacki");  // Takmicar broj 1 zove se Velimir Radlovacki.
        s.Stampaj("Velimir Radlovacki", 80); // Takmicar Velimir Radlovacki osvojio je 80 poena.
    }
}
```

У последњем примеру, у класи `Stampanje` дефинисане су четири јавне методе са
истим именом `Stampaj`. У класи `Program` креиран је објекат `s` класе
`Stampanje`. Ако се из класе `Program` позове метода `s.Stampaj` са аргументом
типа `int` извршиће се прва метода, ако се позове метода `s.Stampaj` са
аргументом типа `string` извршиће се друга метода, ако се позове метода
`s.Stampaj` са два аргумента `int` и `string` извршиће се трећа метода и ако се
позове метода `s.Stampaj` са два аргумента `string` и `int` извршиће се четврта
метода.

Из претходних примера можеш закључити да је преоптерећење функција важан
концепт у програмском језику C# који помаже програмерима да створе
флексибилнији и једноставнији приступ методама класе, омогућавајући корисницима
класа да користе једно име метода за различите, али повезане функционалности.

Преоптерећење функција у класи је засновано искључиво на параметрима метода.
Повратни тип метода није део потписа метода у контексту преклапања, па се
методе не могу разликовати само по повратном типу.
