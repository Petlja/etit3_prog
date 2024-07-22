# Квиз

## Питање 1

```{mchoice}
:answer1: Readonly својства.
:answer2: Заштићени чланови класа.
:answer3: Својства.
:answer4: Приватни чланови класа.
:answer5: Конструктор класе.
:correct: 5

Означи члана класе који се ни под којим условима НЕ наслеђује из базне класе у
изведену класу.
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

## Питање 4

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

## Питање 5

Дефинисане су две класе и класа `Program` са методом `Main()`.

```cs
using System;
class A
{
    private int n = 10;
    public class B : A
    {
        private int m = 20;
        public void Print()
        {
            Console.WriteLine($"{n},{m}");
        }
    }
}
class Program
{
    static void Main()
    {
        A.B b = new A.B();
        b.Print();
    }
}
```

```{mchoice}
:answer1: Програм се неће компајлирати.
:answer2: Програм ће се успешно компајлирати и извршити.
:answer3: У изведеној класи `B` доступно је приватно поље `n` базне класе `А`.
:answer4: У изведеној класи `B` није доступно приватно поље `n` базне класе `А`, јер се приватни чланови не наслеђују.
:answer5: Није могуће инстанцирати објекат `b` јер за класу `A` није експлицитно наведен модификатор приступа. 
:answer6: У конзоли ће се исписати `10,20`.
:correct: 2,3,6

Штиклирај тачне исказе
```
