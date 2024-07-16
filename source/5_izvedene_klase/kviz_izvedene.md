# Квиз

## Питање 1

Наведени су кључне речи које одређују типове класа:

1. `abstract`
2. `sealed`
3. `partial`
4. `interface`

```{fitb}
:answer: "3,1,4,2"

У празнине испед описа упиши цифру редног броја под којим је наведен одговарајући тип класе.

|blank| - класа која се простире у више фајлова. |blank| - класа садржи само
декларације метода, али не и дефиницију (тело) методе. |blank| - класа која се
не може инстанцирати. |blank| - класа из које се не може наслеђивати.
```

## Питање 2

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

У празнине упиши шта би се исписало у конзоли након извршавања наведене методе.

`x.Poruka1();` исписало би се |blank|,
`x.Poruka2();` исписало би се |blank|,
`y.Poruka1();` исписало би се |blank| и
`y.Poruka2();` исписало би се |blank|.
```

## Питање 3

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

Kреирани су објекти ових класа и из њих позвана метода `Metod()`. У празнине
упиши шта метод `Metod()` враћа при позиву из наведених објеката.

`KlasaA a = new KlasaA(); a.Metod();` враћа вредност |blank|,
`KlasaB b = new KlasaВ(); b.Metod();` враћа вредност |blank|,
`KlasaA bb = new KlasaB(); bb.Metod();` враћа вредност |blank|,
`KlasaC c = new KlasaC(); c.Metod();` враћа вредност |blank|,
`KlasaB cc = new KlasaC(); cc.Metod();` враћа вредност |blank| и
`KlasaA ccc = new KlasaC(); ccc.Metod();` враћа вредност |blank|.
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
:answer: "10,200,250"

У празнине упиши шта метод `Uvecaj()` враћа при позиву из наведених објеката.

`r.Uvecaj();` враћа |blank|,
`rDin.Uvecaj();` враћа |blank| и
`rDev.Uvecaj();` враћа |blank|.
```

## Питање 5

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

## Питање 6

Дефинисане су три класе:

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            KlasaB b = new KlasaB();
            b.Print();
        }
    }

    class KlasaA
    {
        string s;
        public KlasaA(string s) { this.s = s; }
        public void Print() { Console.WriteLine(this.s); }
    }

    class KlasaB : KlasaA { }
}
```

```{mchoice}
:answer1: Програм има грешку, јер KlasaB нема подразумевани конструктор KlasaB().
:answer2: Програм има грешку јер KlasaB има подразумевани конструктор, док родитељска KlasaА нема такав конструктор. Програм би радио без грешке уколико би се уклонио конструктор са параметрима из KlasaА.
:answer3: Програм има грешку која се може отклонити уколико би се у KlasaА експлицитно додао конструктор без параметара KlasaА().
:answer4: Програм нема грешку, извршава се, али се на конзоли ништа не исписује јер је поље s добило подразумевану вредност String.Empty.
:correct: 2,3

Анализирај дате класе и процени који су од понуђених исказа тачни. Заокружи
бројеве испред очекиваних одговора.
```

## Питање 7

Дат је кôд програма који садржи објекте две класе у којима је дефинисан метод
`ТoString()`.

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            Object a = new Klasa();
            Object obj = new Object();
            Console.WriteLine(a);
            Console.WriteLine(obj);
        }
    }
}

class Klasa
{
    int x;
    public override string ToString() { return "x u A je " + x; }
}
```

```{mchoice}
:answer1: Програм има грешку, јер наредбу Console.WriteLine(a) треба заменити наредбом Console.WriteLine(a.ТoString()).
:answer2: Приликом извршавања наредбе Console.WriteLine(a), програм позива се метод ТoString() наслеђен из класе Object.
:answer3: Приликом извршавања наредбе Console.WriteLine(a), програм позива метод ТoString() из класе Klasa.
:answer4: Приликом извршавања наредбе Console.WriteLine(obj), програм позива метод ТoString() из класе Object.
:correct: 3,4

Анализирај кôд датог програма и одреди који су од датих исказа тачни. Заокружи
бројеве испред очекиваних одговора.
```

## Питање 8

```{mchoice}
:answer1: Readonly својства.
:answer2: Заштићени чланови класа.
:answer3: Својства.
:answer4: Приватни чланови класа.
:answer5: Конструктор класе.
:correct: 5

Заокружи број испред наведеног члана класе који се ни под којим условима НЕ
наслеђује из родитељске класе у изведену класу.
```
