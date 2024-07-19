# Квиз

## Питање 1

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

## Питање 2

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

## Питање 3

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

## Питање 4

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

## Питање 5

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

## Питање 6

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

## Питање 7

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

## Питање 8

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

## Питање 9

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

## Питање 10

```{mchoice}
:answer1: извршава се само конструктор изведене класе.
:answer2: прво се извршава конструктор родитељске класе, али само ако је позван кључном речју base.
:answer3: обавезно се прво извршава конструктор изведене, а потом конструктор родитељске класе.
:answer4: обавезно се прво извршава конструктор родитељске, а потом конструктор изведене класе.
:correct: 4

Означи исказ који представља исправан наставак дате тврдње. При креирању
објеката изведене класе...
```

## Питање 11

```{mchoice}
:answer1: Службена реч base може послужити за позивање конструктора родитељске класе.
:answer2: Службена реч base може послужити за позивање приватних метода родитељске класе којима се другачије не може приступити.
:answer3: Службена реч base може послужити за позивање заклоњеног метода родитељске класе.
:answer4: Службена реч base може послужити за позивање заклоњеног поља родитељске класе.
:correct: 2

У програмском језику C# користи се службена реч `base`. Процени који од
наредних исказа, који дефинишу дату службену реч, НИЈЕ тачан. Означи очекивани
одговор.
```
