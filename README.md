# Triangulate-C#

This program calculates what type of triangle we are working with and shows a picture of that triangle. 
Additionally, the program is able to work out the missing length of the triangle if the user enters an angle.


    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    
    namespace Triangulate
    {
        public partial class Form1 : Form
        {
            double H = 0;
            double O = 0;
            double A = 0;
            double Angle = 0;
            public Form1()
            {
                InitializeComponent();
                Iscos_triangle.Hide();
                right_triangle.Hide();
                scalene.Hide();
            }
    
            private void pictureBox1_Click(object sender, EventArgs e)
            {
    
            }
    
    
            private void Solve_btn_Click(object sender, EventArgs e)
            {
    
                label6.Text = "";
                label5.Text = "";
                label4.Text = "";
    
    
    
                Iscos_triangle.Hide();
                right_triangle.Hide();
                scalene.Hide();
    
                double hypot, adj, oppos, angle;
    
                if (string.IsNullOrEmpty(texbox_H.Text))
                {
                    oppos = double.Parse(textbox_O.Text);
                    adj = double.Parse(textbox_A.Text);
                    angle = double.Parse(textBox_angle.Text) * (Math.PI / 180);
                    double hypotenuse_find = Math.Sqrt(Math.Pow(adj, 2) + Math.Pow(oppos, 2) - 2 * adj * oppos * Math.Cos(angle));                                         
    
                    H = hypotenuse_find;
                    O = oppos;
                    A = adj;
                    label6.Text += hypotenuse_find.ToString();
                }
                else if (string.IsNullOrEmpty(textbox_O.Text))
                {
                    hypot = double.Parse(texbox_H.Text);
                    adj = double.Parse(textbox_A.Text);
                    angle = double.Parse(textBox_angle.Text) * (Math.PI / 180);
                    double oppos_find = Math.Sqrt(Math.Pow(hypot, 2) + Math.Pow(adj, 2) - 2 * adj * hypot * Math.Cos(angle)); ;
                    O = oppos_find;
                    H = hypot;
                    A = adj;
                    label5.Text += oppos_find.ToString();
                }
                else if (string.IsNullOrEmpty(textbox_A.Text))
                {
                    hypot = double.Parse(texbox_H.Text);
                    oppos = double.Parse(textbox_O.Text);
                    angle = double.Parse(textBox_angle.Text) * (Math.PI / 180);
                    double adj_find = Math.Sqrt(Math.Pow(hypot, 2) + Math.Pow(oppos, 2) - 2 * hypot * oppos * Math.Cos(angle)); ;
                    A = adj_find;
                    H = hypot;
                    O = oppos;
                    label4.Text += adj_find.ToString();
                }
                else
                {
                    A = double.Parse(textbox_A.Text);
                    H = double.Parse(texbox_H.Text); ;
                    O = double.Parse(textbox_O.Text);
                }
    
               
    
                label6.Text = "Hypotenuse: " + H.ToString();
                label5.Text = "Opposite: " + O.ToString();
                label4.Text = "Adjacent: " + A.ToString();
    
                double assumed_hyp = Math.Sqrt(Math.Pow(O, 2) + Math.Pow(A, 2));
    
                if (assumed_hyp == H)
                {
                    right_triangle.Show();
                    Ans_label.Text = "Its a Right Angle Triangle!"; 
                }
                                  
                else if (H == O || O == A || H == A)
                {
                    Iscos_triangle.Show();
                    Ans_label.Text = "Its an Iscoscelese Triangle!";
                }
                   
                else
                {
                    Ans_label.Text = "Its a Scalene Triangle!";
                    scalene.Show();
                }
                
    
            }
        }
    }
