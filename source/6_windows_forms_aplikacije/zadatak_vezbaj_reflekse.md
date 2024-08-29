# Задатак: Вежбај рефлексе

На форму жељених димензија постави две тајмер контроле. На откуцај првог
тајмера на форми треба да се, на насумичној позицији, прикаже зелено или црвено
дугме и стартује други тајмер. На откуцај другог тајмера са форме треба да
нестане приказано дугме и поново се стартује први тајмер и тако редом. Ако
корисник кликне на зелено дугме добија бод...

```{image} images/refleksi.png
:scale: 100
:align: center
```


...а ако кликне на црвено дугме или на форму губи бод:

```{image} images/refleksi2.png
:scale: 100
:align: center
```


## Могуће решење задатка

Задатак треба да решиш динамичким креирањем контрола и додавањем догађаја
динамички креираним контролама.

```cs
using System;
using System.Drawing;
using System.Windows.Forms;

namespace ZadatakVezbajReflekse
{
    public partial class Form1 : Form
    {
        private Random random = new Random();
        private int rezultat = 0;
        private Button dugme = null;

        public Form1()
        {
            InitializeComponent();
            this.Text = "Вежбај рефлексе!";
            timer1.Interval = 1000;
            timer1.Start();
            timer2.Interval = 1000;
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (dugme != null)
            {
                Controls.Remove(dugme);
                dugme.Dispose();
                dugme = null;
            }

            dugme = new Button();
            dugme.Size = new Size(50, 50);
            dugme.Location = new Point(random.Next(0, this.ClientSize.Width - dugme.Width),
                                              random.Next(0, this.ClientSize.Height - dugme.Height));

            if (random.Next(2) == 0)
            {
                dugme.BackColor = Color.Green;
                dugme.Click += zeleno_Click;
            }
            else
            {
                dugme.BackColor = Color.Red;
                dugme.Click += crveno_Click;
            }

            Controls.Add(dugme);
            timer2.Start();
        }

        private void timer2_Tick(object sender, EventArgs e)
        {
            timer2.Stop();
            if (dugme != null)
            {
                Controls.Remove(dugme);
                dugme.Dispose();
                dugme = null;
            }
        }

        private void zeleno_Click(object sender, EventArgs e)
        {
            rezultat++;
            Rezultat();
            ObrisiDugme(sender);
        }

        private void crveno_Click(object sender, EventArgs e)
        {
            rezultat--;
            Rezultat();
            ObrisiDugme(sender);
        }

        private void ObrisiDugme(object sender)
        {
            Controls.Remove((Button)sender);
            ((Button)sender).Dispose();
            dugme = null;
        }

        private void Rezultat()
        {
            this.Text = $"Резултат: {rezultat}";
        }

        private void Form1_Click(object sender, EventArgs e)
        {
            rezultat--;
            Rezultat();
        }
    }
}
```

## Додатни задатак

1. Осмисли и имплементирај покретање и заустављање игре.
2. Осмисли и имплементирај елегантнији начин за приказивање бодова са више
детаља, на пример, колико је бодова освојено од највећег могућег броја бодова.
3. Осмисли и имплементирај нивое тежине играња помоћу комбинованих оквира,
помоћу којих корисник може да убрза или успори тајмере.
