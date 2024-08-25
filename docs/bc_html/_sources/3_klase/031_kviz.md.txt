# Квиз

## Питање 1

У класи `Figura` дат је подразумевани конструктор и конструктор са 4 параметра...

```cs
public Figura() { }
public Figura(string ime, string boja, int pozX, int pozY) { }
```

...и написано је шест наредби помоћу којих су креирани објекти класе `Figura`:

```cs
Figura f = Figura("lovac", "beli", 7, 3);
Figura f = new Figura("beli", "lovac", 7, 3);
Figura f = new Figura();
Figura f = new Figura("lovac", 3, 7, "beli");
Figura f = new Figura("lovac", "beli", 3, 7);
Figura f = new Figura("lovac", "beli", 3);
```

```{mchoice}
:answer1: Прва наредба.
:answer2: Друга наредба.
:answer3: Трећа наредба.
:answer4: Четврта наредба.
:answer5: Пета наредба.
:answer6: Шеста наредба.
:correct: 2,3,5

Штиклирај исправно написане наредбе за креирање објекта класе `Figura`.
```

## Питање 2

```{mchoice}
:answer1: Подразумевани конструктор без параметара се увек аутоматски додаје класи.
:answer2: Подразумевани конструктор без параметара се класи аутоматски додаје уколико у њој није експлицитно дефинисан ниједан конструктор.
:answer3: У класи се мора експлицитно дефинисати бар један конструктор.
:answer4: Конструктори немају тип резултата, чак ни void.
:correct: 2,4

Дати су искази који дефинишу конструктор. Штиклирај тачне исказе.
```

## Питање 3

Дата је дефиниција класе која се састоји од два конструктора, једне методе и
поља `x`. У дефиницији се користи службена реч `this`.

```cs
    class TestPrimer
    {
        public double x;

        public TestPrimer(double x)
        {
            this.Fun();
            this.x = x;
        }

        public TestPrimer()
        {
            Console.WriteLine("Podrazumevani konstruktor");
            this(23);
        }

        public void Fun()
        {
            Console.WriteLine("Poziv metoda fun()");
        }
    }
```

```{mchoice}
:answer1: this.Fun() у конструктору TestPrimer(double x) може се поједноставити и заменити само са Fun().
:answer2: this.x у конструктору TestPrimer(double x) може се поједноставити и заменити само са x.
:answer3: позив конструктора this(23) унутар другог конструктора TestPrimer() је прво што се извршава и мора се писати одмах после декларације public TestPrimer():this(23).
:answer4: this(23) у конструктору Test() мора се заменити са прецизнијим изразом this(23.0).
:correct: 1,3

Анализирај дати кôд и процени тачност следећих исказа. Штиклирај тачне исказе.
```

## Питање 4

Дата је дефиниција класе која се састоји од два конструктора, методе и поља
`x` и `y`. У шестом реду дефинисан је конструктор са параметрима који формира
тачку са координатама `x` и `y`.

```cs
public class Point
{
    private double x, y;
    public Point() { x = 0; y = 0; }
    public void set(double xx, double yy) { x = xx; y = yy; }
    public Point(double x, double y) { ______________; }
}
```

```{mchoice}
:answer1: this.x=x; this.y=y;
:answer2: x=x; y=y;
:answer3: set(x,y);
:answer4: set(this.x,this.y);
:answer5: x=this.x; y=this.y;
:correct: 1,3

Штиклирај наредбе којима се може допунити дефиниција конструктора.
```

## Питање 5

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
:answer2: Приликом извршавања наредбе Console.WriteLine(a), програм позива метод ТoString() наслеђен из класе Object.
:answer3: Приликом извршавања наредбе Console.WriteLine(a), програм позива метод ТoString() из класе Klasa.
:answer4: Приликом извршавања наредбе Console.WriteLine(obj), програм позива метод ТoString() из класе Object.
:correct: 3,4

Анализирај кôд датог програма и одреди који су од датих исказа тачни. Штиклирај
очекиване одговоре.
```

## Питање 6

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
:answer1: Програм има грешку, јер се изразом a1.Equals(a2) проверава једнакост објеката а1 и а2 различитог типа од Object.
:answer2: Програм има грешку, јер се једнакост објеката а1 и а2 типа KlasaА проверава изразом а1 == а2.
:answer3: Програм се извршава без грешке и приказује се true на екрану.
:answer4: Програм се извршава без грешке и приказује се false на екрану.
:correct: 3

Анализирај дати кôд и одреди да ли је кôд исправно написан. Означи исказ који
даје информацију о тачности кода.
```

## Питање 7

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

## Питање 8

Дат је следећи кôд програма:

```cs
namespace TestPrimer
{
    class Test
    {
        int x;

        public Test(string s)
        {
            Console.WriteLine("Klasa Test");
        }

        static void Main(string[] args)
        {
            Test t = null;
            Console.WriteLine(t.x);
        }
    }
}
```

```{mchoice}
:answer1: Програм има грешку јер променљива x није иницијализована.
:answer2: Програм има грешку јер класа Test нема подразумевани конструктор.
:answer3: Програм има грешку јер се у некој класи не може декларисати променљива типа те исте класе, као што је то овде случај са променљивом t.
:answer4: Програм има грешку јер променљива t није иницијализована и има вредност null у моменту када се приказује поље t.x.
:answer5: Програм нема грешака и нормално се извршава, не приказујући ништа на екрану.
:correct: 4

Анализираj дати кôд и означи очекивани одговор.
```
