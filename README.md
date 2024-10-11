//task 1 code
import java.util.Random;
import java.util.Scanner;

public class GuessingGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean playAgain = true;
        int score = 0;

        while (playAgain) {
            int min = 1;
            int max = 100;
            int maxAttempts = 5;
            int attempts = 0;

            Random random = new Random();
            int randomNumber = random.nextInt(max - min + 1) + min;

            System.out.println("A random number between " + min + " and " + max + " has been generated.");
            boolean guessedCorrectly = false;

            while (attempts < maxAttempts && !guessedCorrectly) {
                System.out.print("Attempt " + (attempts + 1) + "/" + maxAttempts + ". Enter your guess: ");
                int userGuess = scanner.nextInt();
                attempts++;

                if (userGuess == randomNumber) {
                    System.out.println("Correct! You guessed the number.");
                    guessedCorrectly = true;
                    score++;
                } else if (userGuess > randomNumber) {
                    System.out.println("Too high! Try again.");
                } else {
                    System.out.println("Too low! Try again.");
                }
            }

            if (!guessedCorrectly) {
                System.out.println("Sorry, you've used all attempts. The correct number was: " + randomNumber);
            }

            System.out.println("Your current score: " + score);
            System.out.print("Do you want to play another round? (yes/no): ");
            String response = scanner.next();

            if (!response.equalsIgnoreCase("yes")) {
                playAgain = false;
            }
        }

        System.out.println("Thanks for playing! Final score: " + score);
        scanner.close();
    }
}
//task 2 code
import java.util.Scanner;

public class MarksCalculator {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Input the number of subjects
        System.out.print("Enter the number of subjects: ");
        int numberOfSubjects = scanner.nextInt();

        // Initialize variables
        int totalMarks = 0;
        int marks;
        
        // Take input of marks for each subject
        for (int i = 1; i <= numberOfSubjects; i++) {
            System.out.print("Enter marks obtained in subject " + i + " (out of 100): ");
            marks = scanner.nextInt();
            totalMarks += marks;
        }

        // Calculate average percentage
        double averagePercentage = (double) totalMarks / numberOfSubjects;

        // Determine grade
        char grade;
        if (averagePercentage >= 90) {
            grade = 'A';
        } else if (averagePercentage >= 80) {
            grade = 'B';
        } else if (averagePercentage >= 70) {
            grade = 'C';
        } else if (averagePercentage >= 60) {
            grade = 'D';
        } else {
            grade = 'F';
        }

        // Display results
        System.out.println("\nResults:");
        System.out.println("Total Marks: " + totalMarks + " / " + (numberOfSubjects * 100));
        System.out.printf("Average Percentage: %.2f%%\n", averagePercentage);
        System.out.println("Grade: " + grade);

        scanner.close();
    }
}





//task 3 code 
import java.util.Scanner;

// Class to represent the user's bank account
class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Successfully deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Successfully withdrawn: $" + amount);
            return true;
        } else if (amount > balance) {
            System.out.println("Insufficient balance for this withdrawal.");
            return false;
        } else {
            System.out.println("Invalid withdrawal amount.");
            return false;
        }
    }
}

// Class to represent the ATM machine
class ATM {
    private BankAccount account;

    public ATM(BankAccount account) {
        this.account = account;
    }

    public void withdraw(double amount) {
        if (account.withdraw(amount)) {
            System.out.println("Withdrawal successful. Current balance: $" + account.getBalance());
        } else {
            System.out.println("Withdrawal failed.");
        }
    }

    public void deposit(double amount) {
        account.deposit(amount);
        System.out.println("Current balance: $" + account.getBalance());
    }

    public void checkBalance() {
        System.out.println("Current balance: $" + account.getBalance());
    }

    public void showMenu() {
        System.out.println("\nATM Menu:");
        System.out.println("1. Withdraw");
        System.out.println("2. Deposit");
        System.out.println("3. Check Balance");
        System.out.println("4. Exit");
    }

    public void runATM() {
        Scanner scanner = new Scanner(System.in);
        boolean exit = false;

        while (!exit) {
            showMenu();
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    withdraw(withdrawAmount);
                    break;
                case 2:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    deposit(depositAmount);
                    break;
                case 3:
                    checkBalance();
                    break;
                case 4:
                    exit = true;
                    System.out.println("Exiting ATM. Thank you!");
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }

        scanner.close();
    }
}

// Main class to run the program
public class ATMSimulation {
    public static void main(String[] args) {
        BankAccount userAccount = new BankAccount(500.00);  // Initial balance of $500
        ATM atm = new ATM(userAccount);
        atm.runATM();
    }
}
//task 4
import java.util.*;

class QuizQuestion {
    String question;
    String[] options;
    int correctAnswer;

    public QuizQuestion(String question, String[] options, int correctAnswer) {
        this.question = question;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestion() {
        return question;
    }

    public String[] getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }
}

public class Quiz {
    private List<QuizQuestion> questions;
    private int score;
    private List<String> results;

    public Quiz() {
        questions = new ArrayList<>();
        score = 0;
        results = new ArrayList<>();
        loadQuestions();
    }

    private void loadQuestions() {
        questions.add(new QuizQuestion(
                "What is the capital of France?",
                new String[]{"1. Berlin", "2. Madrid", "3. Paris", "4. Rome"},
                3
        ));
        questions.add(new QuizQuestion(
                "Which planet is known as the Red Planet?",
                new String[]{"1. Earth", "2. Mars", "3. Jupiter", "4. Venus"},
                2
        ));
        questions.add(new QuizQuestion(
                "What is the largest ocean on Earth?",
                new String[]{"1. Indian", "2. Atlantic", "3. Arctic", "4. Pacific"},
                4
        ));
    }

    private void startQuiz() {
        Scanner scanner = new Scanner(System.in);

        for (QuizQuestion question : questions) {
            System.out.println("\n" + question.getQuestion());

            // Display options
            String[] options = question.getOptions();
            for (String option : options) {
                System.out.println(option);
            }

            // Start timer
            Timer timer = new Timer();
            TimerTask task = new TimerTask() {
                @Override
                public void run() {
                    System.out.println("\nTime's up!");
                    System.exit(0);  // End the program if time runs out
                }
            };
            timer.schedule(task, 10000);  // 10-second timer for each question

            System.out.print("Enter your answer (1-4): ");
            int answer = scanner.nextInt();

            timer.cancel();  // Stop the timer if the answer is submitted within time

            if (answer == question.getCorrectAnswer()) {
                System.out.println("Correct!");
                score++;
                results.add(question.getQuestion() + ": Correct");
            } else {
                System.out.println("Incorrect!");
                results.add(question.getQuestion() + ": Incorrect");
            }
        }

        displayResults();
    }

    private void displayResults() {
        System.out.println("\nQuiz Complete!");
        System.out.println("Your score: " + score + " / " + questions.size());

        System.out.println("\nSummary of Answers:");
        for (String result : results) {
            System.out.println(result);
        }
    }

    public static void main(String[] args) {
        Quiz quiz = new Quiz();
        quiz.startQuiz();
    }
}






//task 5
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Class to represent a Course
class Course {
    private String courseCode;
    private String title;
    private String description;
    private int capacity;
    private String schedule;
    private List<Student> registeredStudents;

    public Course(String courseCode, String title, String description, int capacity, String schedule) {
        this.courseCode = courseCode;
        this.title = title;
        this.description = description;
        this.capacity = capacity;
        this.schedule = schedule;
        this.registeredStudents = new ArrayList<>();
    }

    public String getCourseCode() {
        return courseCode;
    }

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    public String getSchedule() {
        return schedule;
    }

    public int getCapacity() {
        return capacity;
    }

    public int getAvailableSlots() {
        return capacity - registeredStudents.size();
    }

    public void registerStudent(Student student) {
        if (getAvailableSlots() > 0) {
            registeredStudents.add(student);
            System.out.println(student.getName() + " successfully registered for " + title);
        } else {
            System.out.println("Course is full. Cannot register for " + title);
        }
    }

    public void dropStudent(Student student) {
        if (registeredStudents.remove(student)) {
            System.out.println(student.getName() + " successfully dropped from " + title);
        } else {
            System.out.println("Student is not registered in this course.");
        }
    }

    public boolean isStudentRegistered(Student student) {
        return registeredStudents.contains(student);
    }
}

// Class to represent a Student
class Student {
    private String studentId;
    private String name;
    private List<Course> registeredCourses;

    public Student(String studentId, String name) {
        this.studentId = studentId;
        this.name = name;
        this.registeredCourses = new ArrayList<>();
    }

    public String getStudentId() {
        return studentId;
    }

    public String getName() {
        return name;
    }

    public List<Course> getRegisteredCourses() {
        return registeredCourses;
    }

    public void registerForCourse(Course course) {
        if (!registeredCourses.contains(course)) {
            course.registerStudent(this);
            registeredCourses.add(course);
        } else {
            System.out.println("Already registered for this course.");
        }
    }

    public void dropCourse(Course course) {
        if (registeredCourses.contains(course)) {
            course.dropStudent(this);
            registeredCourses.remove(course);
        } else {
            System.out.println("You are not registered for this course.");
        }
    }
}

// Main class to manage course registration system
public class CourseRegistrationSystem {
    private List<Course> courses;
    private List<Student> students;

    public CourseRegistrationSystem() {
        courses = new ArrayList<>();
        students = new ArrayList<>();
        loadCourses();
    }

    private void loadCourses() {
        courses.add(new Course("CS101", "Introduction to Programming", "Learn the basics of programming", 30, "Mon/Wed 10-11 AM"));
        courses.add(new Course("MATH201", "Calculus I", "Introduction to Calculus", 25, "Tue/Thu 9-10 AM"));
        courses.add(new Course("ENG301", "Advanced English", "Advanced level English studies", 20, "Fri 2-4 PM"));
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public Student getStudentById(String studentId) {
        for (Student student : students) {
            if (student.getStudentId().equals(studentId)) {
                return student;
            }
        }
        return null;
    }

    public void displayCourses() {
        System.out.println("\nAvailable Courses:");
        for (Course course : courses) {
            System.out.println(course.getCourseCode() + " - " + course.getTitle() + " | " + course.getDescription() + 
                    " | Schedule: " + course.getSchedule() + " | Available slots: " + course.getAvailableSlots());
        }
    }

    public Course getCourseByCode(String courseCode) {
        for (Course course : courses) {
            if (course.getCourseCode().equals(courseCode)) {
                return course;
            }
        }
        return null;
    }

    public void runSystem() {
        Scanner scanner = new Scanner(System.in);

        // Add some students
        Student student1 = new Student("S001", "Alice");
        Student student2 = new Student("S002", "Bob");
        addStudent(student1);
        addStudent(student2);

        boolean exit = false;
        while (!exit) {
            System.out.println("\n1. Display Available Courses");
            System.out.println("2. Register for a Course");
            System.out.println("3. Drop a Course");
            System.out.println("4. Check Registered Courses");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline

            switch (choice) {
                case 1:
                    displayCourses();
                    break;
                case 2:
                    System.out.print("Enter your student ID: ");
                    String studentId = scanner.nextLine();
                    Student student = getStudentById(studentId);
                    if (student != null) {
                        displayCourses();
                        System.out.print("Enter the course code to register: ");
                        String courseCode = scanner.nextLine();
                        Course course = getCourseByCode(courseCode);
                        if (course != null) {
                            student.registerForCourse(course);
                        } else {
                            System.out.println("Invalid course code.");
                        }
                    } else {
                        System.out.println("Invalid student ID.");
                    }
                    break;
                case 3:
                    System.out.print("Enter your student ID: ");
                    studentId = scanner.nextLine();
                    student = getStudentById(studentId);
                    if (student != null) {
                        List<Course> registeredCourses = student.getRegisteredCourses();
                        if (!registeredCourses.isEmpty()) {
                            System.out.println("\nRegistered Courses:");
                            for (Course c : registeredCourses) {
                                System.out.println(c.getCourseCode() + " - " + c.getTitle());
                            }
                            System.out.print("Enter the course code to drop: ");
                            String dropCourseCode = scanner.nextLine();
                            Course dropCourse = getCourseByCode(dropCourseCode);
                            if (dropCourse != null) {
                                student.dropCourse(dropCourse);
                            } else {
                                System.out.println("Invalid course code.");
                            }
                        } else {
                            System.out.println("You are not registered for any courses.");
                        }
                    } else {
                        System.out.println("Invalid student ID.");
                    }
                    break;
                case 4:
                    System.out.print("Enter your student ID: ");
                    studentId = scanner.nextLine();
                    student = getStudentById(studentId);
                    if (student != null) {
                        List<Course> registeredCourses = student.getRegisteredCourses();
                        if (!registeredCourses.isEmpty()) {
                            System.out.println("\nRegistered Courses:");
                            for (Course c : registeredCourses) {
                                System.out.println(c.getCourseCode() + " - " + c.getTitle());
                            }
                        } else {
                            System.out.println("You are not registered for any courses.");
                        }
                    } else {
                        System.out.println("Invalid student ID.");
                    }
                    break;
                case 5:
                    exit = true;
                    System.out.println("Exiting system.");
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }

        scanner.close();
    }

    public static void main(String[] args) {
        CourseRegistrationSystem system = new CourseRegistrationSystem();
        system.runSystem();
    }
}
