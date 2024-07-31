# Квиз

## Питање 1

Дефинисане су две класе:

```cs
public class Roditelj
{
    public virtual void Poruka1()
    {
        Console.WriteLine("R1");
    }
    
    public void Poruka2()
    {
        Console.WriteLine("R2");
    }
}

public class Dete : Roditelj
{
    public override void Poruka1()
    {
        Console.WriteLine("D1");
    }
    
    public new void Poruka2()
    {
        Console.WriteLine("D2");
    }
}
```

У класи `Program` инстанцирана су два објекта:

```cs
class Program
{
    static void Main()
    {
        Dete x = new Dete();
        Roditelj y = new Dete();
        // методе ...
    }
}
```

```{fitb}
:answer: "D1,D2,D1,R2"

У празнине упиши шта би се исписало у конзоли након извршавања методе...

`x.Poruka1();` исписало би се |blank|,
`x.Poruka2();` исписало би се |blank|,
`y.Poruka1();` исписало би се |blank| и
`y.Poruka2();` исписало би се |blank|.
```

## Питање 2

Дефинисане су три класе:

```cs
public class KlasaA
{
    public virtual int Metod()
    {
        return 10;
    }
}

public class KlasaB : KlasaA
{
    public override int Metod()
    {
        return 20;
    }
}

public class KlasaC : KlasaB
{
    public new int Metod()
    {
        return 30;
    }
}
```

```{fitb}
:answer: "10,20,20,30,20,20"

Креирани су објекти ових класа и из њих позвана метода `Metod()`. У празнине
упиши шта метод `Metod()` враћа при позиву из наведених објеката.

`KlasaA a = new KlasaA(); a.Metod();` враћа вредност |blank|,
`KlasaB b = new KlasaВ(); b.Metod();` враћа вредност |blank|,
`KlasaA bb = new KlasaB(); bb.Metod();` враћа вредност |blank|,
`KlasaC c = new KlasaC(); c.Metod();` враћа вредност |blank|,
`KlasaB cc = new KlasaC(); cc.Metod();` враћа вредност |blank| и
`KlasaA ccc = new KlasaC(); ccc.Metod();` враћа вредност |blank|.
```

## Питање 3

Дефинисане су три класе:

```cs
public class Racun
{
    public virtual int Uvecaj() { return 10; }
}

public class Dinarski : Racun
{
    public override int Uvecaj() { return 20 * base.Uvecaj(); }
}

public class Devizni : Dinarski
{
    public override int Uvecaj() { return 50 + base.Uvecaj(); }
}
```

У класи `Program` инстанцирана су три објекта:

```cs
class Program
{
    static void Main()
    {
        Racun r = new Racun();
        Racun rDin = new Dinarski();
        Racun rDev = new Devizni();
    }
}
```

```{fitb}
:answer: "10,200,250"

У празнине упиши шта метод `Uvecaj()` враћа при позиву из наведених објеката.

`r.Uvecaj();` враћа |blank|,
`rDin.Uvecaj();` враћа |blank| и
`rDev.Uvecaj();` враћа |blank|.
```

## Питање 4

Дефинисане су три класе:

```cs
public class Racun
{
    public virtual int Uvecaj() { return 10; }
}

public class Dinarski : Racun
{
    public override int Uvecaj() { return 20 * base.Uvecaj(); }
}

public class Devizni : Dinarski
{
    public override int Uvecaj() { return 50 + base.Uvecaj(); }
}
```

У класи `Program` инстанцирана су три објекта:

```cs
class Program
{
    static void Main()
    {
        Racun r = new Racun();
        Racun rDin = new Dinarski();
        Racun rDev = new Devizni();
    }
}
```

```{fitb}
:answer: "10,200,60"

У празнине упиши шта метод `Uvecaj()` враћа при позиву из наведених објеката.

`r.Uvecaj();` враћа |blank|,
`rDin.Uvecaj();` враћа |blank| и
`rDev.Uvecaj();` враћа |blank|.
```

## Питање 5

```{mchoice}
:answer1: Ако је у изведеној класи надјачана виртуелна метода базне класе, онда се у изведеној класи и даље може приступити виртуелној методи базне класе.
:answer2: Објекат типа базне класе не може да референцира објекат изведене класе.
:answer3: Објекат типа изведене класе може директно да референцира објекат базне класе.
:answer4: Кôд у којем је имплементирано надјачавање метода је флексибилан и модуларан, јер специфичности класа имплементира у њиховим методама.
:correct: 1,4

Штиклирај тачне исказе.
```
