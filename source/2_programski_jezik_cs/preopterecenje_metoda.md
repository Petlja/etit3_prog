# Преоптерећење метода

Преоптерећење метода (енгл. *method overloading*), односно преклапање имена
функција, у програмском језику C# је техника која омогућава дефинисање више
метода са истим именом унутар исте класе, али са различитим скупом параметара.
Ово омогућава да један метод пружи различите функционалности у зависности од
броја или типа аргумената који су му прослеђени. Неки основни аспекти
преоптерећења метода могу се представити кроз неколико случаја, када се
креирају методе са истим именом које имају:

* различите типове параметара,
* различит број параметара,
* различит редослед параметара и
* комбинације различитих типова, броја и редоследа параметара.

## Преоптерећене методе са различитим типовима параметара

Једноставан пример метода са истим именом које имају различите типове
параметара могу бити методе за испис прослеђеног аргумента у конзоли:

```cs
using System;

class Program
{
    static void Stampaj(int broj)
    {
        Console.WriteLine("Broj: " + broj);
    }

    static void Stampaj(string poruka)
    {
        Console.WriteLine("Poruka: " + poruka);
    }

    static void Main()
    {
        Stampaj(5);                  // Broj: 5
        Stampaj("Hello, World!");    // Poruka: Hello, World!
    }
}
```

У овом примеру, у класи `Program` дефинисане су две статичке методе са истим
именом `Stampaj`. Ако је прослеђени аргумент типа `int` извршиће се метода која
има параметар типа `int`, односно, ако је прослеђени аргумент типа `string`
извршиће се метода која има параметар типа `string`.

## Преоптерећене методе са различитим бројем параметара

Једноставан пример метода са истим именом које имају различит број
параметара могу бити методе за испис прослеђеног аргумента у конзоли једанпут
или `n` број пута, где је `n` прослеђен као други аргумент:

```cs
using System;

class Program
{
    static void Stampaj(string poruka)
    {
        Console.WriteLine("Poruka: " + poruka);
    }
    
    static void Stampaj(string poruka, int n)
    {
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine("Poruka: " + poruka);
        }
    }
    
    static void Main()
    {
        Stampaj("Hello, World!");       // Poruka: Hello, World!
        
        Stampaj("Hello, World!", 3);    // Poruka: Hello, World!
    }                                   // Poruka: Hello, World!
}                                       // Poruka: Hello, World!
```

И у овом примеру, у класи `Program` дефинисане су две статичке методе са истим
именом `Stampaj`. Ако је прослеђен један аргумент извршиће се метода која има
један параметар, односно, ако су прослеђена два аргумента извршиће се метода
која има два параметра.

## Преоптерећене методе са различитим редоследом параметара

Једноставан пример метода са истим именом које имају различит редослед
параметара могу бити функције за испис различитих порука на основу редоследа
прослеђених аргумената:

```cs
using System;

class Program
{
    static void Stampaj(int n, string ime)
    {
        Console.WriteLine("Takmicar broj " + n + " zove se " + ime + ".");
    }

    static void Stampaj(string ime, int n)
    {
        Console.WriteLine("Takmicar " + ime + " osvojio je " + n + " poena.");
    }

    static void Main()
    {
        Stampaj(1, "Velimir Radlovacki");  // Takmicar broj 1 zove se Velimir Radlovacki.
        Stampaj("Velimir Radlovacki", 80); // Takmicar Velimir Radlovacki osvojio je 80 poena.
    }
}
```

## Преоптерећене методе са различитим типовима, бројем и/или редоследом параметара

Ради веће флексибилности, по потреби, можеш и комбиновати технике преоптерећења
метода из претходна три примера.

```cs
using System;

class Program
{
    static void Stampaj(string ime)
    {
        Console.WriteLine("Na takmicenju ucestvuje takmicar " + ime + ".");
    }

    static void Stampaj(int n)
    {
        Console.WriteLine("Na takmicenju ucestvuje " + n + " takmicara.");
    }

    static void Stampaj(int n, string ime)
    {
        Console.WriteLine("Takmicar broj " + n + " zove se " + ime + ".");
    }

    static void Stampaj(string ime, int n)
    {
        Console.WriteLine("Takmicar " + ime + " osvojio je " + n + " poena.");
    }

    static void Main()
    {
        Stampaj("Velimir Radlovacki");     // Na takmicenju ucestvuje takmicar Velimir Radlovacki.
        Stampaj(20);                       // Na takmicenju ucestvuje 20 takmicara.
        Stampaj(1, "Velimir Radlovacki");  // Takmicar broj 1 zove se Velimir Radlovacki.
        Stampaj("Velimir Radlovacki", 80); // Takmicar Velimir Radlovacki osvojio je 80 poena.
    }
}
```

Из претходних примера можеш закључити да је преоптерећење метода важан концепт
у објектно-оријентисаном програмирању који помаже програмерима да створе
флексибилније и једноставније приступе методама, односно да користе једно име
методе за различите, али повезане функционалности. Размисли само колико би
сложенији био кôд у програмском језику C за реализацију сличне функционалности.

Преоптерећење метода у програмском језику C# је засновано искључиво на
параметрима метода. Повратни тип метода није део потписа метода у контексту
преоптерећења, па се методе не могу разликовати само по повратном типу.
