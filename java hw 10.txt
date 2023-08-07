package lottery;


import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;

public class Lottery {

    private final int[] winningNumbers = new int[5];
    private int[][] customerNumbers;

    public void run() {
        initializeWinningNumbers();
        setCostumersNumbers();
        printWinningAndCustomersNumbersTable();
        checkWinningsChekWinningForAllCustomers();

    }

    private void initializeWinningNumbers() {
        Random random = new Random();

        int i = 0;
        while (i < winningNumbers.length) {
            int randomNumber = random.nextInt(50) + 1;

            if (!isThisNumberPresentInArray(randomNumber, winningNumbers)) {
                winningNumbers[i] = randomNumber;
                i++;
            }

        }

    }

    private void setCostumersNumbers() {
        Scanner scanner = new Scanner(System.in);
        customerNumbers = new int[3][5];
        for (int c = 0; c < 3; c++) {
            System.out.println("Customer " + (c + 1) + ": insert your lucky numbers");
            for (int i = 0; i < customerNumbers[c].length; i++) {
                System.out.print((i + 1) + " number: ");
                customerNumbers[c][i] = scanner.nextInt();

            }
        }
    }

    private void printWinningAndCustomersNumbersTable() {
        System.out.println("Winning numbers : Customer numbers");
        for (int c = 0; c < 3; c++) {
            for (int i = 0; i < customerNumbers[c].length; i++) {
                System.out.println(winningNumbers[i] + "           " + customerNumbers[c][i]);
            }
        }
    }

    private void checkWinningsChekWinningForAllCustomers() {
        for (int c = 0; c < 3; c++) {
            int count = 0;

            for (int customerNumber : customerNumbers[c]) {
                if (isThisNumberPresentInArray(customerNumber, winningNumbers)) {
                    count++;
                }
            }

            if (count >= 3) {
                System.out.println("Congratulation, you won");
            } else {
                System.out.println("Try again");
                System.out.println();
            }
        }
    }


    private boolean isThisNumberPresentInArray(int targetNumber, int[] array) {
        for (int currentNumber : array) {
            if (currentNumber == targetNumber) {
                return true;
            }
        }
        return false;
    }


}