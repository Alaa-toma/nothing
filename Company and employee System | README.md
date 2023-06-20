# java-
// this was a university project 
public class Employee {  
    private int empNo ;
    private String name ;
    private int age ;
    private int yearOfWork  ;
    private double payRatePerHour ;
    private PaySheet [] PaySheet ;

    public Employee (){
        
    }  
    public Employee (int empNo , String name ,int age ,int yearOfWork ,double payRatePerHour, PaySheet [] PaySheet ){
        
        this.empNo = empNo;
        this.name = name ;
        this.age= age ;
        this.yearOfWork = yearOfWork ;
        this.payRatePerHour = payRatePerHour ;
        this.PaySheet  = PaySheet  ;  
    }   
    public int getEmpNo() {
        return empNo;
    }
    public void setEmpNo(int empNo) {
        this.empNo = empNo;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getYearOfWork() {
        return yearOfWork;
    }

    public void setYearOfWork(int yearOfWork) {
        this.yearOfWork = yearOfWork;
    }

    public double getPayRatePerHour() {
        return payRatePerHour;
    }

    public void setPayRatePerHour(double payRatePerHour) {
        this.payRatePerHour = payRatePerHour;
    }

    public PaySheet[] getPaySheet() {
        return PaySheet;
    }

    public void setPaySheet(PaySheet[] PaySheet) {
        this.PaySheet = PaySheet;
    }

    @Override
    public String toString() {
        return "Employee{" + "empNo=" + empNo + ", name=" + name + ", age=" + age + ", yearOfWork=" + yearOfWork + ", payRatePerHour=" + payRatePerHour + ", PaySheet=" + Arrays.toString(PaySheet) + '}';
    }  
}
// ____________________________________________________________________________

public class PaySheet {
    
    private String weekEndingDate ;
    private int [] workingHourInDay ; 
    
    public PaySheet (){
        
    }
    
     public PaySheet (String weekEndingDate ,  int workingHourInDay []){
     
         this.weekEndingDate = weekEndingDate ;
         this.workingHourInDay = workingHourInDay ;
     }
    public String getWeekEndingDate() {
        return weekEndingDate;
    }
    public void setWeekEndingDate(String weekEndingDate) {
        this.weekEndingDate = weekEndingDate;
    }
    public int[] getWorkingHourInDay() {
        return workingHourInDay;
    }
    public void setWorkingHourInDay(int[] workingHourInDay) {
        this.workingHourInDay = workingHourInDay;
    }
    @Override
    public String toString() {
        return "PaySheet{" + "weekEndingDate=" + weekEndingDate + ", workingHourInDay=" + Arrays.toString(workingHourInDay) + '}';
    }
}

// ____________________________________________________________________________
public class Main {

// to print the information about the employees & their work 

    public static void printinfo(Employee arr[]) {
        System.out.println("EmpNop\t Week \t Total Days/Hours \t Weekly Payment ");

        for (int i = 0; i < arr.length; i++) { // array employee

            for (int q = 0; q < arr[i].getPaySheet().length; q++) { // array weeks
                int m = 0, j = 0;
                double wp = 0;
                for (int w = 0; w < arr[i].getPaySheet()[q].getWorkingHourInDay().length; w++) {
                    if (arr[i].getPaySheet()[q].getWorkingHourInDay()[w] > 0) {
                        m++;
                        j += arr[i].getPaySheet()[q].getWorkingHourInDay()[w];

                    }
                }
                wp = (arr[i].getPayRatePerHour() * j);
                System.out.println(arr[i].getEmpNo() + " \t  " + (q + 1) + "\t\t" + m + "/" + j + "\t\t" + wp);
            }
        }       
    }
//----------------------------------------------------------------------------------------------

// to find the warned employee , An employee is warned if he is absent for two or more days in two consecutive weeks.

    public static void printWarnedEmployees(Employee arr[]) {

        for (int i = 0; i < arr.length; i++) { // objects 
            
            for (int h = 0; h < arr[i].getPaySheet().length - 1; h++) { // arrays of working days .. weeks
                int a = 0, b = 0 ;
                for (int r = 0; r < arr[i].getPaySheet()[h].getWorkingHourInDay().length; r++) { // working days
                    if (arr[i].getPaySheet()[h].getWorkingHourInDay()[r] == 0) {
                        a++;
                    }
                    if (arr[i].getPaySheet()[h + 1].getWorkingHourInDay()[r] == 0) {
                        b++;
                    }
                }
                if (a >= 2 && b >= 2) {
                System.out.println(arr[i].getName());
            }
            }
            
        }         
    }
    
// ----------------------------------------------------------------------------------------------
    
    public static double payinweeks(Employee a) {
        int p = 0;
        for (int i = 0; i < a.getPaySheet().length; i++) {
            for (int m = 0; m < a.getPaySheet()[i].getWorkingHourInDay().length; m++) {
                if (a.getPaySheet()[i].getWorkingHourInDay()[m] > 0) {
                    p += a.getPaySheet()[i].getWorkingHourInDay()[m];
                }
            }
        }
        return p;
    }

 
    public static boolean iswarned(Employee m) {

        int a = 0, b = 0 , r =0 ;
        for (int i = 0; i < m.getPaySheet().length - 1; i++) {
            for (int y = 0; y < m.getPaySheet()[i].getWorkingHourInDay().length; y++) {
                if (m.getPaySheet()[i].getWorkingHourInDay()[y] == 0) {
                    a++;
                }
                if (m.getPaySheet()[i + 1].getWorkingHourInDay()[y] == 0) {
                    b++;
                }
            }
             if (a >= 2 && b >= 2) {
              r++ ;
              break;
             }
        }
        if (r !=0) {
                return true;
            } else {
                return false;
            }
    }

// to sorts unwarned Employees based on TotalPayment    (in all weeks) .
    public static void sortEmps(Object[] o) {
        int s = o.length;
        Employee e[] = new Employee[o.length];
        for (int x = 0; x < s; x++) {
            e[x] = (Employee) o[x];
        }
        for (int c = 0; c < e.length; c++) {
            for (int q = 0; q < s - 1 - c; q++) {
                if (payinweeks(e[q]) > payinweeks(e[q + 1])) {
                    Employee t = e[q + 1];
                    e[q + 1] = e[q];
                    e[q] = t;

                }
            }

        }

        for (int n = 0; n < e.length; n++) {
            if (iswarned(e[n]) == false) {
                System.out.println(e[n].toString());
            }
        }
    }

    public static void main(String[] args) {

        //arras of working Hour In Day for every employee 
        int arr1[] = {0, 4, 6, 0, 8};
        int arr2[] = {7, 2, 0, 0, 8};
        int arr3[] = {8, 8, 7, 4, 0};

       
        
        // PaySheet objects 
        PaySheet p1 = new PaySheet("7/7/2023", arr1);
        PaySheet p2 = new PaySheet("19/5/2025", arr2);
        PaySheet p3 = new PaySheet("28/9/2030", arr3);

        // PaySheet arrays (of objects )
        PaySheet prr1[] = {p1, p2, p3};
        PaySheet prr2[] = {p1, p3};
        PaySheet prr3[] = {p2, p3};
        PaySheet prr4[] = {p1, p2};

        // Employee objects
        Employee e1 = new Employee(1, "AA", 35, 2018, 50.0, prr1);
        Employee e2 = new Employee(2, "BB", 29, 2022, 40.0, prr2);
        Employee e3 = new Employee(3, "CC", 40, 2019, 60.0, prr3);
        Employee e4 = new Employee(4, "DD", 25, 2020, 35.0, prr4);

        // array of Employee objects 
        Employee err[] = {e1, e2, e3, e4};
        Object o[] = {e1, e2, e3, e4};

         printinfo(err);
         printWarnedEmployees(err);
        sortEmps(o);
        
    }
}
