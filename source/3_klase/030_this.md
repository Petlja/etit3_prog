# Кључна реч this

У програмском језику C#, кључна реч `this` има важну улогу и користи се у
различитим ситуацијама. У овој лекцији фокус ће бити на њеној употреби у
класама.

Кључну реч `this` користићеш за референцирање тренутног објекта, односно
инстанце класе. Ова могућност је нарочито корисна када желиш да разликујеш поља
класе од параметара конструктора или метода који имају исто име. У следећем
примеру...

```cs
class Osoba
{
    private string ime;

    public Osoba(string ime)
    {
        this.ime = ime;
    }

    public void UnesiIme(string ime)
    {
        this.ime = ime;
    }

    public void IspisiIme()
    {
        Console.WriteLine("Ime: " + this.ime);
    }

    public string VratiIme()
    {
        return this.ime;
    }
}
```

...у класи `Osoba` више пута је употребљена кључна реч `this`:

* у конструктору, `this.ime` је поље класе, а `ime` је параметар конструктора,
* у методи `UnesiIme`, `this.ime` је поље класе, а `ime` је параметар методе,
* у методи `IspisiIme`, `this.ime` користи се за испис вредности поља `ime` и
* у методи `VratiIme`, `this.ime` користи се за враћање вредности поља `ime`.

Кључну реч `this` можеш користити и за позивање других конструктора унутар исте
класе, што може бити корисно за избегавање дуплирања кода. На пример:

```cs
class Osoba
{
    private string ime;
    private string mesto;
    private int pttBroj;

    public Osoba(string ime) : this(ime, "Nepoznato", 0)
    {

    }

    public Osoba(string ime, string mesto, int pttBroj)
    {
        this.ime = ime;
        this.mesto = mesto;
        this.pttBroj = pttBroj;
    }
}
```

У овом примеру у класи `Osoba` постоје два конструктора. Конструктором са три
параметра постављају се вредности свих поља. Конструктор са једним параметром
помоћу кључне речи `this` позива конструктор са три параметра, где се вредност
првог поља поставља кроз први параметар, вредност другог поља на `Nepoznato` и
вредност трећег поља на `0`.

Кључну реч `this` можеш користити да проследиш тренутни објекат као параметар
другим методама. На пример:

```cs
class Osoba
{
    private string ime;
    private string adresa;

    public Osoba(string ime, string adresa)
    {
        this.ime = ime;
        this.adresa = adresa;
    }

    public void PrikaziOsobu()
    {
        PrikaziPodatke(this);
    }

    private void PrikaziPodatke(Osoba osoba)
    {
        Console.WriteLine("Ime: " + osoba.ime);
        Console.WriteLine("Adresa: " + osoba.adresa);
    }
}
```

Као што је на почетку лекције написано, кључна реч `this` користи се у
различитим ситуацијама, па тако и приликом декларације индексера, приликом
дефинисања продужених метода итд., али ти случајеви излазе ван домена ове
лекције.

Важно је да запамтиш да кључну реч `this` треба да користиш у ситуацијама када
треба референцирати тренутни објекат, позивати други конструктор унутар исте
класе или прослеђивати објекат као параметар.
