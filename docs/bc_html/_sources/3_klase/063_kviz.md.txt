# Квиз

## Питање 1

```{mchoice}
:answer1: Назива се глобална променљива.
:answer2: Назива се статичка променљива.
:answer3: Назива се локална променљива.
:answer4: Назива се блоковска променљива.
:correct: 3

Како се назива променљива дефинисана унутар неког метода?
```

## Питање 2

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

Анализирај дати кôд и одреди резултат извршавања методе. Означи тачан исказ.
```

## Питање 3

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

Анализирај дати кôд и одреди шта ће се исписати у конзоли. Означи очекивани
одговор.
```

## Питање 4

```{mchoice}
:answer1: public void Print(params string[] niska, params double[] broj)
:answer2: public void Print(params double[] broj, string niska)
:answer3: public void params Print(double d1, double d2)
:answer4: public void Print(params double[] broj)
:answer5: public void Print(int n, params double[] broj)
:correct: 4,5

Дате су наредбе које дефинишу заглавље методе Print() са променљивим бројем
параметара. Одреди које од понуђених наредби исправне. Штиклирај очекиване
одговоре.
```

## Питање 5

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

Да би кôд био комплетиран потребно је допунити девети ред условом `if` наредбе.
Означи очекивани одговор.
```

## Питање 6

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

Да би кôд био комплетиран потребно је допунити двадесети ред.
Означи очекивани одговор.
```

## Питање 7

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

Анализираj дати кôд и означи очекивани одговор.
```
