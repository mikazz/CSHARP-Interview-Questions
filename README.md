# C# Interview Questions
Collection of different interview questions


# Given an array of ints, write a C# method to sum all the values that are even numbers.




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
