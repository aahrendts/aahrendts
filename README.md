- 👋 Hi, I’m @aahrendts
- 👀 I’m interested in Programming and Cybersecurity
- 🌱 I’m currently learning Java Programming
- 💞️ I’m looking to collaborate on codeing and other tech subjects
- 📫 How to reach me doubleaahrendts@gmail.com

import java.io.File;
import java.io.IOException;
import java.util.Scanner;

class Main
{
    public static void main(String[] args) throws IOException
    {
        Scanner input = new Scanner(new File("Lab8Data.txt"));

        // If there is a data in the file, then 16 reads are needed to read that data

        int sentinel = input.nextInt();

        while(sentinel != -999){
            int[][] square = new int[4][4];
            square[0][0] = sentinel;
            for(int i = 1; i < 16; i++)
                square[i/4][i%4] = input.nextInt();
            sentinel = input.nextInt();

            for(int i = 0; i < 4; i++){
                for(int j = 0; j < 3; j++)
                    System.out.print(square[i][j] + " ");
                System.out.println(square[i][3]);
            }

            if( isMagicSquare(square) ){
                System.out.println("IS a magic square");
            }
            else
                System.out.println("NOT a magic square");
            System.out.println();
        }
    }

    public static boolean isMagicSquare(int[][] square){
        int firstRowSum = 0;
        for(int i = 0; i < square.length; i++){ // i is the index of column
            firstRowSum += square[0][i];
        }

        int sumNums; 
        // rows
        for(int i = 1; i < square.length; i++){ // i is the index of row
            sumNums = 0;
            for(int j = 0; j < square.length; j++) // j is the index of column
                sumNums += square[i][j];
            if(sumNums != firstRowSum)
                return false;
        }

        // columns
        for(int i = 0; i < square.length; i++){ // i is the index of row
            sumNums = 0;
            for(int j = 0; j < square.length; j++) // j is the index of column
                sumNums += square[j][i]; //[j][i] to move over ith column
            if(sumNums != firstRowSum)
                return false;
        }

        sumNums = 0; 
        // Main diagnal
        for(int i = 0; i < square.length; i++) // i is the index of row and column
            sumNums += square[i][i];

        if(sumNums != firstRowSum)
                return false;

        sumNums = 0;
        // secondary diagnal
        for(int i = 0; i < square.length; i++) // i is the index of row and column
            sumNums += square[i][square.length - 1 - i];

        if(sumNums != firstRowSum)
                return false;

        return true;
    }

}
