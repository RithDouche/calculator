/*
Date        Developer           Changes
2/6/2025    Sotharith Sieng     creates the Gui       
2/11/2025   Sotharith Sieng     implemement the operation  

*/
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Calculator
{
    public partial class Form1 : Form
    {
        private double leftOperand = 0.0;
        private String mathOperation = "";
        private bool mathOpinProgress = false;
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }
        // When a button is clicked (any button), the number is displayed
        private void numBtn_Click(object sender, EventArgs e)
        {
            if(display.Text == "0" || mathOpinProgress == true && display.Text !=".")
            {
                //clear the display
                //1 - display is only a 0
                //2 - do a math operation and it is not a "."
                display.Clear();
            }

            mathOpinProgress = false;
            display.Text += ((Button)sender).Text;
        }

        // If CE button is clicked, the display changes to 0
        private void clearEntryBtn_Click(object sender, EventArgs e)
        {
            display.Text = "0";
        }

        private void clearAllBtn_Click(object sender, EventArgs e)
        {
            // Clear memory holding "first operands" and possibly math operation "operator"
            //math operation "operator"
            leftOperand = 0.0;
            mathOpinProgress = false;
            // Repeat clear entry button click
            clearEntryBtn_Click(sender, e);
        }

        // Changes sign to negative. If already negative, it switches back to positive
        private void posNegBtn_Click(object sender, EventArgs e)
        {
            display.Text = (-double.Parse(display.Text)).ToString();
        }

        // Checks if the display contains a decimal, and if it doesn't the calculator will place one
        // Not currently using in this app
        private void decimalBtn_Click_orig(object sender, EventArgs e)
        {
            // example of conditional operator
            display.Text = (display.Text.Contains(".")) ? display.Text : display.Text + ".";
        }
        // Second version using ternary operator - example of an expression-bodied method
        private void decimalBtn_Click(object sender, EventArgs e) =>
            // example of conditional operator
            display.Text = (display.Text.Contains(".")) ? display.Text : display.Text + ".";

        private void backspace_Click(object sender, EventArgs e)
        {
            if (display.Text.Length > 1)
            {
                // sunny day scenario - take off one Char
                display.Text = display.Text.Substring(0, display.Text.Length - 1);
            }
            else
            {
                display.Text = "0";
            }

            
        }

        private void mathOperationBtn_Click(object sender, EventArgs e)
        {
            leftOperand = double.Parse(display.Text); //get the left operand from the current display
            mathOperation = ((Button)sender).Text; // get the operation from the button that was clicked
            mathOpinProgress = true;
            //for debugging to mae it obvious that an operation wa captured
            display.Clear();
        }

        private void equalBtn_Click(object sender, EventArgs e)
        {
            // based on the saved math operation that was chosen just before equals
            switch (mathOperation)
            {
                case "+":
                    display.Text = (leftOperand + double.Parse(display.Text)).ToString();
                    break;
                case "-":
                    display.Text = (leftOperand - double.Parse(display.Text)).ToString();
                    break;
                case "x":
                    display.Text = (leftOperand * double.Parse(display.Text)).ToString();
                    break;
                case "/":
                    display.Text = (leftOperand / double.Parse(display.Text)).ToString();
                    break;
            }
        }
    }
}
