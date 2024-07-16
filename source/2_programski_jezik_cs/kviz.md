# Квиз

## Питање 1

Дат је следећи кôд програма:

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(fun(5));
        }
        
        public int fun(int n)
        {
            return n;
        }
        
        public void fun(int n)
        {
            Console.WriteLine(n);
        }
    }
}
```

```{mchoice}
:answer1: Програм има грешку, јер се не може одредити коју верзију преоптерећеног метода fun() треба позвати.
:answer2: Програм има грешку, јер је друга верзија преоптерећеног метода fun() дефинисана али се нигде не позива.
:answer3: Програм се нормално извршава и у конзоли исписује 5 једанпут.
:answer4: Програм се нормално извршава и у конзоли исписује 5 двапут.
:correct: 1

Анализираj дати кôд и заокружи број испред очекиваног одговора.
```

## Питање 2

Дат је следећи кôд програма који формира и штампа елементе низа `а`:

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] a = new int[5];
            for (int i = 0; i < a.Length; i++) a[i] = i;
            Console.Write(a[i] + " ");
        }
    }
}
```

```{mchoice}
:answer1: Програм у конзоли исписује бројеве 0 1 2 3 4.
:answer2: Програм има грешку, јер ће у последњој наредби Console.Write методa Main покушати приступ непостојећем елементу а[5].
:answer3: Програм у конзоли исписује број 5.
:answer4: Програм има грешку, јер променљива i у последњој наредби Console.Write у методу Main неће имати дефинисану вредност.
:correct: 4

Анализирај дати кôд и процени шта ће се догодити након његовог извршавања. Заокружи број испред очекиваног одговора.
```

## Питање 3

Дата је декларација променљиве и низа:

```cs
int k;
int[ ] brojevi = {5, 12, 37, 7, 27, 33, 36};
```

На основу дате декларације одредити шта је резултат позива:

```cs
k = Array.BinarySearch(brojevi, 37);
```

```{mchoice}
:answer1: k=0, јер метод BinarySearch прво изврши сортирање низа у опадајућем редоследу, па онда тражи задату вредност.
:answer2: метод BinarySearch баца изузетак увек када је низ неуређен и програм "пуца".
:answer3: k=2, јер се тражени елемент налази на позицији 2.
:answer4: k добија неочекивану вредност, јер низ мора бити сортиран у растућем поретку пре позива методе BinarySearch.
:answer5: k=6, јер метод BinarySearch прво изврши сортирање низа у растућем редоследу, па онда тражи задату вредност.
:correct: 4

Заокружи број испред очекиваног одговора.
```

## Питање 4

Дата је декларација једне стринг и једне целобројне променљиве, као и део кода:

```cs
string str = "Primer";
int broj = 66;
Console.WriteLine(str + broj + 65);
Console.WriteLine(broj + 65 + str);
```

```{mchoice}
:answer1: Primer6665 131Primer
:answer2: Primer6665 6665Primer
:answer3: Primer131 131Primer
:answer4: PrimerBA BAPrimer
:correct: 1

Анализирај дати кôд и процени шта ће се приказати на екрану након његовог извршења. Заокружити број испред очекиваног одговора.
```

## Питање 5

Дат је кôд који дефинише рекурзивни метод:

```cs
public long fun(int n)
{
    return n * fun(n - 1);
}
```

```{mchoice}
:answer1: Резултат позива fun(3) je 1.
:answer2: Резултат позива fun(3) je 2.
:answer3: Резултат позива fun(3) je 6.
:answer4: Позив fun(3) изазива грешку јер производи бесконачан ланац позива истог метода fun(…).
:correct: 4

Анализирај дати кôд и одреди резултат извршавања задатог метода. Заокружити број испред очекиваног одговора.
```

## Питање 6

Дат је кôд који дефинише рекурзивни метод:

```cs
namespace TestPrimer
{
    class Program
    {
        static void Main(string[] args)
        {
            fun(2);
        }

        public static void fun(int n)
        {
            while (n > 1)
            {
                Console.Write((n - 1) + " ");
                fun(n - 1);
            }
        }
    }
}
```

```{mchoice}
:answer1: Програм у конзоли не исписује ништа.
:answer2: Програм у конзоли исписује 1 2 3.
:answer3: Програм у конзоли исписује 3 2 1.
:answer4: Програм у конзоли бесконачно исписује 1 1 1 1 1 ….
:answer5: Програм у конзоли бесконачно исписује 2 2 2 2 2 ….
:correct: 4

Анализирај дати кôд и одреди шта ће се исписати у конзоли. Заокружи број испред очекиваног одговора.
```

## Питање 7

Дат је рекурзивни метод који проверава да ли је неки стринг палиндром.

```cs
public static bool palindrom(String s)
{
    if (s.Length <= 1)
    {
        return true; // bazni slučaј
    }
    else
    {
        if (___________________)
        {
            return false;
        }
        else
        {
            return palindrom(s.Substring(1, s.Length - 2));
        }
    }
}
```

```{mchoice}
:answer1: s[0] != s[s.Length - 1]
:answer2: s[0] != s[s.Length]
:answer3: s[1] != s[s.Length - 1]
:answer4: s[1] != s[s.Length]
:correct: 1

Да би кôд био комплетиран потребно је допунити девети ред условом `if` наредбе. Заокружи број испред очекиваног одговора.
```

## Питање 8

Дат је рекурзивни метод који проверава да ли је неки стринг палиндром.

```cs
public static bool Palindrom(String s)
{
    return Palindrom(s, 0, s.Length - 1);
}

public static bool Palindrom(String s, int levi, int desni)
{
    if (desni <= levi)
    {
        return true; // bazni slucaj
    }
    else
    {
        if (s[levi] != s[desni])
        {
            return false;
        }
        else
        {
            return ___________________;
        }
    }
}
```

```{mchoice}
:answer1: Palindrom(s)
:answer2: Palindrom(s, levi, desni)
:answer3: Palindrom(s, levi + 1, desni - 1)
:answer4: Palindrom(s, levi + 1, desni)
:answer5: Palindrom(s, levi, desni - 1)
:correct: 3

Да би кôд био комплетиран потребно је допунити двадесети ред. Заокружи број испред очекиваног одговора.
```
