//  Sadra Irannia
// Project for Software Development Course (PDA)
// Date: 31/10/2022


//         ------------------------------------------------------------------------------
//    Import Necessary Java Libraries
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Arrays;
import java.util.Scanner;
import java.io.PrintWriter;
import java.util.SortedMap;
import static java.lang.System.in;

//         ------------------------------------------------------------------------------
//   Declare Global Variables
public class Main {

    // Global Variables
    public static File inputFile; // File to be read

    public static Scanner userInput = new Scanner(in); // To receive user input
    public static Scanner fileScanner = new Scanner(in); // To read from the file

    // Define Global Arrays

    public static String [][] runnerData = new String[16][3];
    public static String [] firstNames = new String[16];
    public static String [] lastNames = new String[16];
    public static int []  times = new int[16];

    // Array for sorted times
    public static String [][]  sortedTimes = new String[16][3];

    // Main Method with password requirement

    //         ------------------------------------------------------------------------------  
    //    Begin Main Program
    public static void main(String[] args) throws FileNotFoundException{

        String password = "g"; // Password for club access
        int attemptsLeft = 3;

        do{
            System.out.println("Welcome to Clyde Runners Club.");
            System.out.println("Please enter your password: ");
            String userPassword = userInput.nextLine();
            if(userPassword.equals(password)){
                System.out.println("Password Accepted.");

                displayMenu();

            } else {
                attemptsLeft--;
                System.out.println("Incorrect password.");// Inform user
                System.out.println("Remaining attempts: "+attemptsLeft+".");
            }
        } while(attemptsLeft != 0);
        System.out.println("Exceeded maximum attempts. Access denied.");
        System.exit(0);
    }

    // Main menu for program options, accessed after password verification
    public static void displayMenu() throws FileNotFoundException{

        int choice = 0;

        do{
            System.out.println("\n\n\nSelect an option:");
            System.out.println("1. Load and Display File");
            System.out.println("2. Sort and Display Runner Times");
            System.out.println("3. Show Fastest Runner");
            System.out.println("4. Show Slowest Runner");
            System.out.println("5. Search Runner by Time");
            System.out.println("6. Check Time Frequency");
            System.out.println("7. Exit Program");
            choice = userInput.nextInt();

            if(choice == 1){
                loadFile();
            }
            else if (choice == 2) {
                sortRunners();
            }
            else if (choice == 3) {
                displayFastest();
            }
            else if (choice == 4) {
                displaySlowest();
            }
            else if (choice == 5) {
                
                findRunnerByTime();
            }
            else if (choice == 6) {
                checkTimeFrequency();
            }
            else if (choice == 7) {
                System.out.println("Thank you. Exiting.");
                System.exit(0);
            }

        } while(choice != 7);
    }

    //         ------------------------------------------------------------------------------  
    //     Option 1
    // This function reads the file and populates arrays with runner data
    public static void loadFile() throws FileNotFoundException{

        String filePath = "src/race_results.txt"; // Path to the file
        inputFile = new File(filePath);
        fileScanner = new Scanner(inputFile);

        String line = null;
        int i = 0;
        // Loop through entire file
        while(fileScanner.hasNextLine()){
            // Process each line
            line = fileScanner.nextLine(); // Read line into local variable
            String [] columns = line.split(" "); // Split line by spaces
            System.out.println(Arrays.deepToString(columns));
            for (int j = 0; j < 3 ; j++){
                    runnerData[i][j] = columns[j];
                }
            i++;
        }

        // Display parsed file data
        System.out.println("\n\nRunner Records : \n"+Arrays.deepToString(runnerData));

        for(int j = 0; j < runnerData.length; j++){  // Populate arrays with runner data
            times[j] = Integer.parseInt(runnerData[j][2]); // Running times
            lastNames[j] = runnerData[j][1]; // Runner last names
            firstNames[j] = runnerData[j][0];  // Runner first names
        }

        System.out.println("First Names: "+Arrays.toString(firstNames));
        System.out.println("Last Names: "+Arrays.toString(lastNames));
        System.out.println("Run Times: "+Arrays.toString(times));

        fileScanner.close(); // Close file
    }

    //         ------------------------------------------------------------------------------  
    //     Option 2
    // Sorts runners by times from slowest to fastest
    public static void sortRunners() throws FileNotFoundException {
        sortedTimes = runnerData;

        String tempFirstName;
        String tempLastName;
        String tempRunTime;
        for(int out = 1; out < sortedTimes.length; out++) {
            for (int inner = out; inner > 0 ; inner--) {
                 int current = Integer.parseInt(sortedTimes[inner][2]);
                 int previous = Integer.parseInt(sortedTimes[inner-1][2]);
                if (current < previous) {
                    tempFirstName = sortedTimes[inner][0];
                    sortedTimes[inner][0] = sortedTimes[inner-1][0];
                    sortedTimes[inner-1][0] = tempFirstName;

                    tempLastName = sortedTimes[inner][1];
                    sortedTimes[inner][1] = sortedTimes[inner-1][1];
                    sortedTimes[inner-1][1] = tempLastName;

                    tempRunTime = sortedTimes[inner][2];
                    sortedTimes[inner][2] = sortedTimes[inner-1][2];
                    sortedTimes[inner-1][2] = tempRunTime;
                }
            }
        }
        saveSortedData();
    }

    // Outputs sorted runner times to a file
    public static void saveSortedData() {

        try{
            PrintWriter writer = new PrintWriter("src/SortedRunners.txt");
            for(int i = 0; i < sortedTimes.length; i++) {
                  writer.print("\nRunner: " + sortedTimes[i][0] + " " + sortedTimes[i][1] + " Time: " + sortedTimes[i][2]);
              }
            writer.close();
            System.out.println("\nSorted Records from Slowest to Fastest: \n"+Arrays.deepToString(sortedTimes));

        }catch (Exception e){
            System.out.println("Unexpected error: please try again.");
        }
    }

    //         ------------------------------------------------------------------------------  
    //     Option 3
    // Finds and displays the fastest runner
    public static void displayFastest() {
        int index = 0;
        int fastestTime = times[0];

        try{
            for(int i = 0; i < times.length; i++) {
                if (times[i] > fastestTime) {
                    fastestTime = times[i];
                    index = i;
                }
            }
            System.out.printf("\nFastest Runner: " + firstNames[index] + " " + lastNames[index] + " Time: " + times[index]);

            PrintWriter writer = new PrintWriter("src/FastestRunner.txt");
            writer.print("Fastest Runner: " + firstNames[index] + " " + lastNames[index] + " Time: " + times[index]);
            writer.close();

    }catch (Exception e){
        System.out.println("Unexpected error: please try again.");
    }
    }
}
