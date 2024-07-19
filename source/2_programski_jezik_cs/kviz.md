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

Анализирај дати кôд и одреди шта ће се исписати у конзоли. Заокружи број испред очекиваног одговора.
```

## Питање 4

Дате су наредбе које дефинишу заглавље методе Print() са променљивим бројем параметара.

```{mchoice}
:answer1: public void Print(params string[] niska, params double[] broj)
:answer2: public void Print(params double[] broj, string niska)
:answer3: public void params Print(double d1, double d2)
:answer4: public void Print(params double[] broj)
:answer5: public void Print(int n, params double[] broj)
:correct: 4,5

Одреди које од понуђених наредби исправне. Штиклирај очекиване одговоре.
```

## Питање 5

```{mchoice}
:answer1: Локални и глобални.
:answer2: Процедурални и непроцедурални.
:answer3: Статички (класни) и нестатички (објектни).
:answer4: Спољашњи и унутрашњи.
:correct: 3

Какви могу бити чланови класе (поља и методе) у програмском језику C#?
```
