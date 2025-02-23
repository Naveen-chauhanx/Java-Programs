import java.util.*;

class Detail {

    final int Account_no;
    final int pin;

    Detail(int A, int P) {
        this.Account_no = A;
        this.pin = P;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Detail detail = (Detail) obj;
        return Account_no == detail.Account_no && pin == detail.pin;
    }

    @Override
    public int hashCode() {
        return Objects.hash(Account_no, pin);
    }
}

public class ATM {

    static Scanner sc = new Scanner(System.in);
    static Map<Detail, Double> Accounts = new HashMap<>();
    static int ac = 412095;

    static void adding_Account() {
        System.out.println("Set PIN");
        Detail d = new Detail(ac++, sc.nextInt());
        Accounts.put(d, 0.0);
    }

    static void access_Account() {
        System.out.print("Enter Account no: ");
        int accountNo = sc.nextInt();
        System.out.print("PIN: ");
        int pin = sc.nextInt();
    
        Detail d = new Detail(accountNo, pin);
    
        if (!Accounts.containsKey(d)) { 
            System.out.println("Invalid Account or PIN");
            return;
        }
    
        while (true) {
            System.out.println("\n1 -> Deposit Amount");
            System.out.println("2 -> Withdraw Amount");
            System.out.println("3 -> Check Balance");
            System.out.println("4 -> Exit");
    
            System.out.print("Press the Number: ");
            int x = sc.nextInt();
            double amount;
    
            switch (x) {
                case 1:
                    System.out.print("Enter the Amount you want to deposit: ");
                    amount = sc.nextDouble();
                    Accounts.put(d, Accounts.get(d) + amount);
                    System.out.println("Successfully deposited " + amount);
                    break;
    
                case 2:
                    System.out.print("Enter the Amount you want to withdraw: ");
                    amount = sc.nextDouble();
                    if (amount + 0.50 > Accounts.get(d)) {
                        System.out.println("Insufficient Balance");
                    } else {
                        System.out.println("Successful withdrawal: " + amount);
                        Accounts.put(d, Accounts.get(d) - amount - 0.50);
                    }
                    break;
    
                case 3:
                    System.out.println("Balance: $" + Accounts.getOrDefault(d, 0.0));
                    break;
    
                case 4:
                    System.out.println("Thank you for accessing account " + accountNo);
                    return;
    
                default:
                    System.out.println("Invalid option, try again\n");
            }
        }
    }
    

    static void display_Accounts() {
        for(Map.Entry<Detail, Double> e : Accounts.entrySet()){
            System.out.println("Account no: " + e.getKey().Account_no + " | Pin: " + e.getKey().pin + " | Balance: $" + e.getValue());
        }
    }

    public static void main(String[] args) {

        while (true) {

            System.out.println("1 -> For Adding Account");
            System.out.println("2 -> Access Bank Account");
            System.out.println("3 -> Display All Bank Account");
            System.out.println("4 -> Exit \n");
            System.out.print("Press the Digit :- ");

            int x = sc.nextInt();
            switch (x) {
                case 1:
                    adding_Account();
                    break;
                case 2:
                    access_Account();
                    break;
                case 3:
                    display_Accounts();
                    break;
                case 4:
                    System.out.println("Thank you for using");
                    sc.close();
                    return;
                default:
                    System.out.println("Invalid value entered, please try again");
            }
        }
    }
}
