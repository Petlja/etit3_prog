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

## Питање 9

Дат је кôд којим су креиране три класе у ланцу наслеђивања. Унутар сваке класе
декларисан је по један `private`, `public` и `protected` атрибут. У методи
`Main()` класе `Program` креиран је објекат `s` класе `Sin` (`Sin s = new Sin();`).

```cs
public class Deda
{
    private double penzija;
    protected string adresa;
    public string ime;
}

public class Otac : Deda
{
    private double plata;
    protected string firma;
    public string struka;
}

public class Sin : Otac
{
    private double prosek;
    protected int razred;
    public string skola;
}
```

```{mchoice}
:answer1: adresa
:answer2: ime
:answer3: firma
:answer4: struka
:answer5: razred
:answer6: skola
:correct: 2,4,6

Штиклирај поља која ће бити видљива у креираном објекту `s` класе `Sin`.
```

## Питање 10

Дат је кôд којим су креиране три класе у ланцу наслеђивања.

```cs
public class Deda
{
    private double penzija;
    protected string adresa;
    public string ime;
}

public class Otac : Deda
{
    private double plata;
    protected string struka;
}

public class Sin : Deda
{
    public int razred;
}
```

```{mchoice}
:answer1: penzija
:answer2: adresa
:answer3: ime
:answer4: plata
:answer5: struka
:answer6: razred
:correct: 2,3,6

Имајући у виду класификаторе приступа пољима класа, заокружити бројеве испред
поља која ће бити видљива унутар класе `Sin`.
```

## Питање 11

```{mchoice}
:answer1: new
:answer2: virtual
:answer3: sealed
:answer4: override
:answer5: abstract
:answer6: base
:correct: 2,3,5

Да би наслеђени метод могао да се редефинише и тиме измени његова
функционалност у класама наследницама, у родитељској класи испред ознаке
повратног типа метода наводи се нека од понуђених кључних речи. Штиклирај
кључнe речи омогућавају редефинисање дефинисаног метода кроз ланац наслеђивања.
```

## Питање 12

Дефинисане су три класе:

```cs
class Program
{
    public static void Main(string[] args)
    {
        B b = new B();
        b.Metod(5);
        Console.WriteLine("b.i je " + b.CitajI());
    }
}

class A
{
    int i;

    public int CitajI()
    {
        return i;
    }

    public void Metod(int i)
    {
        this.i = i;
    }
}

class B : A
{
    public void Metod(string s)
    {
        Console.WriteLine(s);
    }
}
```

```{mchoice}
:answer1: Програм има грешку, јер је метод Metod(int i) надјачан (предефинисан) са различитим потписом у класи B.
:answer2: Програм има грешку, јер се b.Mетод(5) не може позвати пошто је метод Metod(int i) заклоњен у класи B.
:answer3: Програм има грешку због b.i, јер је поље i неприступачно из класе B.
:answer4: Програм нема грешке, јер наслеђени метод класе А, Metod(int i) није надјачан у класи B, већ је дефинисан преоптерећен метод Metod(string s).
:correct: 4

Анализирај дати кôд и одредити да ли је кôд исправно написан. Означи исказ који
даје информацију о тачности кода.
```

## Питање 13

Дефинисане су две класе:

```cs
class Program
{
    public static void Main(string[] args)
    {
        Object a1 = new KlasaA();
        Object a2 = new KlasaA();
        Console.WriteLine(a1.Equals(a2));
    }
}

class KlasaA
{
    int x;
    public bool Equals(KlasaA a)
    {
        return this.x == a.x;
    }
}
```

```{mchoice}
:answer1: Програм има грешку, јер се изразом a1.Equals(a2) проверава једнакост објеката а1 и а2 различитог типа од Object.
:answer2: Програм има грешку, јер се једнакост објеката а1 и а2 типа KlasaА проверава изразом а1 == а2.
:answer3: Програм се извршава без грешке и приказује се true на екрану.
:answer4: Програм се извршава без грешке и приказује се false на екрану.
:correct: 4

Анализирај дати кôд и одредити да ли је кôд исправно написан. Означи исказ који
даје информацију о тачности кода.
```

## Питање 14

Дефинисане су две класе:

```cs
class Program
{
    public static void Main(string[] args)
    {
        KlasaA a1 = new KlasaA();
        KlasaA a2 = new KlasaA();
        Console.WriteLine(a1.Equals(a2));
    }
}

class KlasaA
{
    int x;
    public bool Equals(KlasaA a)
    {
        return this.x == a.x;
    }
}
```

```{mchoice}
:answer1: Програм има грешку, јер се изразом a1.Equals(a2) проверава једнакост објеката а1 и
а2 различитог типа од Object.
:answer2: Програм има грешку, јер се једнакост објеката а1 и а2 типа KlasaА проверава
изразом а1 == а2.
:answer3: Програм се извршава без грешке и приказује се true на екрану.
:answer4: Програм се извршава без грешке и приказује се false на екрану.
:correct: 3

Анализирај дати кôд и одредити да ли је кôд исправно написан. Означи исказ који
даје информацију о тачности кода.
```
