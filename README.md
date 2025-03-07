# NumberGuessingGame-java
This Java application is a simple guessing number game where the computer selects a random number between a specified range, and the player tries to guess that number. The game provides feedback to the player after each guess, guiding them to adjust their next guess based on whether it was too high or too low.

Features:
Random Number Generation: The computer generates a random number between a specified minimum and maximum value.
User Input: The player inputs their guess through standard input (console).
Feedback Mechanism: After each guess, the player receives feedback indicating whether their guess was too high, too low, or correct.
Game Loop: The game continues until the player guesses the correct number.
Technologies Used:
Java programming language
How to Use:
Clone the repository to your local machine.
Open the project in your preferred Java IDE or compile and run using command line tools.
Follow the instructions printed in the console to play the game:
Enter your guess when prompted.
Receive feedback after each guess to guide your subsequent guesses.
Continue guessing until you correctly identify the number.
example:

Guess the number between 1 and 100:
Your guess: 50
Too low! Try guessing a higher number.
Your guess: 75
Too high! Try guessing a lower number.
Your guess: 60
Too high! Try guessing a lower number.
Your guess: 55
Too high! Try guessing a lower number.
Your guess: 52
Too low! Try guessing a higher number.
Your guess: 53
Congratulations! You guessed the number 53 correctly!

CODE:
import java.util.ArrayList;
import java.util.Random;
import java.util.Scanner;

public class NumberGuessing{

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        System.out.println(name + ", welcome to the number guessing game!");
        System.out.println("In this game, you need to guess the secret number generated by the system.");

        guessNumber();
    }

    public static void guessNumber() {
        Random random = new Random();
        int secretNumber = random.nextInt(100) + 1;
        ArrayList<Integer> divisors = new ArrayList<>();

        // Find divisors of the secret number
        for (int i = 1; i <= secretNumber; i++) {
            if (secretNumber % i == 0) {
                divisors.add(i);
            }
        }

        Scanner scanner = new Scanner(System.in);
        int attempts = 0;

        while (true) {
            try {
                System.out.print("Guess a number between 1 and 100: ");
                int guess = scanner.nextInt();
                attempts++;

                if (guess == secretNumber) {
                    System.out.println("Congratulations, you guessed the number!");
                    System.out.println("Number of attempts: " + attempts);
                    
                    // Star rating based on attempts
                    if (attempts <= 3) {
                        System.out.println("Excellent, you got 5 stars *****");
                    } else if (attempts == 4) {
                        System.out.println("Very good, you got 4 stars ****");
                    } else {
                        System.out.println("Good, you got 1 star *");
                        System.out.println("Try hard to get big stars!");
                    }

                    System.out.print("Do you want to play the game again? (1 to continue, 0 to stop): ");
                    int playAgain = scanner.nextInt();
                    if (playAgain == 1) {
                        guessNumber(); // Restart the game
                    } else {
                        break; // Exit the game
                    }
                } else if (guess < secretNumber) {
                    System.out.println("Your guessed number " + guess + " is lesser than the secret number, try again!");
                } else {
                    System.out.println("Your guessed number " + guess + " is greater than the secret number, try again!");
                }

                // Provide hints based on attempts
                switch (attempts) {
                    case 1:
                        if (secretNumber <= 50) {
                            System.out.println("Hint 1: The secret number is less than fifty (50)");
                        } else {
                            System.out.println("Hint 1: The secret number is above fifty (50)");
                        }
                        break;
                    case 2:
                        if (secretNumber % 2 == 0) {
                            System.out.println("Hint 2: The secret number is even");
                        } else {
                            System.out.println("Hint 2: The secret number is odd");
                        }
                        break;
                    case 3:
                        if (isPrime(secretNumber)) {
                            System.out.println("Hint 3: The secret number is a prime number.");
                        } else {
                            System.out.println("Hint 3: The secret number is not a prime number.");
                        }
                        break;
                    case 4:
                        System.out.print("Hint 4: The secret number is divisible by: ");
                        for (int divisor : divisors) {
                            System.out.print(divisor + " ");
                        }
                        System.out.println();
                        break;
                    case 5:
                        System.out.println("Hint 5: The square of the secret number is: " + (secretNumber * secretNumber));
                        break;
                    case 6:
                        System.out.println("Hint 6: The cube root of the secret number is: " + Math.cbrt(secretNumber));
                        break;
                }
            } catch (Exception e) {
                System.out.println("Invalid input, please enter a number between 1 and 100.");
                scanner.nextLine(); // Clear the input buffer
            }
        }
    }

    public static boolean isPrime(int n) {
        if (n < 2) {
            return false;
        }
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }
}
