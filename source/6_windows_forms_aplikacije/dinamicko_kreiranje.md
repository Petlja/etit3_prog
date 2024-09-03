# Динамичко креирање контрола

На почетку поглавља поменуто је да контроле у *Windows Forms App*
*(.NET Framework)* пројектима можеш постављати на два начина:

* статички, односно помоћу дизајнера, током израде апликације (енгл.
*Design-Time*), или
* динамички, односно програмским кодом у току извршавања апликације (енгл.
*Run-Time*).

Динамичко креирање контрола је корисно у ситуацијама када није унапред познат
број или врста контрола потребних у апликацији или када се број или врста
контрола мења у зависности од акција корисника или неких других фактора.

Нека је задатак да креираш једноставну *Windows Forms App (.NET Framework)*
апликацију у којој корисник бира да ли жели да му се прикаже неки текст у
лабели или нека слика у оквиру за слике. Како не знаш унапред да ли ће корисник
одабрати опцију за приказ текста или опцију за приказ слике, не можеш унапред
поставити контролу у дизајнеру која ће да одговара избору корисника. Решење је
да динамички креираш ону контролу коју је корисник одабрао.

Наравно, решење може бити да поставиш обе контроле, сакријеш их, па прикажеш
ону коју је корисник одабрао, али онда твоја апликација непотребно креира
два објекта у меморији, уместо једног. Биће ситуација када је број контрола
које треба поставити велик и непредвидив, па сакривање статички постављених
контрола не може да буде решење.

Креирај *Windows Forms App (.NET Framework)* пројекат са формом димензија
640×480. У врху постави једну лабелу са текстом "Који програмски језик је 2000.
године дизајнирао Андерс Хејлсберг у компанији Microsoft?" Испод
постави два дугмета са текстом "Прикажи текст" и "Прикажи слику".

```{image} images/dinamicko-01.png
:scale: 100
:align: center
```

Ако корисник кликне на прво дугме, испод треба да се прикаже лабела са текстом
"Програмски језик C#", а друго дугме треба да постане онемогућено. Ако корисник
кликне на друго дугме, испод треба да се прикаже следећа слика...

![C# лого](https://upload.wikimedia.org/wikipedia/commons/d/d2/C_Sharp_Logo_2023.svg)

...а прво дугме треба да постане онемогућено.

Кликни на прво дугме и креирај догађај миша `Click`, па исто то уради и са
другим дугметом. У тексту задатка тражи се да кликом на прво дугме, друго дугме
треба да постане онемогућено и обрнуто - кликом на друго дугме, прво дугме треба
да постане онемогућено:

```cs
private void btnTekst_Click(object sender, EventArgs e)
{
    btnSlika.Enabled = false;
}

private void btnSlika_Click(object sender, EventArgs e)
{
    btnTekst.Enabled = false;
}
```

## Креирање инстанци контрола

У догађају `btnTekst_Click` потребно је да креираш инстанцу контроле коју желиш
да додаш - у овом случају инстанцу лабеле:

```cs
Label lblOdgovor = new Label();
```

У догађају `btnSlika_Click` потребно је да креираш инстанцу оквира за слику:

```cs
PictureBox pcbOdgovor = new PictureBox();
```

## Дефинисање својстава динамички креираних контрола

Након иницијализације, потребно је да дефинишеш својства динамички креираних
контрола. Пошто те контроле не постоје током дизајна програма, односно нису
видљиве у дизајнеру, својства мораш дефинисати у самом коду.

Својства које треба прво да подесиш су својство `Name` и својство `Location`
којим се одређује локација динамички креиране контроле на форми у односу на
горњи леви угао форме одређене *(X, Y)* координатама. Након тога можеш
дефинисати остала својства контроле.

У случају лабеле, поред својстава `Name` и `Location`, биће довољно да
дефинишеш својство `Text`, својство `Font` и својство `AutoSize`:

```cs
lblOdgovor.Name = "lblOdgovor";
lblOdgovor.Location = new Point(140, 160);
lblOdgovor.Text = "Програмски језик C#";
lblOdgovor.Font = new Font("Microsoft Sans Serif", 24);
lblOdgovor.AutoSize = true;
```

У случају оквира за слике, поред својстава `Name` и `Location`, биће довољно да
дефинишеш саму слику, па након тога дефинишеш својство `Image`, својство
`SizeMode` и својство `ClientSize`:

```cs
pcbOdgovor.Name = "pcbOdgovor";
pcbOdgovor.Location = new Point(200, 160);
Bitmap slika = new Bitmap("C_Sharp_Logo_2023.svg.png");
pcbOdgovor.Image = slika;
pcbOdgovor.SizeMode = PictureBoxSizeMode.StretchImage;
pcbOdgovor.ClientSize = new Size(205, 205);
```

## Додавање динамички креиране контроле на форму

Када си креирао инстанце жељених контрола и дефинисао њихова својства, потребно
је да те контроле додаш на форму користећи методу `Controls.Add()`.

Додавање динамички креиране лабеле `lblOdgovor` на форму изгледаће овако...

```cs
this.Controls.Add(lblOdgovor);
```

...односно, додавање динамички креираног оквира за слику `pcbOdgovor` на форму
изгледаће овако:

```cs
this.Controls.Add(pcbOdgovor);
```

На крају, креирање инстанце, дефинисање својстава и постављање лабеле на форму
изгледаће овако...

```cs
private void btnTekst_Click(object sender, EventArgs e)
{
    btnSlika.Enabled = false;
    Label lblOdgovor = new Label();
    lblOdgovor.Name = "lblOdgovor";
    lblOdgovor.Location = new Point(140, 160);
    lblOdgovor.Text = "Програмски језик C#";
    lblOdgovor.Font = new Font("Microsoft Sans Serif", 24);
    lblOdgovor.AutoSize = true;
    this.Controls.Add(lblOdgovor);
}
```

...односно, креирање инстанце, дефинисање својстава и постављање оквира за
слику на форму изгледаће овако:

```cs
private void btnSlika_Click(object sender, EventArgs e)
{
    btnTekst.Enabled = false;
    PictureBox pcbOdgovor = new PictureBox();
    pcbOdgovor.Name = "pcbOdgovor";
    pcbOdgovor.Location = new Point(200, 160);
    Bitmap slika = new Bitmap("C_Sharp_Logo_2023.svg.png");
    pcbOdgovor.SizeMode = PictureBoxSizeMode.StretchImage;
    pcbOdgovor.ClientSize = new Size(205, 205);
    pcbOdgovor.Image = slika;
    this.Controls.Add(pcbOdgovor);
}
```

Кликом на прво дугме, друго дугме постаће онемогућено, креираће се
инстанца контроле лабела са дефинисаним својствима и на крају, креирана
контрола биће постављена на форму:

```{image} images/dinamicko-02.png
:scale: 100
:align: center
```

Кликом на друго дугме, прво дугме постаће онемогућено, креираће се
инстанца контроле оквир за слику са дефинисаним својствима и на крају, креирана
контрола биће постављена на форму:

```{image} images/dinamicko-03.png
:scale: 100
:align: center
```

## Додавање догађаја динамички креираним компонентама

Нека је претходни задатак проширен још једним захтевом - када се кликне на
динамички креирану контролу `pcbOdgovor`, треба да се прикаже порука "Слика је
преузета са сајта wikimedia.org".

Питање је како дефинисати догађај клика на динамички креирану контролу, када та
контрола не постоји током дизајна? Одговор лежи у руковаоцима догађаја. Потребно
је да мануелно напишеш догађај клика на динамички креирану контролу, на пример
овако...

```cs
private void pcbOdgovor_Click(object sender, EventArgs e)
{
    MessageBox.Show("Слика је преузета са сајта wikimedia.org");
}
```

...па контроли `pcbOdgovor` додаш тај догађај помоћу руковаоца догађаја.
Значи, после креирања контроле `pcbOdgovor`, а пре њеног додавања на форму,
потребно је да доделиш догађај `pcbOdgovor_Click` контроли `pcbOdgovor` на
следећи начин:

```cs
pcbOdgovor.Click += new EventHandler(pcbOdgovor_Click);
```

Сада се кликом на контролу `pcbOdgovor` иницира догађај `pcbOdgovor_Click`:

```{image} images/dinamicko-04.png
:scale: 100
:align: center
```

## Уклањање динамички креираних контрола

Претходни задатак може се проширити са још једним захтевом. На дну форме
постави дугме `btnReset` са текстом "Ресетуј" које је иницијално онемогућено.

```cs
private void Form1_Load(object sender, EventArgs e)
{
    btnReset.Enabled = false;
}
```

Кликом на дугмад `btnTekst` или `btnSlika`, дугме `btnReset` треба да постане
омогућено. Кликом на `btnReset` треба уклонити динамички креирану контролу са
форме и поново омогућити дугме `btnTekst` или `btnSlika`.

```{image} images/dinamicko-05.png
:scale: 100
:align: center
```

Динамичке компоненте могу се уклонити на више начина. Први и најједноставнији
начин није погодан за овај пример. Подразумева коришћење `Controls.Remove()`
методе када постоји референца на динамички креирану контролу. На пример, у
догађају `btnTekst_Click`, где постоји референца на динамички креирану контролу
`lblOdgovor`, могла би се додати линија кода...

```cs
this.Controls.Remove(lblOdgovor);
```

...за уклањање контроле са форме и након тога још једна линија кода...

```cs
lblOdgovor.Dispose();
```

...за ослобађање ресурса које је контрола заузела.

Други начин, који јесте погодан за овај пример, подразумева уклањање контроле
на основу њеног имена. Додај дугме са текстом `btnReset` на дну форме, како је
тражено у задатку и креирај догађај `btnReset_Click`.

Ако је корисник био кликнуо на дугме `btnSlika` и на форми се налази динамички
креирана контрола `pcbOdgovor`...

```{image} images/dinamicko-06.png
:scale: 100
:align: center
```

...ову контролу можеш пронаћи и уклонити на следећи начин:

```cs
Control kontrolaZaBrisanje = this.Controls.Find("pcbOdgovor", true).FirstOrDefault();
if (kontrolaZaBrisanje != null)
{
    this.Controls.Remove(kontrolaZaBrisanje);
    kontrolaZaBrisanje.Dispose();
}
```

Ако је корисник био кликнуо на дугме `btnTekst` и на форми се налази динамички
креирана контрола `lblOdgovor`...

```{image} images/dinamicko-07.png
:scale: 100
:align: center
```
...ову контролу можеш пронаћи и уклонити као и претходну:

```cs
Control kontrolaZaBrisanje = this.Controls.Find("lblOdgovor", true).FirstOrDefault();
if (kontrolaZaBrisanje != null)
{
    this.Controls.Remove(kontrolaZaBrisanje);
    kontrolaZaBrisanje.Dispose();
}
```

На крају, када си обрисао динамички креирану контролу, омогући дугмад
`btnTekst` и `btnSlika`, а онемогући дугме `btnReset`.

## Комплетно решење задатка

Комплетно решење овог задатка, у којем си на форму додавао динамички креиране
контроле са жељеним својствима и догађајима и омогућио уклањање динамички
креираних контрола изгледа овако:

```cs
using System;
using System.Drawing;
using System.Linq;
using System.Windows.Forms;

namespace DinamickoKreiranjeKontrola
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            btnReset.Enabled = false;
        }

        private void btnTekst_Click(object sender, EventArgs e)
        {
            btnSlika.Enabled = false;
            btnReset.Enabled = true;
            Label lblOdgovor = new Label();
            lblOdgovor.Name = "lblOdgovor";
            lblOdgovor.Location = new Point(140, 160);
            lblOdgovor.Text = "Програмски језик C#";
            lblOdgovor.Font = new Font("Microsoft Sans Serif", 24);
            lblOdgovor.AutoSize = true;
            this.Controls.Add(lblOdgovor);
            btnTekst.Enabled = false;
        }

        private void btnSlika_Click(object sender, EventArgs e)
        {
            btnTekst.Enabled = false;
            btnReset.Enabled = true;
            PictureBox pcbOdgovor = new PictureBox();
            pcbOdgovor.Name = "pcbOdgovor";
            pcbOdgovor.Location = new Point(200, 160);
            Bitmap slika = new Bitmap("C_Sharp_Logo_2023.svg.png");
            pcbOdgovor.SizeMode = PictureBoxSizeMode.StretchImage;
            pcbOdgovor.ClientSize = new Size(205, 205);
            pcbOdgovor.Image = slika;
            pcbOdgovor.Click += new EventHandler(pcbOdgovor_Click);
            this.Controls.Add(pcbOdgovor);
            btnSlika.Enabled = false;
        }

        private void pcbOdgovor_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Слика је преузета са сајта wikimedia.org");
        }

        private void btnReset_Click(object sender, EventArgs e)
        {
            Control kontrolaZaBrisanje = this.Controls.Find("pcbOdgovor", true).FirstOrDefault();
            if (kontrolaZaBrisanje == null)
            {
                kontrolaZaBrisanje = this.Controls.Find("lblOdgovor", true).FirstOrDefault();
            }
            if (kontrolaZaBrisanje != null)
            {
                this.Controls.Remove(kontrolaZaBrisanje);
                kontrolaZaBrisanje.Dispose();
            }
            btnTekst.Enabled = true;
            btnSlika.Enabled = true;
            btnReset.Enabled = false;
        }
    }
}
```
