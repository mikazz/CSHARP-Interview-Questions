# C# Interview Questions
Collection of different interview questions


# Given an array of ints, write a C# method to sum all the values that are even numbers.

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


# What is the output of the short program below? Explain your answer.
## Default datatype values

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


# Given an instance circle of the following class:

    public sealed class Circle {
        private double radius;
        public double Calculate(Func<double, double> op) {
            return op(radius);
        }
    }

# write code to calculate the circumference of the circle, without modifying the Circle class itself.

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
