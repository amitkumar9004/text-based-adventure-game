# text-based-adventure-game
import java.util.Scanner;

public class AdventureGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean playAgain = true;

        while (playAgain) {
            startAdventure(scanner);
            playAgain = askToPlayAgain(scanner);
        }

        System.out.println("Thank you for playing! Goodbye!");
        scanner.close();
    }

    private static void printWithBorder(String message) {
        String border = "*".repeat(message.length() + 4);
        System.out.println("\n" + border);
        System.out.println("* " + message + " *");
        System.out.println(border + "\n");
    }

    private static String makeChoice(Scanner scanner, String prompt, String[] choices) {
        String choice;
        while (true) {
            System.out.print(prompt);
            choice = scanner.nextLine().trim().toLowerCase();
            for (String validChoice : choices) {
                if (choice.equals(validChoice)) {
                    return choice;
                }
            }
            System.out.println("\nInvalid choice. Please try again.");
        }
    }

    private static void startAdventure(Scanner scanner) {
        printWithBorder("Welcome to the Adventure Game!");
        System.out.println("You find yourself in a dark forest with two paths in front of you.");

        String choice1 = makeChoice(scanner, "Do you take the left path or the right path? (left/right): ", new String[]{"left", "right"});

        if (choice1.equals("left")) {
            System.out.println("\nYou take the left path and encounter a river.");
            String choice2 = makeChoice(scanner, "Do you swim across or build a raft? (swim/raft): ", new String[]{"swim", "raft"});

            if (choice2.equals("swim")) {
                System.out.println("\nYou decide to swim across the river but the current is too strong. You get swept away and end up on an unknown shore.");
                printWithBorder("The End");
            } else if (choice2.equals("raft")) {
                System.out.println("\nYou build a raft and safely cross the river. On the other side, you find a treasure chest!");
                printWithBorder("Congratulations! You found the treasure!");
            }

        } else if (choice1.equals("right")) {
            System.out.println("\nYou take the right path and encounter a wild animal.");
            String choice2 = makeChoice(scanner, "Do you run away or try to tame it? (run/tame): ", new String[]{"run", "tame"});

            if (choice2.equals("run")) {
                System.out.println("\nYou run away and find a hidden cave where you can rest and stay safe for the night.");
                printWithBorder("The End");
            } else if (choice2.equals("tame")) {
                System.out.println("\nYou try to tame the animal and succeed. The animal becomes your loyal companion and guides you to a hidden village.");
                printWithBorder("Congratulations! You found a new friend and a safe place to stay!");
            }
        }
    }

    private static boolean askToPlayAgain(Scanner scanner) {
        String choice = makeChoice(scanner, "Do you want to play again? (yes/no): ", new String[]{"yes", "no"});
        return choice.equals("yes");
    }
}
