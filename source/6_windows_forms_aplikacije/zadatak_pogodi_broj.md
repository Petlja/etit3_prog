# Задатак: Погађање замишљеног броја

Доступне су: једна контрола `textBox1`, једна контрола `button1` и једна
контрола `label1`. Креирај апликацију "ПОГОДИ ЗАМИШЉЕН БРОЈ" за погађање
насумично генерисаног броја у интервалу од 1 до 100.

## Могуће решење задатка

```cs
using System;
using System.Windows.Forms;

namespace PogodiBroj
{
    public partial class Form1 : Form
    {
        private int zamisljeni;
        private Random random;
        public Form1()
        {
            InitializeComponent();
            random = new Random();
            Resetuj();
        }

        private void Resetuj()
        {
            zamisljeni = random.Next(1, 101);
            label1.Text = "Погоди замишљени број између 1 и 100";
            textBox1.Clear();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            int uneti;
            if (int.TryParse(textBox1.Text, out uneti))
            {
                if (uneti < 1 || uneti > 100)
                {
                    label1.Text = "Унеси број између 1 и 100.";
                }
                else if (uneti < zamisljeni)
                {
                    label1.Text = "Погрешно, твој број је мањи од замишљеног.";
                }
                else if (uneti > zamisljeni)
                {
                    label1.Text = "Погрешно, твој број је већи од замишљеног.";
                }
                else
                {
                    label1.Text = "Честитам! Погодиo си број!";
                    MessageBox.Show("Честитам! Погодиo си број!");
                    Resetuj();
                }
            }
            else
            {
                label1.Text = "Унеси валидан број!";
            }
        }
    }
}
```

## Додатни задаци

* Креирај систем за праћење броја покушаја погађања. Број покушаја треба да
буде приказан у лабели.
