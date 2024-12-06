import java.io.PrintStream;
import java.util.Iterator;
import java.util.Scanner;

public class Main {
   public Main() {
   }

   public static void main(String[] var0) {
      Scanner var1 = new Scanner(System.in);
      Database var2 = new Database();
      var2.addCourse(new Course("CS101", "Intro to Computer Science", "Basic concepts of computer science", 30, "MWF 9-10AM"));
      var2.addCourse(new Course("ENG102", "English Literature", "Study of classic English literature", 25, "TTH 1-2:30PM"));
      var2.addStudent(new StudentCourse("S001", "Alice"));
      var2.addStudent(new StudentCourse("S002", "Bob"));

      label46:
      while(true) {
         System.out.println("\n1. List Courses");
         System.out.println("2. Register for a Course");
         System.out.println("3. Drop a Course");
         System.out.println("4. Exit");
         System.out.print("Choose an option: ");
         int var3 = var1.nextInt();
         String var4;
         StudentCourse var5;
         String var6;
         Course var7;
         switch (var3) {
            case 1:
               System.out.println("\nAvailable Courses:");
               Iterator var8 = var2.getAvailableCourses().iterator();

               while(true) {
                  if (!var8.hasNext()) {
                     continue label46;
                  }

                  Course var9 = (Course)var8.next();
                  PrintStream var10000 = System.out;
                  String var10001 = var9.getCode();
                  var10000.println("Code: " + var10001 + ", Title: " + var9.getTitle() + ", Available Slots: " + (var9.getCapacity() - var9.getEnrolledStudents()));
               }
            case 2:
               System.out.print("Enter Student ID: ");
               var4 = var1.next();
               var5 = var2.getStudent(var4);
               if (var5 != null) {
                  System.out.print("Enter Course Code: ");
                  var6 = var1.next();
                  var7 = var2.getCourse(var6);
                  if (var7 != null && var7.hasAvailableSlots()) {
                     if (var5.registerCourse(var7)) {
                        System.out.println("Registered successfully.");
                     } else {
                        System.out.println("Registration failed.");
                     }
                     break;
                  }

                  System.out.println("Course not found or full.");
                  break;
               }

               System.out.println("Student not found.");
               break;
            case 3:
               System.out.print("Enter Student ID: ");
               var4 = var1.next();
               var5 = var2.getStudent(var4);
               if (var5 != null) {
                  System.out.print("Enter Course Code: ");
                  var6 = var1.next();
                  var7 = var2.getCourse(var6);
                  if (var7 != null) {
                     if (var5.dropCourse(var7)) {
                        System.out.println("Dropped successfully.");
                     } else {
                        System.out.println("Drop failed.");
                     }
                  } else {
                     System.out.println("Course not found.");
                  }
               } else {
                  System.out.println("Student not found.");
               }
               break;
            case 4:
               System.out.println("Exiting. Thank you!");
               var1.close();
               return;
            default:
               System.out.println("Invalid option. Please try again.");
         }
      }
   }
}
