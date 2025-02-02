# Task: Process File to Sum and Multiply Numbers

This C# program reads a file containing numbers (one per line), calculates their sum and product, and then displays the results. It gracefully handles errors like missing files and invalid number formats.

🔹 How it works:

1️⃣ The user is prompted to enter the name or path of a file.

2️⃣ The program reads all lines from the file and tries to convert each line into an integer.

3️⃣ If a line is not a valid number, it throws a format error.

4️⃣ It then computes both the sum and the product of the numbers.

5️⃣ Any errors (e.g., file not found, formatting issues) are caught and a friendly error message is displayed.

6️⃣ The process repeats until the user chooses to quit.

```
using System;
using System.Collections.Generic;
using System.IO; 

class Program
{
    static void Main()
    {
        while (true)
        {
            try
            {
                Console.Write("Write the name of the file or its path: ");
                string input = Console.ReadLine();
 
                string[] lines = File.ReadAllLines(input);

                List<int> numbers = new List<int>();
                foreach (string line in lines)
                {
                    if (int.TryParse(line, out int num))
                    {
                        numbers.Add(num);
                    }
                    else
                    {
                        throw new FormatException("Error formatting: invalid number found.");
                    }
                }

                int SumNumbers(List<int> nums)
                {
                    int sum = 0;
                    foreach (int num in nums)
                    {
                        sum += num;
                    }
                    return sum;
                }

                int MultiplyNumbers(List<int> nums)
                {
                    int product = 1;
                    foreach (int num in nums)
                    {
                        product *= num;
                    }
                    return product;
                }

                int sum = SumNumbers(numbers);
                int product = MultiplyNumbers(numbers);

                // Display results
                Console.WriteLine($"Sum of numbers: {sum}");
                Console.WriteLine($"Product of numbers: {product}");
            }
            catch (FileNotFoundException)
            {
                Console.WriteLine("Error: File not found.");
            }
            catch (FormatException fe)
            {
                Console.WriteLine($"Error: {fe.Message}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
            finally
            {
                Console.WriteLine("Operation completed!");
            }

            Console.WriteLine("To quit type `q`, to continue press any key");
            if (Console.ReadLine().Equals("q", StringComparison.OrdinalIgnoreCase))
                break;
        }
    }
}

```
