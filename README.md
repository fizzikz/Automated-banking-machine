# Automated-banking-machine
automated bank teller with capability of storing, editing database of clients and performing essential banking transactions. 
package bank;

import java.io.File;
import java.io.IOException;
import java.util.Scanner;

/**
 *
 * @author Vishnu
 */
public class Practice {
    public static void main(String[] args) throws IOException{
        
        Scanner keyboard = new Scanner (System.in);
        ATM Atmobject = new ATM() ; 
        Scanner Filecheck = new Scanner(new File("C:/Users/Vishnu/Documents/2SH4 labs/bank/Bank/build/classes/bank/filefullofmoney.txt")); 
 
        while(Filecheck.hasNext()){
             
             Atmobject.PIN  = Filecheck.nextInt(); // First number from the file is inialized as the PIN
             Atmobject.Chequing_Balance = Filecheck.nextDouble(); // Second number from the file is inialized as the the initial Chequing Balance
             Atmobject.Savings_Balance = Filecheck.nextDouble(); //Third number from the file is inialized as the initial Saving Balance
        }
        Filecheck.close(); // Closes the file 
        
        int PIN_check , counter = 2 , option, next_option ;
        double money_added ;
        
        System.out.printf("Enter PIN number: ");
        PIN_check = keyboard.nextInt();
        
        while(PIN_check != Atmobject.PIN && counter >0){ // If the pin entered doesn't match the file PIN
            System.out.printf("The Pin entered is wrong. Please try again.\n" );
            System.out.printf("Enter PIN number: ");
            PIN_check = keyboard.nextInt() ;
            counter-- ;
        }
        
        if (PIN_check == Atmobject.PIN){
           Atmobject.menu();
           System.out.println("Your option is : ");
           option = keyboard.nextInt();
           
           switch(option){
               case 1 :
                   Atmobject.deposit_to_Balance();
                   Atmobject.transaction();
                   break;
               
               case 2 : 
                   Atmobject.withdrawal_to_Balance();
                   Atmobject.transaction();
                   break ;
                   
               case 3 : 
                   Atmobject.transfer();
                   Atmobject.transaction();
                   break;
                   
               case 4 :
                   Atmobject.final_Chequing_Balance = Atmobject.Chequing_Balance ;
                   Atmobject.final_Savings_Balance = Atmobject.Savings_Balance ;
                   Atmobject.transaction();
                   break;
                   
               default: 
                   System.err.println("Sorry, wrong option.");
                   Atmobject.final_Chequing_Balance = Atmobject.Chequing_Balance ;
                   Atmobject.final_Savings_Balance = Atmobject.Savings_Balance ;
                   break;
           }
        }

       else{
           System.err.printf("Sorry, Wrong Pin again. You had your 3 tries.\n" );
           Atmobject.final_Chequing_Balance = Atmobject.Chequing_Balance ;
           Atmobject.final_Savings_Balance = Atmobject.Savings_Balance ;
       }
        // Writes the file  with same PIN , updated Chequing and Saving Balance.
        writefile WriteFile = new writefile(new String(Atmobject.PIN + " "+Atmobject.final_Chequing_Balance+" "+Atmobject.final_Savings_Balance));
        System.out.println("\nHave a Wonderful Day\n"); // A nice greeting message :)
    }
}
