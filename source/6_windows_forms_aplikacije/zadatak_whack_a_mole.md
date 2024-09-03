# Задатак: Игра - кликни на кртицу

Припреми слику кртице (нпр. `krtica.bmp`) и слику рупе (нпр. `rupa.bmp`) и
учитај их у фајл са ресурсима. Постави девет оквира за слику, једну лабелу и
један тајмер. Иницијално, у свим оквирима за слику треба да буде учитана слика
рупе, а у лабели текст `Резултат: 0`. На откуцај тајмера, у насумично одабраном
оквиру за слику треба да се прикаже слика кртице. Ако корисник кликне на слику
кртице повећава се резултат у лабели.

```{image} images/zadatak_whack_a_mole.png
:scale: 100
:align: center
```


## Могуће решење задатка

```cs
using System;
using System.Windows.Forms;

namespace ZadatakUdariKrticu
{
    public partial class Form1 : Form
    {
        private Random random = new Random();
        private int rezultat = 0;
        private PictureBox[] rupe;
        private int krtica = -1;

        public Form1()
        {
            InitializeComponent();
            InicijalizujIgru();
        }

        private void InicijalizujIgru()
        {
            rupe = new PictureBox[] { pictureBox1, pictureBox2, pictureBox3, pictureBox4, pictureBox5, pictureBox6, pictureBox7, pictureBox8, pictureBox9 };
            foreach (var rupa in rupe)
            {
                rupa.Image = Properties.Resources.rupa;
                rupa.SizeMode = PictureBoxSizeMode.StretchImage;
                rupa.Tag = "rupa";
                rupa.Click += Rupa_Click;
            }
            timer1.Interval = 1000;
            timer1.Start();
            label1.Text = "Резултат: " + rezultat;
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (krtica >= 0)
            {
                rupe[krtica].Image = Properties.Resources.rupa;
                rupe[krtica].Tag = "rupa";
            }
            krtica = random.Next(rupe.Length);
            rupe[krtica].Image = Properties.Resources.krtica;
            rupe[krtica].Tag = "krtica";
        }

        private void Rupa_Click(object sender, EventArgs e)
        {
            var kliknuto = sender as PictureBox;
            if (kliknuto != null && kliknuto.Tag.ToString() == "krtica")
            {
                rezultat++;
                label1.Text = "Резултат: " + rezultat;
                kliknuto.Image = Properties.Resources.rupa;
                kliknuto.Tag = "rupa";
                krtica = -1;
            }
        }
    }
}
```

## Додатни задатак

Усаврши игру на следећи начин:

1. Промени систем бодовања тако да се у лабели приказује текст `Резултат: Х од Y`
где је `Х` број кликнутих кртица, а `Y` укупан број кртица који се до датог
тренутка појавио.
2. Дефиниши максимални број појављивања кртица (или омогући кориснику да одабере
тај број или га унесе) тако да игра има свој крај.
3. Дефиниши више нивоа тежине играња којима се мења брзина откуцаја тајмера у
милисекундама.
