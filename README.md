using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace minhbh01655
{
    internal class Program
    {
        static void Main(string[] args)

        {
            int userInput = 1;
            while (userInput != 0)
            {
                
                string name = Getname();
                int customerType = GetcustomerType();
                (double thismonth, double lastmonth) = GetWaterM();
                double numbers = Getnumbers(customerType);

                double price = Price(customerType, thismonth, lastmonth);

                bill(name, lastmonth, thismonth, price, numbers, customerType);

                Console.WriteLine("*Press 1 to continue, or 0 to exit*");
                userInput = int.Parse(Console.ReadLine());
            }
        }
        static string Getname()
        {
            string name;
            while (true)
            {
                Console.WriteLine("~Customer name:");
                name = Console.ReadLine();
                name = name.Trim();
                if (double.TryParse(name, out double result))
                {
                    Console.WriteLine("--------------------------------------------------------------");
                    Console.WriteLine("Invalid input. Please enter a valid name (cannot be a number).");
                    Console.WriteLine("--------------------------------------------------------------");
                }
                else if (string.IsNullOrEmpty(name))
                {
                    Console.WriteLine("------------------------------------------------------------------------");
                    Console.WriteLine("Invalid input. Customer name cannot be empty. Please enter a valid name.");
                    Console.WriteLine("------------------------------------------------------------------------");
                }
                else
                {
                    break;
                }
            }
            return name;
        }


        static int GetcustomerType()
        {
            int customerType = 0;
            Console.WriteLine("--------Enter the customer type:-------------");
            Console.WriteLine(" 1. Household                                ");
            Console.WriteLine(" 2. Administrative agency, Public services   ");
            Console.WriteLine(" 3. Production units                         ");
            Console.WriteLine(" 4. Business services                        ");
            Console.WriteLine("---------------------------------------------");

            while (true)
            {
                Console.WriteLine("~Your choice:");
                if (int.TryParse(Console.ReadLine(), out customerType) && customerType >= 1 && customerType <= 4)
                {
                    break;
                }
                Console.WriteLine("---------------------------------------------");
                Console.WriteLine("~Please enter a valid customer type (1 to 4).");
                Console.WriteLine("---------------------------------------------");
            }
            return customerType;
        }


        static (double thismonth, double lastmonth) GetWaterM()
        {
            double thismonth ,lastmonth;
            while (true)
            {
                Console.WriteLine("~This month’s water meter readings:");
                if (double.TryParse(Console.ReadLine(), out thismonth))
                {
                    Console.WriteLine("~Last month’s water meter readings:");
                    if (double.TryParse(Console.ReadLine(), out lastmonth))
                    {
                        if (thismonth >= lastmonth)
                        {
                            break;
                        }
                        Console.WriteLine("------------------------------------------------------------------------------------------------");
                        Console.WriteLine("~Invalid readings. This month's reading should be greater than or equal to last month's reading.");
                        Console.WriteLine("------------------------------------------------------------------------------------------------");
                    }
                }
                Console.WriteLine("-----------------------------------");
                Console.WriteLine("~Please enter valid meter readings.");
                Console.WriteLine("-----------------------------------");
            }
            return (thismonth, lastmonth);  
        }


        static double Getnumbers(int customerType)
        {
            double numbers = 0;
            if (customerType == 1)
            {
                while (true)
                {
                    Console.WriteLine("~Number of family members:");
                    if (int.TryParse(Console.ReadLine(), out int result) && result >= 1)
                    {
                        numbers = result;
                        break;
                    }
                    Console.WriteLine("-------------------------------------------------------------------------");
                    Console.WriteLine("~Invalid input for number of family members. Please enter a valid number.");
                    Console.WriteLine("-------------------------------------------------------------------------");
                }
            }
            return numbers;
        }


        static double Price(int customerType, double thismonth, double lastmonth)
        {
            double price = 0;
            switch (customerType)
            {
                case 1:

                    double total1 = thismonth - lastmonth;
                    {
                        if (total1 <= 10)
                        {
                            price = 5.973;
                        }
                        else if (total1 <= 20)
                        {
                            price = 7.052;
                        }
                        else if (total1 <= 30)
                        {
                            price = 8.699;
                        }
                        else
                        {
                            price = 15.929;
                        }
                    }
                    break;
                case 2:
                    price = 9.955;
                    break;
                case 3:
                    price = 11.615;
                    break;
                case 4:
                    price = 22.068;
                    break;
                default:
                    Console.WriteLine("-----------------------------------");
                    Console.WriteLine("Please check the information again!");
                    Console.WriteLine("-----------------------------------");
                    break;
            }
            Console.WriteLine("Press enter twice to display the bill ");
            Console.ReadLine();
            return price;

        }

        static void bill(string name, double lastmonth, double thismonth, double price, double numbers, int customerType)
        {

            Console.WriteLine("_________YOUR BILL_________");
            Console.WriteLine("* Name:{0}", name);
            Console.WriteLine("---------------------------");


            double total = thismonth - lastmonth;
            double special = customerType == 1 ? (total / numbers) * price : total  * price;
            
            double Amount = special * 0.1;
            double VAT = special * 0.1;
            double all = special + Amount + VAT;


            Console.WriteLine("* Water consumed: {0}m3", total);
            Console.WriteLine("* Water Bill: {0} VND", special);
            Console.WriteLine("* Enviroment fees: {0} VND", Amount);
            Console.WriteLine("* VAT(10%): {0} VND", VAT);
            Console.WriteLine("* Total bill: {0} VND", all);


            Console.WriteLine("---------------------------");

            return;
        }
    }
}
