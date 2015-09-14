//# Math-Quiz
//A simple math quiz that has random problems.
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace MathQuiz
{
    public partial class Form1 : Form

    {
        //Create a random object called randomizer
        //to generate random numbers.
        Random randomizer = new Random();

        //These integer variables store the numbers
        //for addition problems.
        int addend1;
        int addend2;

        //These integer variables store the numbers
        //for subtraction problems.
        int minuend;
        int subtrahend;

        //These integer variables store the numbers
        //for multiplication problems.
        int multiplcand;
        int multiplier;

        //These integer variables store the numbers
        //for division problems.
        int dividend;
        int divisor;

        //The timeLeft int keeps track of the 
        //remaining time.
        int timeLeft;

        

        
        public Form1()
        {
            InitializeComponent();
            
            
        }

        public void StartTheQuiz()
        {
            //Generate two random numbers to add.
            //Store values in the variables in 'addend1' and
            //'addened2'.
            addend1 = randomizer.Next(51);
            addend2 = randomizer.Next(51);

            //Convert the two random numbers into strings
            //so they can be displayed in the label controls.
            plusLeftLabel.Text = addend1.ToString();
            plusRightLabel.Text = addend2.ToString();

            //'sum' is the name of the numericUpDown control.
            //This step makes sure that the value is zero
            //before adding anything to it.
            sum.Value = 0;

            //Fill in the subtraction problem.

            minuend = randomizer.Next(1, 101);
            subtrahend = randomizer.Next(1, minuend);
            minusLeftLabel.Text = minuend.ToString();
            minusRightLabel.Text = subtrahend.ToString();
            Difference.Value = 0;

            //Fill in the multiplication problem

            multiplcand = randomizer.Next(2, 11);
            multiplier = randomizer.Next(2, 11);
            timesLeftLabel.Text = multiplcand.ToString();
            timesRightLabel.Text = multiplier.ToString();
            product.Value = 0;

            //Fill in the division problem
            divisor = randomizer.Next(2, 11);
            int temporaryQuotient = randomizer.Next(2, 11);
            dividend = divisor * temporaryQuotient;
            dividedLeftLabel.Text = dividend.ToString();
            dividedRightLabel.Text = divisor.ToString();
            quotient.Value = 0;


            //Start the timer

            timeLeft = 60;
            TimeLabel.Text = "60 seconds";
            timer1.Start();

        }
            
        
        
        private void CheckTheAnswer()
        {
            if ((addend1 + addend2 == sum.Value) 
                && (minuend - subtrahend == Difference.Value)
                && (multiplcand * multiplier == product.Value)
                && (dividend / divisor == quotient.Value))
            {
                MessageBox.Show("You are right!");
            }
                else 
                { 
                MessageBox.Show("Sorry, that was incorrect.");
            }
        }

        private void label3_Click(object sender, EventArgs e)
        {

        }

        private void label4_Click(object sender, EventArgs e)
        {

        }

        private void startButton_Click(object sender, EventArgs e)
        {
            StartTheQuiz();
            startButton.Enabled = false;
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            if ((addend1 + addend2 == sum.Value)
                && (subtrahend - minuend == Difference.Value)
                && (multiplcand * multiplier == product.Value)
                && (dividend / divisor == quotient.Value))
            {
                timer1.Stop();
                MessageBox.Show("Congratulations!, you got all the answers right.");
                startButton.Enabled = true;



            }
            if (timeLeft > 0)
            {
                // If CheckTheAnswer() return false, keep counting 
                // down. Decrease the time left by one second and  
                // display the new time left by updating the  
                // Time Left label.

                timeLeft--;
                timeLeft = timeLeft - 1;
                TimeLabel.Text = timeLeft + " seconds";            

            }
            else
            {
                //If the user ran out of time stop the timer
                //show the message box and fill out the answers
                timer1.Stop();
                TimeLabel.Text = "Time's up!";
                MessageBox.Show("Sorry, you didn't finish in time.");
                sum.Value = addend1 + addend2;
                Difference.Value = minuend - subtrahend;
                product.Value = multiplcand * multiplier;
                quotient.Value = dividend / divisor; 
                startButton.Enabled = true;

                
            }
        }

        private void answer_Enter(object sender, EventArgs e)
        {
            //Select the whole answer in the numericUpdown Control
            NumericUpDown answerBox = sender as NumericUpDown;

            if (answerBox != null)
            {
                int lengthOfAnswer = answerBox.Value.ToString().Length;
                answerBox.Select(0, lengthOfAnswer);

            }

        }

        

        
        
            
        }

    }


