# Задатак: Квиз питања са једним тачним одговором

На форму постави оквир за групу, у оквир за групу постави четири радио-дугмета,
а испод оквира за групу постави једно дугме. Креирај апликацију "КВИЗ ЗНАЊА" у
којој питања увек имају један тачан одговор. Питања и одговори треба да буду
дефинисани у фајлу `pitanja.txt` на следећи начин:

```text
Који се од следећих типова података користи за представљање целих бројева?
int
float
string
bool
1
Какви могу бити чланови класе?
Локални и глобални.
Спољашњи и унутрашњи.
Функцијски и процедурални.
Статички и нестатички.
4
```

На следеће питање прелази се тек када је дат тачан одговор на тренутно питање.

![Задатак - Квиз](./images/zadatak_scq.png)

## Могуће решење задатка

```cs
using System;
using System.Collections.Generic;
using System.Windows.Forms;
using System.IO;

namespace ZadatakRadioButtonKviz
{
    public partial class Form1 : Form
    {
        private List<string[]> pitanja;
        private int trenutnoPitanje;
        public Form1()
        {
            InitializeComponent();
            button1.Text = "ОДГОВОРИ";
            button1.TabIndex = 0;
            UcitajPitanja();
            PrikaziPitanje(0);
        }

        private void UcitajPitanja()
        {
            pitanja = new List<string[]>();
            string[] linije = File.ReadAllLines("pitanja.txt");
            for (int i = 0; i < linije.Length; i += 6)
            {
                string[] setPitanja = new string[6];
                Array.Copy(linije, i, setPitanja, 0, 6);
                pitanja.Add(setPitanja);
            }
        }

        private void PrikaziPitanje(int redniBroj)
        {
            trenutnoPitanje = redniBroj;
            var q = pitanja[redniBroj];
            groupBox1.Text = q[0];
            radioButton1.Text = q[1];
            radioButton2.Text = q[2];
            radioButton3.Text = q[3];
            radioButton4.Text = q[4];
        }

        private void button1_Click(object sender, EventArgs e)
        {
            var q = pitanja[trenutnoPitanje];
            int tacno = int.Parse(q[5]);
            int odgovor = 0;
            if (radioButton1.Checked) odgovor = 1;
            else if (radioButton2.Checked) odgovor = 2;
            else if (radioButton3.Checked) odgovor = 3;
            else if (radioButton4.Checked) odgovor = 4;
            bool tacanOdgovor = (tacno == odgovor);
            if (tacanOdgovor)
            {
                MessageBox.Show("Одговор је тачан!");
                int sledecePitanje = trenutnoPitanje + 1;
                if (sledecePitanje < pitanja.Count)
                {
                    radioButton1.Checked = false;
                    radioButton2.Checked = false;
                    radioButton3.Checked = false;
                    radioButton4.Checked = false;
                    PrikaziPitanje(sledecePitanje);
                }
                else
                {
                    MessageBox.Show("Крај квиза");
                    groupBox1.Visible = false;
                    button1.Visible = false;
                }
            }
            else
            {
                MessageBox.Show("Одговор није тачан. Покушај поново.");
            }
        }
    }
}
```

## Додатни задатак

1. Креирај систем за бодовање, тако да се за свако тачно одговорено питање
добија 1 бод. На следеће питање прелази се након одговора на тренутно
питање, без обзира да ли је одговор био тачан или нетачан. Тренутно стање
бодова треба да буде приказано у лабели на форми.
2. Омогући да се сет питања и одговора приказује насумичним (а не увек истим)
редоследом.
3. Обради могуће изузетке, нарочито приликом рада са фајлом.
