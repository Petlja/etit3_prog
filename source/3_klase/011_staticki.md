# Статички чланови и статичке класе

До сада си научио да се у програмском језику C# користе кључне речи `public`,
и `private` као модификатори приступа. Поред ових кључних речи, у дефиницијама
чланова класа појављивала се и кључна реч `static`, на пример у свакој
дефиницији методе `static void Main()`. Чему онда служи кључна реч `static`,
ако није модификатор приступа?

Кључну реч `static` користићеш у више ситуација. Најчешће ће то бити приликом
дефинисања чланова класе који припадају класи, али не и инстанци те класе.
Овакви чланови класе називају се статички чланови класе. Супротно, чланови
класе који припадају инстанци класе називају се нестатички чланови класе.
Ако је поље, метод, својство или догађај декларисан као `static`, онда припада
класи, а не и инстанци објеката те класе. То значи и да се статичким члановима
може приступити без креирања инстанце класе.

На пример, ако су у класи `Brojanje` дефинисана два статичка члана, поље
`brojac` и метода `Povecaj()`...

```cs
public class Brojanje
{
    public static int brojac = 0;

    public static void Povecaj()
    {
        brojac++;
    }
}
```

...онда се тим статичким члановима може приступити директно, без инстанцирања
објекта класе `Brojac`:

```cs
Brojanje.brojac = 5;
Console.WriteLine(Brojanje.brojac);    // 5
Brojanje.Povecaj();
Console.WriteLine(Brojanje.brojac);    // 6
```

То значи и да статички чланови класе не могу директно да користе нестатичке
чланове класе. У следећем примеру...

```cs
public class Brojanje
{
    public int x = 0;
    public static int brojac = x;

    public static void Povecaj()
    {
        Console.WriteLine(x);
        brojac++;
    }
}
```

дефинисана су три члана, нестатичко поље `x`, статичко поље `brojac` и метода
`Povecaj()`. Прва грешка направљена је у статичком пољу `brojac` где је
референцирано статичко поље `x`:

```text
CS0236: A field initializer cannot reference the non-static field, method, or property 'Brojanje.x'
```

Друга грешка направљена је у телу методе `Povecaj()` где се опет рефенцира
статичко поље `x`:

```text
CS0120: An object reference is required for the non-static field, method, or property 'Brojanje.x'
```

Такође, статичке чланове класе не можеш користити у инстанци класе, јер
припадају само класи, а не и инстанци класе. У првом примеру...

```cs
public class Brojanje
{
    public static int brojac = 0;

    public static void Povecaj()
    {
        brojac++;
    }
}
```

...поље `brojac` и метода `Povecaj()` су статички чланови класе. Ако креираш
инстанцу класе `Brojanje`, онда у креираном објекту не можеш користи наведене
статичке чланове:

```cs
Brojanje x = new Brojanje();
Console.WriteLine(x.brojac);
Console.WriteLine(x.Povecaj());
```

Након инстанцирања објекта `x` класе `Brojanje` направљене су две грешке - прва
приликом покушаја приступа статичком пољу `brojac`...

```text
CS0176: Member 'Brojanje.brojac' cannot be accessed with an instance reference; qualify it with a type name instead
```

...и друга приликом покушаја приступа статичкој методи `Povecaj()`

```text
CS0176: Member 'Brojanje.Povecaj()' cannot be accessed with an instance reference; qualify it with a type name instead
```

## Статичке класе

Поред чланова класе и саме класе могу бити статичке ако приликом декларације
класе наведеш кључну реч `static`. Статичке класе не могу бити инстанциране и
могу садржати само статичке чланове. Тако класу `Brojanje` из претходног
примера можеш слободно декларисати као статичку класу, јер садржи само два
статичка члана:

```cs
public static class Brojanje
{
    public static int brojac = 0;

    public static void Povecaj()
    {
        brojac++;
    }
}
```

Овим поступком ћеш и даље моћи да користиш статичке чланове класе као и раније:

```cs
Brojanje.brojac = 5;
Console.WriteLine(Brojanje.brojac);    // 5
Brojanje.Povecaj();
Console.WriteLine(Brojanje.brojac);    // 6
```

Међутим, ако покушаш да инстанцираш објекат статичке класе...

```cs
Brojanje x = new Brojanje();
```

компајлер ће одмах јавити грешке:

```text
CS0723: Cannot declare a variable of static type 'Brojanje'
CS0712: Cannot create an instance of the static class 'Brojanje'
```
