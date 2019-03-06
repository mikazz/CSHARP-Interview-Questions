# C# Interview Questions
Collection of different interview questions


# 1. Given an array of ints, write a C# method to sum all the values that are even numbers.

    using System;
    using System.Linq;

    class Program {

        static void Main() {

            int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9};

            Console.WriteLine(string.Join(" ", array));
            Console.WriteLine(SumAllEvenNumbers(array));
            Console.WriteLine(SumAllEvenNumbers2(array));
        }

        static long SumAllEvenNumbers(int[] intArray) {
            return intArray.Where(i => i % 2 == 0).Sum(i => (long)i);
        }

        static long SumAllEvenNumbers2(int[] intArray) {
            return (from i in intArray where i % 2 == 0 select (long)i).Sum();
        }
    }


# 2. What is the output of the short program below? Explain your answer. (Default datatype values)

    using System;

    class Program {
        // Field is never assigned to, and will always have its default value
        static String location; // String is a reference type
        static DateTime time; // DateTime is a value type

        static void Main() {
            Console.WriteLine(location == null ? "location is null" : location);
            Console.WriteLine(time == null ? "time is null" : time.ToString());

            // Both variables are uninitialized
            // As a value type, an unitialized DateTime variable 
            // is set to a default value of midnight of 1/1/1 (year 1 A.D.), not null.

            Console.WriteLine(default(String));
            Console.WriteLine(default(DateTime));
        }
    }
    
    /*
    location is null
    1/1/0001 12:00:00 AM
    */


# 3. Given an instance circle of the following class:

    public sealed class Circle {
        private double radius;
        public double Calculate(Func<double, double> op) {
            return op(radius);
        }
    }

## Write code to calculate the circumference of the circle, without modifying the Circle class itself.

    using System;

    class Program {

        static void Main() {

            var circle = new Circle();
            var value = circle.Calculate(r => 2 * Math.PI * r);
            Console.WriteLine(value);
        }
    }

    public sealed class Circle {
        private double radius = 5; // default value for double is 0
        public double Calculate(Func<double, double> op) {
            return op(radius);
        }
    }
    

# 4. What is the output of the program below? Explain your answer. (Threading and Async)


    using System;
    using System.Threading;
    using System.Threading.Tasks;

    class Program {
        private static string result;
        private static string result2;

        static void Main() {
            SaySomething();
            SaySomething2();
            Console.WriteLine("Result: " + result);
            Console.WriteLine("Result: " + result2);
        }

        static async Task<string> SaySomething() {
            /* SaySomething() will just output a blank line (not "Hello world!").
             * This is because result will still be uninitialized when Console.WriteLine is called.
             *  
             * The function called by await (in this case Task.Delay) is
             * executed asynchronously, and the line after the await statement
             * isn’t signaled to execute until Task.Delay completes (in 5 milliseconds).
             * However, within that time, control has already returned to the caller,
             * which executes the Console.WriteLine statement on a string that hasn’t
             * yet been initialized.
             *
             */

            await Task.Delay(5);
            result = "Hello world!";
            return "Something";
        }

        static async Task<string> SaySomething2() {
            /*
             * An async method without at least one await statement
             * in it operates just like a synchronous method
             */

            Thread.Sleep(5);
            result2 = "Hello world!";
            return "Something";
        }
    }


# 5. What is the output of the program below? Explain your answer. (Delegate)


    using System;
    using System.Collections.Generic;

    class Program {

        delegate void Printer();
        static void Main() {

            List<Printer> printers = new List<Printer>();
            int i=0;

            for(; i < 10; i++){
                // After we exit the loop, the variable i has been set to 10
                // By the time each delegate is invoked, the value passed to all of them is 10.
                Console.WriteLine("Value Inside Loop: " + i);
                printers.Add(delegate { Console.WriteLine(i); });
            }

            Console.WriteLine("Value After Loop: " + i);

            foreach (var printer in printers){
                printer();
            }
        }
    }

