# Заједнички чланови класе

У контексту објектно-оријентисаног програмирања, термин "заједнички чланови
класе" (енгл. *Common Members*) односи се на чланове класе (понајвише поља и
методе) који су доступни свим класама које наслеђују базну класе. То значи да
су ти чланови дефинисани у базној класи и доступни су у свим изведеним класама,
без потребе да се поново дефинишу у свакој од њих.

```cs
public class Ucenik
{
    // Заједничкa поља
    public string ime { get; set; }
    public string prezime { get; set; }

    // Заједничка метода
    public void Ispisi()
    {
        Console.WriteLine(ime + prezime);
    }
}

public class Cas : Ucenik
{
    // Специфични члан класе Час
    public string predmet { get; set; }

    // Специфична метода класе Час
    public void SkolskiCas()
    {
        Console.WriteLine(ime + prezime + " pohadja " + predmet);
    }
}

public class Ocena : Ucenik
{
    // Специфични члан класе Оцена
    public int ocena { get; set; }

    // Специфична метода класе Оцена
    public void SkolskiCas()
    {
        Console.WriteLine(ime + prezime + " dobio je ocenu " + ocena.ToString());
    }
}
```

Већ је напоменуто да, у програмском језику C#, све класе наслеђују, директно
или индиректно, класу `System.Object`, која је базна класа свих *.NET* типова.
`System.Object` пружа неколико заједничких чланова који су доступни свим
типовима који га наслеђују:

* `Equals()`: Ова метода се користи за поређење објекта са другим
објектом. Основна имплементација проверава да ли две референце упућују на исти
објекат.

```cs
public virtual bool Equals(object obj);
```

* `ReferenceEquals`: Ова метода се користи за поређење две референце на
објекат.

```cs
public static bool ReferenceEquals (object objA, object objB);
```

* `GetHashCode()`: Ова метода враћа хеш код објекта. Хеш код је број који се
користи за брзо претраживање и поређење објеката у хеш табелама.

```cs
public virtual int GetHashCode();
```

* `GetType()`: Ова метода враћа тип објекта. Корисна је када су ти потребне
информације о типу објекта у време извршавања програма.

```cs
public Type GetType();
```

* `ToString()`: Ова метода враћа стринг који представља објекат. Основна
имплементација враћа име типа објекта.

```cs
public virtual string ToString();
```

* `Finalize()`: Ова метода се позива пре него што објекат буде сакупљен од
стране сакупљача смећа (енгл. *garbage collector*). Ово је место за чишћење
неуправљаних ресурса које објекат можда користи.

```cs
protected virtual void Finalize();
```

* `MemberwiseClone()`: Овај метод прави плитку копију текућег објекта. То значи
да копира све вредности чланова, али не и објекте на које они могу упућивати.

```cs
protected object MemberwiseClone();
```

О плитким и дубоким копијама учио си у лекцији
[Конструктор копије](../3_klase/022_konstruktor_kopije.md), а сви ови чланови класе
`Object` описани су детаљно у званичној
[документацији](https://learn.microsoft.com/en-us/dotnet/api/system.object?view=netframework-4.8).
