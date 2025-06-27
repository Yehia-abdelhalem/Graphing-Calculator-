# Graphing Calculator

A C# graphing calculator built with object-oriented programming and a graphical user interface (GUI) using Windows Forms. This project demonstrates the integration of real-time plotting, scientific computation, and user expression parsing.

---

## 🧮 Features

- Standard arithmetic operations: `+`, `-`, `×`, `÷`, `Mod`, `Exp`
- Scientific functions: `sin`, `cos`, `tan`, `sinh`, `log`, `ln`, `sqrt`, etc.
- Graphing of mathematical expressions like:  
  - `sin(x)`  
  - `x^2`  
  - `exp(x)`
- Base conversions: Binary, Octal, Hexadecimal
- Real-time graph plotting with [ScottPlot](https://scottplot.net/)
- Expression parsing using [NCalc](https://archive.codeplex.com/?p=ncalc)
- Clean Windows Forms GUI

---

## 🛠️ Technologies Used

- **C#** and **.NET Framework**
- **WinForms** – GUI development
- **ScottPlot** – Plotting mathematical functions
- **NCalc** – Parsing and evaluating expressions

---

## 🧰 Setup Instructions

To run the application:

1. Clone the repository:
   ```bash
   git clone https://github.com/Yehia-abdelhalem/Graphing-Calculator.git
NOTE::
To use the calculator's full features, ensure ScottPlot and NCalc are installed via NuGet. Example namespaces used:
----code-----
to use it you must download ScottPlot and Ncalc to calculate.

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using OpenTK.Audio.OpenAL;
using ScottPlot.WinForms;
using NCalc;
using System.Text.RegularExpressions;

namespace Scientific_calculator
{
    public partial class Form1 : Form
    {
        double enterFirstValue, enterSecondValue;

        string op;

        FormsPlot formsPlot;


        private Panel graphPanel;
        private TextBox inputBox;
        private Button plotButton;
        private FormsPlot plotControl;
        public Form1()
        {
            InitializeComponent();


            // Initialize formsPlot
            formsPlot = new FormsPlot
            {
                Dock = DockStyle.Fill
            };
            panel1_graph.Controls.Add(formsPlot);


        }

        private void EnterNumbers(object sender, EventArgs e)
        {
            Button num = (Button)sender;

            if (textBox1.Text == "0")
                textBox1.Text = "";
            {
                if (num.Text == ".")
                {
                    if (!textBox1.Text.Contains("."))
                        textBox1.Text = textBox1.Text + num.Text;
                }
                else
                {
                    textBox1.Text = textBox1.Text + num.Text;
                }
            }
        }

        private void numberOperators(object sender, EventArgs e)
        {
            Button num = (Button)sender;

            enterFirstValue = Convert.ToDouble(textBox1.Text);
            op = num.Text;
            textBox1.Text = "";



        }

        private void Btnequal_Click(object sender, EventArgs e)
        {
            enterSecondValue = Convert.ToDouble(textBox1.Text);

            switch (op)
            {
                case "+":

                    textBox1.Text = (enterFirstValue + enterSecondValue).ToString();
                    break;
                case "-":

                    textBox1.Text = (enterFirstValue - enterSecondValue).ToString();

                    break;

                case "×":

                    textBox1.Text = (enterFirstValue * enterSecondValue).ToString();
                    break;

                case " ÷":

                    textBox1.Text = (enterFirstValue / enterSecondValue).ToString();

                    break;

                case "Mod":
                    textBox1.Text = (enterFirstValue % enterSecondValue).ToString();
                    break;


                case "Exp":

                    double E = Convert.ToDouble(textBox1.Text);
                    double J;
                    J = enterSecondValue;

                    textBox1.Text = Math.Exp(E * Math.Log(J * 4)).ToString();

                    break;



                default:
                    break;
            }
        }

        private void CLR_Click(object sender, EventArgs e)
        {
            textBox1.Text = "0";

        }

        private void BtnCLR_Click(object sender, EventArgs e)
        {
            textBox1.Text = "0";

            string N;
            N = Convert.ToString(textBox1.Text);

            N = "";
        }

        private void button4_Click(object sender, EventArgs e)
        {
            double q = Convert.ToDouble(textBox1.Text);
            textBox1.Text = Convert.ToString(-1 * q);
        }

        private void button1_Back(object sender, EventArgs e)
        {
            if (textBox1.Text.Length > 0)
            {
                textBox1.Text = textBox1.Text.Remove(textBox1.Text.Length - 1, 1);

            }

            if (textBox1.Text == "")
            {
                textBox1.Text = "0";

            }
        }

        private void fILEToolStripMenuItem_Click(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {
            this.Width = 210;
            textBox1.Width = 170;
            panel1_graph.Visible = false;


        }

        private void standardToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.Width = 320;
            textBox1.Width = 170;
            panel1_graph.Visible = false;
        }

        private void scientificToolStripMenuItem_Click(object sender, EventArgs e)
        {
            this.Width = 590;
            textBox1.Width = 350;
            panel1_graph.Visible = false;
            BTN_PLOT.Visible = false;   
           
        }

        private void exitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            DialogResult exitcal;

            exitcal = MessageBox.Show("Confirm if you want to exit", "scientific calculator", MessageBoxButtons.YesNo, MessageBoxIcon.Question);

            if (exitcal == DialogResult.Yes)
            {
                Application.Exit();
            }
        }

        private void button11_Click(object sender, EventArgs e)
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = Convert.ToString(a, 2);

        }

        private void btn_pie_Click(object sender, EventArgs e)
        {
            textBox1.Text = "3.141592653589976323";

        }

        private void btn_log_Click(object sender, EventArgs e)
        {
            double Log = Convert.ToDouble(textBox1.Text);
            Log = Math.Log10(Log);
            textBox1.Text = Convert.ToString(Log);


        }

        private void btn_sqrt_Click(object sender, EventArgs e)
        {
            double sqrt = Convert.ToDouble(textBox1.Text);
            sqrt = Math.Sqrt(sqrt);
            textBox1.Text = Convert.ToString(sqrt);

        }

        private void Btn_square_Click(object sender, EventArgs e)
        {
            double x;
            x=Convert.ToDouble(textBox1.Text)*Convert.ToDouble(textBox1.Text);
            textBox1.Text=x.ToString(); 

        }

        private void Btn_cube_Click(object sender, EventArgs e)
        {
            double x;
            x = Convert.ToDouble(textBox1.Text) * Convert.ToDouble(textBox1.Text)* Convert.ToDouble(textBox1.Text);
            textBox1.Text = x.ToString();
        }

        private void btn_sinh_Click(object sender, EventArgs e)
        {
            double sinh = Convert.ToDouble(textBox1.Text);
            sinh = Math.Sinh(sinh);
            textBox1.Text = Convert.ToString(sinh);

        }

        private void btn_sin_Click(object sender, EventArgs e)
        {
            double sinh = Convert.ToDouble(textBox1.Text);
            sinh = Math.Sin(sinh);
            textBox1.Text = Convert.ToString(sinh);

        }

        private void btn_cosh_Click(object sender, EventArgs e)
        {
            double cosh = Convert.ToDouble(textBox1.Text);
            cosh = Math.Cosh(cosh);
            textBox1.Text = Convert.ToString(cosh);
        }

        private void btncos_Click(object sender, EventArgs e)
        {
            double cosh = Convert.ToDouble(textBox1.Text);
            cosh = Math.Cos(cosh);
            textBox1.Text = Convert.ToString(cosh);
        }

        private void btn_tanh_Click(object sender, EventArgs e)
        {
            double Tanh = Convert.ToDouble(textBox1.Text);
            Tanh = Math.Tanh(Tanh);
            textBox1.Text = Convert.ToString(Tanh);
            
        }

        private void btn_tan_Click(object sender, EventArgs e)
        {
            double Tanh = Convert.ToDouble(textBox1.Text);
            Tanh = Math.Tan(Tanh);
            textBox1.Text = Convert.ToString(Tanh);
        }

        private void btn_fraction_Click(object sender, EventArgs e)
        {
            double x;
            x=Convert.ToDouble(1.0/Convert.ToDouble(textBox1.Text));
            textBox1.Text=Convert.ToString(x);
        }

        private void btn_ln_Click(object sender, EventArgs e)
        {
            double ln = Convert.ToDouble(textBox1.Text);
            ln = Math.Log(ln);
            textBox1.Text = Convert.ToString(ln);
        }

        private void btn_percentage_Click(object sender, EventArgs e)
        {
            double a;
            a = Convert.ToDouble(textBox1.Text) / Convert.ToDouble(100);
            textBox1.Text = Convert.ToString(a);
        }

        private void button7_Click(object sender, EventArgs e)
        {
            double dec = Convert.ToDouble(textBox1.Text);
            int i1 = Convert.ToInt32(dec);
            int i2 = (int)dec;
            textBox1.Text = Convert.ToString(i2);
        }

        private void btn_hex_Click(object sender, EventArgs e)
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = Convert.ToString(a, 16);
        }

        private void button19_Click(object sender, EventArgs e)
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = Convert.ToString(a, 8);
        }

        private void button1_Click(object sender, EventArgs e)
        {

        }

        private void graphingToolStripMenuItem_Click(object sender, EventArgs e)
        {

            this.Width = 890;
            textBox1.Width = 500;
            panel1_graph.Controls.Clear();
            panel1_graph.Visible = true;
            BTN_PLOT.Visible = true;


            // Create new plot
            formsPlot = new FormsPlot
            {
                Dock = DockStyle.Fill
            };

            panel1_graph.Controls.Add(formsPlot);

            // Get X and Y data (e.g., y = x^2)
            double[] xs = Enumerable.Range(0, 10).Select(x => (double)x).ToArray();
            double[] ys = xs.Select(x => x * x).ToArray();

            // Plot the data
            formsPlot.Plot.Add.Scatter(xs, ys);
            formsPlot.Refresh();

        }

        private void panel1_graph_Paint(object sender, PaintEventArgs e)
        {

        }

        private void BTN_PLOT_Click(object sender, EventArgs e)
        {

            if (formsPlot == null)
            {
                formsPlot = new FormsPlot { Dock = DockStyle.Fill };
                panel1_graph.Controls.Clear();
                panel1_graph.Controls.Add(formsPlot);
                panel1_graph.Visible = true;
            }

            string input = textBox1.Text.Trim();

            if (string.IsNullOrEmpty(input))
            {
                MessageBox.Show("Enter a function like sin(x), x^2, etc.");
                return;
            }

            // Convert ^ to Pow()
            input = Regex.Replace(input, @"(\w+)\^(\w+)", "Pow($1,$2)", RegexOptions.IgnoreCase);

            double[] xs = Enumerable.Range(-100, 201).Select(i => i / 10.0).ToArray();
            List<double> ys = new List<double>();

            foreach (double x in xs)
            {
                try
                {
                    var expr = new Expression(input);

                    // Register custom functions (per-expression)
                    expr.EvaluateFunction += (name, args) =>
                    {
                        double arg = Convert.ToDouble(args.Parameters[0].Evaluate());

                        switch (name.ToLower())
                        {
                            case "sin": args.Result = Math.Sin(arg); break;
                            case "cos": args.Result = Math.Cos(arg); break;
                            case "tan": args.Result = Math.Tan(arg); break;
                            case "sqrt": args.Result = Math.Sqrt(arg); break;
                            case "log": args.Result = Math.Log10(arg); break;
                            case "ln": args.Result = Math.Log(arg); break;
                            case "abs": args.Result = Math.Abs(arg); break;
                            case "exp": args.Result = Math.Exp(arg); break;
                            case "pow":
                                double baseVal = Convert.ToDouble(args.Parameters[0].Evaluate());
                                double expVal = Convert.ToDouble(args.Parameters[1].Evaluate());
                                args.Result = Math.Pow(baseVal, expVal);
                                break;
                                
                        }
                    };

                    expr.Parameters["x"] = x;
                    object result = expr.Evaluate();
                    ys.Add(Convert.ToDouble(result));
                }
                catch
                {
                    ys.Add(double.NaN);
                }
            }

            formsPlot.Plot.Clear();
            formsPlot.Plot.Add.Scatter(xs, ys.ToArray());
            formsPlot.Plot.Axes.AutoScale();
            formsPlot.Refresh();

        }

        private void PlotButton_Click(object sender, EventArgs e)
        {
            try
            {
                string expression = textBox1.Text;
                var xs = Enumerable.Range(-50, 101).Select(x => (double)x).ToArray();
                var ys = xs.Select(x =>
                {
                    var expr = new NCalc.Expression(expression);
                    expr.Parameters["x"] = x;
                    return Convert.ToDouble(expr.Evaluate());
                }).ToArray();

                plotControl.Plot.Clear();
                plotControl.Plot.Add.Scatter(xs, ys);
                plotControl.Refresh();
            }
            catch (Exception ex)
            {
                MessageBox.Show("Error: " + ex.Message);
            }
        }

    }
}
