import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.StringWriter;
import java.util.InputMismatchException;
import java.util.Scanner;

public class App {
    public static int menuLoja(Scanner scam) {
        boolean isTrue = false;
        int option = 0;

        while (!isTrue) {
            System.out.println("1 - Mustang v8 | 20BTC");
            System.out.println("2 - Porsche 911 | 50BTC");
            System.out.println("3 - BMW X5 | 10BTC");
            System.out.println("4 - Exit");

            try {
                option = scam.nextInt();

                if (option >= 1 && option <= 4) {
                    isTrue = true;
                } else {
                    System.out.println("Enter a correct option please ");
                }
            } catch (InputMismatchException e) {
                log(e);
                System.out.println("Enter a correct option please ");
                scam.nextLine();
            } catch (Exception e) {
                log(e);
                System.out.println("Error: ");
                scam.nextLine();
            }
        }
        return option;
    }

    public static void log(Exception e) {
        try (FileWriter write = new FileWriter("C:\\Users\\firey\\Documents\\logs.txt", true); 
                PrintWriter pWriter = new PrintWriter(write)) { 
            StringWriter wWriter = new StringWriter(); 
            e.printStackTrace(new PrintWriter(wWriter)); 
            pWriter.println(wWriter.toString());
        } catch (IOException e1) {
            System.err.println("Error" + e.getMessage());
        }
    }

    public static void main(String[] args) throws Exception {
        Scanner scam = new Scanner(System.in);
        Price prices = new Price();

        int option = 1;

        System.out.println(
                "Welcome to the lonf Store, here you can buy unlimited products for BitCoin. We do not accept DogeCoin "
                        + "\n");

        while (option != 4) {
            option = menuLoja(scam);

            if (option == 1) {
                prices.buy(1);
            } else if (option == 2) {
                prices.buy(2);
            } else if (option == 3) {
                prices.buy(3);
            } else if (option == 4) {
                System.out.println("Exiting...");
            }
        }
        System.out.println("Final Price: " + prices.returnPrice() + "BTC");
    }
}
