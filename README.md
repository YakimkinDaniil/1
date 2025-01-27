2. Напишите программу, в которой из строки "I have 3 cats, 4 dogs, and 1 turtle" отбираются цифры. Из этих цифр формируется массив.
// Объект для получения строки с консоли
Scanner scan = new Scanner(System.in);
// Список для хранения цифр
List<Integer> arrayDigits = new ArrayList<>();
// Получение строки с консоли
String inputString = scan.nextLine();

// Проход по каждому символу строки
for (char c : inputString.toCharArray()) {
   // Проверяем, является ли символ цифрой
   if (Character.isDigit(c)) {
       // Преобразуем символ в число и добавляем в список
       arrayDigits.add(Character.getNumericValue(c));
   }
}
// Вывод результата
System.out.println("Найденные цифры: " + arrayDigits);

3. Разработайте программу, которая выводит в консоль все цифры, входящие в натуральное число n. К примеру, если дано число 2359, то в консоль выводятся отдельно числа 2, 3, 5, 9.
public class Main {
   public static void main(String[] args) {

       Scanner scanner = new Scanner(System.in);
       int userInt = scanner.nextInt();
       if (userInt <= 0) {
           System.out.println("Данное число ненатуральное!");
       } else {
           String stringNumber = Integer.toString(userInt);
           char[] sctringChar = stringNumber.toCharArray();
           System.out.println("Цифры в числе:");
           for (char digit : sctringChar) {
               System.out.println(digit);
           }
       }
   }
}

5. Напишите программную реализацию бинарного дерева поиска.
public class task5 {

    static class Node {
        int key;
        Node left, right;

        public Node (int item) {
            key = item;
            left = right = null;
        }
    }

    static class BinarySearchTree {
        Node root;

        // Конструктор
        BinarySearchTree() {
            root = null;
        }

        // Вставка нового ключа
        void insert(int key) {
            root = insertRec(root, key);
        }

        /* Функция для вставки нового узла с заданным
        ключом */
        Node insertRec(Node root, int key) {
            //Если дерево пусто, возвращаем новый узел
            if (root == null) {
                root = new Node(key);
                return root;
            }

            // Иначе, рекурсивно вызываем функцию вставки
            if (key < root.key)
                root.left = insertRec(root.left, key);
            else if (key > root.key)
                root.right = insertRec(root.right, key);

            // Возвращаем неизменный узел
            return root;
        }

        // Поиск ключа в BST
        boolean search(int key) {
            return searchRec(root, key);
        }

        /* Функция для поиска узла с заданным ключом */
        boolean searchRec(Node root, int key) {
            // Базовый случай: пустое дерево
            if (root == null)
                return false;

            // Если ключ совпадает с корневым
            if (root.key == key)
                return true;

            // Если ключ меньше корневого, рекурсивно ищем в левом поддереве
            if (key < root.key)
                return searchRec(root.left, key);

            // Если ключ больше корневого, рекурсивно ищем в правом поддереве
            return searchRec(root.right, key);
        }

        // Обход дерева в порядке inorder
        void inorder() {
            inorderRec(root);
        }

        /* Функция для выполнения обхода дерева inorder */
        void inorderRec(Node root) {
            if (root != null) {
                inorderRec(root.left);
                System.out.print(root.key + " ");
                inorderRec(root.right);
            }
        }

        // Обход дерева в порядке preorder
        void preorder() {
            preorderRec(root);
        }

        /* Функция для выполнения обхода дерева preorder */
        void preorderRec(Node root) {
            if (root != null) {
                System.out.print(root.key + " ");
                preorderRec(root.left);
                preorderRec(root.right);
            }
        }

        // Обход дерева в порядке postorder
        void postorder() {
            postorderRec(root);
        }

        /* Функция для выполнения обхода дерева postorder */
        void postorderRec(Node root) {
            if (root != null) {
                postorderRec(root.left);
                postorderRec(root.right);
                System.out.print(root.key + " ");
            }

        }
    }

    // Основная функция для тестирования
    public static void main (String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        /* Вставка узлов */
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        /* Поиск узлов */
        System.out.println("Поиск 60: " + tree.search(60));
        System.out.println("Поиск 90: " + tree.search(90));

        /* Обходы дерева */
        System.out.println("Обход inorder:");
        tree.inorder();
        System.out.println();

        System.out.println("Обход preorder:");
        tree.preorder();
        System.out.println();

        System.out.println("Обход postorder:");
        tree.postorder();
        System.out.println();
    }
}
6. Разработайте программу, которая выводит буквы английского алфавита, используя цикл while в MySQL/PostgreSQL.
ЭТО ЕСЛИ ОН РАЗРЕШИТ ДЕЛАТЬ БЕЗ ДЖАВЫ.

CREATE TABLE alphabet_table (
    letter CHAR(1)
);

DO $$ 
DECLARE
    alphabet_char CHAR(1);
    start INTEGER := 65; -- кодировка символа 'A'
BEGIN
    WHILE start <= 90 LOOP
        SELECT chr(start) INTO alphabet_char;
        INSERT INTO alphabet_table (letter) VALUES (alphabet_char);
        start := start + 1;
    END LOOP;
END $$;

SELECT * FROM alphabet_table;

НА ДЖАВЕ:
package org.example;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Main {
   public static void main(String[] args) {
       String url = "jdbc:postgresql://localhost:5432/postgres";
       String user = "postgres";
       String password = "postgres";
       String query = "SELECT CHR(x) AS letter FROM generate_series(65, 90) AS x";
      
       try (Connection connection = DriverManager.getConnection(url, user, password);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery(query)) {

           System.out.println("Алфавит:");
          
           while (resultSet.next()) {
               String letter = resultSet.getString("letter");
               System.out.print(letter + " ");
           }

       } catch (Exception e) {
           e.printStackTrace();
       }
   }
}

POM.XML:
    <dependencies>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.6.0</version> <!-- Замените на актуальную версию -->
        </dependency>
    </dependencies>

7. Напишите программу, которая будет выводить в консоль введённое слово 6 раз и сохранять в MySQL/PostgreSQL.
сначала создаём бд postgres
CREATE DATABASE word_db;
\c word_db;

CREATE TABLE words (
    id SERIAL PRIMARY KEY,
    word VARCHAR(255) NOT NULL
);
Далее настраиваем pom.xml:
<dependencies>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <version>42.2.23</version>
    </dependency>
</dependencies>
код:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class WordSaver {
     private static final String DB_URL = "jdbc:postgresql://localhost:5432/word_db";
    private static final String DB_USER = "postgres"; 
    private static final String DB_PASSWORD = "postgres"; 

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Введите слово: ");
        String word = scanner.nextLine();

        for (int i = 0; i < 6; i++) {
            System.out.println(word);
        }

        saveWordToDatabase(word);
    }

    private static void saveWordToDatabase(String word) {
        String insertSQL = "INSERT INTO words (word) VALUES (?)";

        try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
             PreparedStatement preparedStatement = connection.prepareStatement(insertSQL)) {

            preparedStatement.setString(1, word);
            preparedStatement.executeUpdate();

            System.out.println("Слово успешно сохранено в базу данных.");

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}


8. Разработать программу для вывода на экран кубов первых десяти положительных чисел.
public class Cubes {
   public static void main(String[] args) {
       System.out.println("Кубы первых десяти положительных чисел:");
       for (int i = 1; i <= 10; i++) {
           int cube = i * i * i;
           System.out.println("Куб числа " + i + " равен " + cube);
       }
   }
}

9. Напишите программу, которая по дате определяет день недели, на который эта дата приходится.
https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/DayOfWeek.html 
https://metanit.com/java/tutorial/12.3.php 

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.DayOfWeek;
import java.util.Scanner;

public class DayOfWeekCalculator {
   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);

       System.out.print("Введите дату в формате ГГГГ-ММ-ДД: ");
       String inputDate = scanner.nextLine();
       //форматирование даты
       DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");

       try {
           LocalDate date = LocalDate.parse(inputDate, formatter);

           //получаем день недели
           DayOfWeek dayOfWeek = date.getDayOfWeek();


           System.out.println("День недели для даты " + inputDate + ": " + dayOfWeek);
       } catch (Exception e) {
           System.out.println("Ошибка: неверный формат даты. Пожалуйста, используйте ГГГГ-ММ-ДД.");
       } finally {
           scanner.close();
       }
   }
}

10. Написать класс, который при введении даты в формате ДД.ММ.ГГ (к примеру, 22.10.20) выводит номер недели. Даты начиная с 2020 по 2022 годы. К примеру, первая неделя в 2020 году: 1-5 января, вторая неделя – 6-12 января. Значит при вводе 08.01.20 вывод должен быть: Неделя 2.

11. Разработайте программу, реализующую рекурсивное вычисление факториала.

public class Factorial {

    // Метод для рекурсивного вычисления факториала
    public static int factorial(int n) {
        // Базовый случай: факториал 0 и 1 равен 1
        if (n == 0 || n == 1) {
            return 1;
        }
        // Рекурсивный случай: n * факториал (n-1)
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        // Пример использования метода factorial
        int number = 10;
        int result = factorial(number);
        System.out.println("Факториал числа " + number + " равен " + result);
    }
}

12. Разработать класс-оболочку для числового типа double. Реализовать статические методы сложения, деления, возведения в степень.
public class DoubleWrapper {

   private double value;

   public DoubleWrapper(double value) {
       this.value = value;
   }

   public double getValue() {
       return value;
   }

   public void setValue(double value) {
       this.value = value;
   }

   public static double add(double a, double b) {
       return a + b;
   }

   public static double divide(double a, double b) throws ArithmeticException {
       if (b == 0) {
           throw new ArithmeticException("Делитель не может быть равен нулю");
       }
       return a / b;
   }

   public static double power(double base, double exponent) {
       return Math.pow(base, exponent);
   }

   public static void main(String[] args) {
       DoubleWrapper dw1 = new DoubleWrapper(5.0);
       DoubleWrapper dw2 = new DoubleWrapper(3.0);

       System.out.println("Сложение: " + DoubleWrapper.add(dw1.getValue(), dw2.getValue()));
       System.out.println("Деление: " + DoubleWrapper.divide(dw1.getValue(), dw2.getValue()));
       System.out.println("Возведение в степень: " + DoubleWrapper.power(dw1.getValue(), dw2.getValue()));
   }
}


13. Разработать программу, которая заполняет двумерный массив случайными положительными числами в диапазоне от 1 до 100 до тех пор, пока сумма граничных элементов не станет равной 666. Пользователь вначале вводит размер матрицы.
// Объект для получения строки с консоли
Scanner scan = new Scanner(System.in);
Random random = new Random();

// Получаем параметры размерности матрицы
System.out.println("Введите количество строк: ");
int rows = Integer.parseInt(scan.nextLine());
System.out.println("Введите количество столбцов: ");
int cols = Integer.parseInt(scan.nextLine());

// создаем пустую матрицу и переменную для сохранения суммы граничных элементов
int[][] matrix = new int[rows][cols];
int sum = 0;

// Повторяем, пока сумма граничных элементов не станет равной 666
do {
   sum = 0;

   // Заполняем матрицу случайными числами
   for (int i = 0; i < rows; i++) {
       for (int j = 0; j < cols; j++) {
           matrix[i][j] = random.nextInt(100) + 1;
       }
   }
   // Вычисляем сумму граничных элементов
   for (int i = 0; i < rows; i++) {
       for (int j = 0; j < cols; j++) {
           // Верхняя и нижняя границы
           if (i == 0 || i == rows - 1) {
               sum += matrix[i][j];
           }
           // Левые и правые границы (кроме уже учтенных углов)
           else if (j == 0 || j == cols - 1) {
               sum += matrix[i][j];
           }
       }
   }
} while (sum != 666);

// Выводим результат
System.out.println("Матрица с суммой граничных элементов 666:");
for (int i = 0; i < rows; i++) {
   for (int j = 0; j < cols; j++) {
       System.out.print(matrix[i][j] + "\t");
   }
   System.out.println();
}
System.out.println("Сумма граничных элементов: " + sum);

14. Разработать программу, в которой требуется создать класс, описывающий геометрическую фигуру – треугольник. Методами класса должны быть – вычисление площади, периметра. Создать класс-наследник, определяющий прямоугольный треугольник.
public class Triangle {

   int firstSide;
   int secondSide;
   int thirdSide;
   int sumSide;

   public Triangle(){}
   public Triangle(int firstSide, int secondSide, int thirdSide) {
       this.firstSide = firstSide;
       this.secondSide = secondSide;
       this.thirdSide = thirdSide;
   }

   public int P(){
       return firstSide +secondSide + thirdSide;
   }

   public double S(){
       int p = P()/2;
       return Math.sqrt(p*(p-firstSide)*(p-secondSide)*(p-thirdSide));
   }
}

import java.awt.*;
import java.util.ArrayList;

public class TriS extends Triangle{

   private double base;
   private double height;

   public TriS(int firstSide, int secondSide, int thirdSide, double base, double height) {
       super(firstSide, secondSide, thirdSide);
       this.base = base;
       this.height = height;
   }

   @Override
   public double S(){
       return (base * height) / 2;
   }

}

public class Main {

   public static void main(String[] args) {

      Triangle tri = new Triangle(3,4,5);
       System.out.println(tri.P());
      System.out.println(tri.S());

      TriS triS = new TriS(10,10,10,10, 20);
       System.out.println( triS.S());
      System.out.println(triS.P());

}
}

15. Разработать программу, в которой требуется создать абстрактный класс. В этом абстрактном классе определить абстрактные методы вычисления функции в определенной точке. Создать классы-наследники абстрактного класса, описывающими уравнения прямой и параболы. Программа должна выводить в консоль значение функции при вводе определенного значения.
Структура следующая:
 
 
1. Function - это главный абстрактный класс, в котором мы определяем абстрактный метод вычисления функции в точке x
 

2. LinearFunction - это дочерний класс. Он наследует метод класса Function.
 

3. QuadraticFunction - это дочерний класс. Он наследует метод класса Function.
 

4. test - здесь запускаем программу
 

19. Создать класс Matrix для работы с двумерными матрицами. Создать методы для генерации нулевой матрицы, а также для генерации матрицы со случайными величинами – применить Math.random(). Реализовать метод сложения матриц.
package org.example;

import java.util.Random;

public class Matrix {
    private int rows;
    private int cols;
    private int[][] matrix;

    public Matrix(int rows, int cols) {
        this.rows = rows;
        this.cols = cols;
        this.matrix = new int[rows][cols];
    }

    public void generateZeroMatrix() {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                matrix[i][j] = 0;
            }
        }
    }

    public void generateRandomMatrix() {
        Random random = new Random();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                matrix[i][j] = random.nextInt(100);
            }
        }
    }

    public Matrix add(Matrix other) {
        if (this.rows != other.rows || this.cols != other.cols) {
            throw new IllegalArgumentException("Размеры матриц должны совпадать.");
        }

        Matrix result = new Matrix(this.rows, this.cols);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.matrix[i][j] = this.matrix[i][j] + other.matrix[i][j];
            }
        }
        return result;
    }

    public void displayMatrix() {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                System.out.print(matrix[i][j] + "\t");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Matrix mat0 = new Matrix(5, 5);
        mat0.generateZeroMatrix();
        System.out.println("Нулевая матрица");
        mat0.displayMatrix();

        Matrix mat1 = new Matrix(3, 3);
        mat1.generateRandomMatrix();

        Matrix mat2 = new Matrix(3, 3);
        mat2.generateRandomMatrix();

        System.out.println("\nМатрица 1:");
        mat1.displayMatrix();

        System.out.println("\nМатрица 2:");
        mat2.displayMatrix();

        Matrix sumMatrix = mat1.add(mat2);
        System.out.println("\nСумма Матриц:");
        sumMatrix.displayMatrix();
    }
}
20. Реализовать класс MyMath для работы с числами. Реализовать статический метод класса MyMath.round(), который округляет дробь до целого числа. Также статический метод abs(), который находит модуль числа. Статический метод MyMath.pow() для нахождения степени числа. Библиотеку Math не использовать.
public class MyMath {

   // Метод для округления дроби до целого числа
   public static int round(double number) {
       int intPart = (int) number;
       double fractionPart = number - intPart;

       if (fractionPart > 0.5) {
           return intPart + 1;
       } else if (fractionPart < -0.5) {
           return intPart - 1;
       } else {
           return intPart;
       }
   }

   // Метод для нахождения модуля числа
   public static int abs(int number) {
       return number < 0 ? -number : number;
   }

   // Метод для нахождения степени числа
   public static double pow(double base, int exponent) {
       double result = 1;
       boolean isNegative = exponent < 0;
       int absExponent = isNegative ? -exponent : exponent;

       for (int i = 0; i < absExponent; i++) {
           result *= base;
       }

       return isNegative ? 1 / result : result;
   }

   public static void main(String[] args) {
       // Примеры использования методов
       System.out.println("Round(2.3): " + MyMath.round(2.3)); // 2
       System.out.println("Round(2.7): " + MyMath.round(2.7)); // 3
       System.out.println("Round(-2.3): " + MyMath.round(-2.3)); // -2
       System.out.println("Round(-2.7): " + MyMath.round(-2.7)); // -3

       System.out.println("Abs(-5): " + MyMath.abs(-5)); // 5
       System.out.println("Abs(5): " + MyMath.abs(5)); // 5

       System.out.println("Pow(2, 3): " + MyMath.pow(2, 3)); // 8
       System.out.println("Pow(2, -3): " + MyMath.pow(2, -3)); // 0.125
   }
}

23. Разработать класс для представления комплексных чисел с возможностью задания вещественной и мнимой частей в виде массива из двух чисел типа int. Определить методы для выполнения операций сложения, вычитания и умножения комплексных чисел.
public class ComplexNumber {
   private int[] parts; // Массив для хранения вещественной и мнимой частей

   // Конструктор
   public ComplexNumber(int real, int imaginary) {
       parts = new int[2];
       parts[0] = real; // Вещественная часть
       parts[1] = imaginary; // Мнимая часть
   }

   public int getReal() {
       return parts[0];
   }

   public int getImaginary() {
       return parts[1];
   }

   // Метод для сложения комплексных чисел
   public ComplexNumber add(ComplexNumber other) {
       int realPart = this.getReal() + other.getReal();
       int imaginaryPart = this.getImaginary() + other.getImaginary();
       return new ComplexNumber(realPart, imaginaryPart);
   }

   // Метод для вычитания комплексных чисел
   public ComplexNumber subtract(ComplexNumber other) {
       int realPart = this.getReal() - other.getReal();
       int imaginaryPart = this.getImaginary() - other.getImaginary();
       return new ComplexNumber(realPart, imaginaryPart);
   }

   // Метод для умножения комплексных чисел
   public ComplexNumber multiply(ComplexNumber other) {
       int realPart = this.getReal() * other.getReal() - this.getImaginary() * other.getImaginary();
       int imaginaryPart = this.getReal() * other.getImaginary() + this.getImaginary() * other.getReal();
       return new ComplexNumber(realPart, imaginaryPart);
   }

   // Переопределение метода toString для удобного вывода
   @Override
   public String toString() {
       return parts[0] + " + " + parts[1] + "i";
   }

   // Пример использования класса
   public static void main(String[] args) {
       ComplexNumber num1 = new ComplexNumber(3, 2); // 3 + 2i
       ComplexNumber num2 = new ComplexNumber(1, 7); // 1 + 7i

       ComplexNumber sum = num1.add(num2);
       ComplexNumber difference = num1.subtract(num2);
       ComplexNumber product = num1.multiply(num2);

       System.out.println("Сумма: " + sum);
       System.out.println("Разность: " + difference);
       System.out.println("Произведение: " + product);
   }
}

25. Сделайте класс User, в котором будут следующие protected поля - name (имя), age (возраст), public методы setName, getName, setAge, getAge. Сделайте класс Worker, который наследует от класса User и вносит дополнительное private поле salary (зарплата), а также методы public getSalary и setSalary. Создайте объект этого класса 'Иван', возраст 25, зарплата 1000. Создайте второй объект этого класса 'Вася', возраст 26, зарплата 2000. Найдите сумму зарплата Ивана и Васи. Сделайте класс Student, который наследует от класса User и вносит дополнительные private поля стипендия, курс, а также геттеры и сеттеры для них.


class User {
   protected String name;
   protected int age;

   //сеттеры и геттеры
   public void setName(String name) {
       this.name = name;
   }

   public String getName() {
       return name;
   }

   public void setAge(int age) {
       this.age = age;
   }

   public int getAge() {
       return age;
   }
}

//класс Worker, наследующий от User
class Worker extends User {
   private double salary;

   //сеттеры и геттеры
   public void setSalary(double salary) {
       this.salary = salary;
   }
   public double getSalary() {
       return salary;
   }
}

//класс Student, наследующий от User
class Student extends User {
   private double scholarship;
   private int course;

   public void setScholarship(double scholarship) {
       this.scholarship = scholarship;
   }

   public double getScholarship() {
       return scholarship;
   }

   public void setCourse(int course) {
       this.course = course;
   }
   public int getCourse() {
       return course;
   }
}


public class Main {
   public static void main(String[] args) {
       Worker ivan = new Worker();
       ivan.setName("Иван");
       ivan.setAge(25);
       ivan.setSalary(1000);

       Worker vasya = new Worker();
       vasya.setName("Вася");
       vasya.setAge(26);
       vasya.setSalary(2000);

       //сумма зарплат Ивана и Васи
       double totalSalary = ivan.getSalary() + vasya.getSalary();

       System.out.println("Сумма зарплат Ивана и Васи: " + totalSalary);

       Student student = new Student();
       student.setName("Алексей");
       student.setAge(20);
       student.setScholarship(500);
       student.setCourse(2);

       System.out.println("Студент: " + student.getName() + ", возраст: " + student.getAge() +
               ", стипендия: " + student.getScholarship() + ", курс: " + student.getCourse());
   }
}


27. Создайте класс Number для конвертации десятичного числа в бинарный, восьмеричный, шестнадцатеричный вид. Реализовать в виде статических методов класса. Числа вводятся с клавиатуры с запросом в какой численный вид конвертировать.
29. Напишите программу, которая заполняет списочный массив случайными числами типа Integer (значения этих чисел были от 1 до 100). Список должен содержать 100 элементов. Затем отсортируйте по убыванию список и выведите первые 10 значений в консоль. Результаты сохраните в MySQL/PostgreSQL.

CREATE DATABASE number;
\c number;

CREATE TABLE random_numbers (
    id SERIAL PRIMARY KEY,
    value INT NOT NULL
);



import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Random;

public class RandomNumberSorter {

    // Метод для заполнения списка случайными числами
    public static List<Integer> generateRandomNumbers(int size, int min, int max) {
        List<Integer> numbers = new ArrayList<>();
        Random random = new Random();
        for (int i = 0; i < size; i++) {
            numbers.add(random.nextInt((max - min) + 1) + min);
        }
        return numbers;
    }

    // Метод для сохранения результатов в базе данных
    public static void saveToDatabase(List<Integer> numbers) {
        String url = "jdbc:postgresql://localhost:5432/number";
        String user = "postgres";
        String password = "postgres";

        String sql = "INSERT INTO random_numbers (value) VALUES (?)";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            for (int number : numbers) {
                pstmt.setInt(1, number);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        // Генерация списка случайных чисел
        List<Integer> numbers = generateRandomNumbers(100, 1, 100);

        // Сортировка списка по убыванию
        Collections.sort(numbers, Collections.reverseOrder());

        // Вывод первых 10 значений в консоль
        System.out.println("Первые 10 значений отсортированного списка:");
        for (int i = 0; i < 10; i++) {
            System.out.println(numbers.get(i));
        }

        // Сохранение результатов в базе данных
        saveToDatabase(numbers);
    }
}

30. Разработайте программу, которая заполняет список случайными числами. Количество элементов и числовой диапазон вводятся пользователем. Программа должна проверять, входит ли число (также вводится пользователем) в данный список. Должен быть реализован бинарный поиск. Результаты должны сохраняться в MySQL/PostgreSQL и выводиться оттуда же.
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Random;
import java.util.Scanner;

public class RandomNumberSearch {

   private static final String DB_URL = "jdbc:postgresql://localhost:5432/randomnumbersdb";
   private static final String DB_USER = "postgres";
   private static final String DB_PASSWORD = "your_password";

   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);

       System.out.print("Введите количество элементов: ");
       int numElements = scanner.nextInt();

       System.out.print("Введите минимальное значение диапазона: ");
       int minRange = scanner.nextInt();

       System.out.print("Введите максимальное значение диапазона: ");
       int maxRange = scanner.nextInt();

       List<Integer> randomNumbers = generateRandomNumbers(numElements, minRange, maxRange);
       Collections.sort(randomNumbers);

       System.out.print("Введите число для поиска: ");
       int searchNumber = scanner.nextInt();

       boolean found = binarySearch(randomNumbers, searchNumber);
       saveResultToDatabase(searchNumber, found);

       System.out.println("Результаты поиска:");
       printResultsFromDatabase();

       scanner.close();
   }

   private static List<Integer> generateRandomNumbers(int numElements, int minRange, int maxRange) {
       List<Integer> randomNumbers = new ArrayList<>();
       Random random = new Random();
       for (int i = 0; i < numElements; i++) {
           randomNumbers.add(random.nextInt((maxRange - minRange) + 1) + minRange);
       }
       return randomNumbers;
   }

   private static boolean binarySearch(List<Integer> list, int target) {
       int left = 0;
       int right = list.size() - 1;
       while (left <= right) {
           int mid = left + (right - left) / 2;
           if (list.get(mid) == target) {
               return true;
           }
           if (list.get(mid) < target) {
               left = mid + 1;
           } else {
               right = mid - 1;
           }
       }
       return false;
   }

   private static void saveResultToDatabase(int number, boolean found) {
       String insertSQL = "INSERT INTO SearchResults (number, found) VALUES (?, ?)";
       try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            PreparedStatement pstmt = conn.prepareStatement(insertSQL)) {
           pstmt.setInt(1, number);
           pstmt.setBoolean(2, found);
           pstmt.executeUpdate();
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   private static void printResultsFromDatabase() {
       String selectSQL = "SELECT number, found FROM SearchResults";
       try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(selectSQL)) {
           while (rs.next()) {
               int number = rs.getInt("number");
               boolean found = rs.getBoolean("found");
               System.out.println("Число: " + number + ", Найдено: " + found);
           }
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }
}

Создание бд и таблицы:
CREATE DATABASE RandomNumbersDB;
CREATE TABLE SearchResults (
    id SERIAL PRIMARY KEY,
    number INT,
    found BOOLEAN
);



31. На основе класса BitSet разработайте программу для реализации битовых операций AND, OR, XOR, а также маскирования.

import java.util.BitSet;

public class BitSetOperations {

    public static void main(String[] args) {
        // Создание и инициализация BitSet
        BitSet bitSet1 = new BitSet();
        bitSet1.set(0);
        bitSet1.set(1);
        bitSet1.set(2);
        bitSet1.set(3);

        BitSet bitSet2 = new BitSet();
        bitSet2.set(0);
        bitSet2.set(1);
        bitSet2.set(2);
        bitSet2.set(3);

        // Выполнение битовых операций
        BitSet andResult = (BitSet) bitSet1.clone();
        andResult.and(bitSet2);
        System.out.println("AND: " + andResult);

        BitSet orResult = (BitSet) bitSet1.clone();
        orResult.or(bitSet2);
        System.out.println("OR: " + orResult);

        BitSet xorResult = (BitSet) bitSet1.clone();
        xorResult.xor(bitSet2);
        System.out.println("XOR: " + xorResult);

        // Маскирование битов
        BitSet mask = new BitSet();
        mask.set(0);
        mask.set(1);
        mask.set(2);
        mask.set(3);

        BitSet maskedResult = (BitSet) bitSet1.clone();
        maskedResult.and(mask);
        System.out.println("Masked: " + maskedResult);
    }
}

32. Напишите программу, которая получает в качестве входных данных два числа. Эти числа являются количество строк и столбцов двумерной коллекции целых чисел. Далее элементы заполняются случайными числами и выводятся в консоль в виде таблицы.
import java.util.Random;
import java.util.Scanner;

public class RandomMatrix {
   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);
       Random random = new Random();

       // Получаем количество строк и столбцов от пользователя
       System.out.print("Введите количество строк: ");
       int rows = scanner.nextInt();
       System.out.print("Введите количество столбцов: ");
       int cols = scanner.nextInt();

       // Создаем двумерный массив
       int[][] matrix = new int[rows][cols];

       // Заполняем массив случайными числами
       for (int i = 0; i < rows; i++) {
           for (int j = 0; j < cols; j++) {
               matrix[i][j] = random.nextInt(100); // Случайные числа от 0 до 99
           }
       }

       // Выводим массив в виде таблицы
       for (int i = 0; i < rows; i++) {
           for (int j = 0; j < cols; j++) {
               System.out.print(matrix[i][j] + "\t");
           }
           System.out.println();
       }

       scanner.close();
   }
}

33. Разработайте программу, которая получает в качестве параметра два числа – количество строк и столбцов двумерной коллекции целых чисел. Коллекция заполняется случайными числами, после чего на экран выводятся максимальное и минимальное значения с индексами ячеек.
import java.util.Random;
import java.util.Scanner;

public class TwoDimensionalArray {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Получение количества строк и столбцов от пользователя
        System.out.print("Введите количество строк: ");
        int rows = scanner.nextInt();
        System.out.print("Введите количество столбцов: ");
        int cols = scanner.nextInt();

        // Создание и заполнение двумерного массива случайными числами
        int[][] array = new int[rows][cols];
        Random random = new Random();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                array[i][j] = random.nextInt(100);
            }
        }

        // Поиск максимального и минимального значений и их индексов
        int maxValue = Integer.MIN_VALUE;
        int minValue = Integer.MAX_VALUE;
        int maxRow = -1, maxCol = -1;
        int minRow = -1, minCol = -1;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (array[i][j] > maxValue) {
                    maxValue = array[i][j];
                    maxRow = i;
                    maxCol = j;
                }
                if (array[i][j] < minValue) {
                    minValue = array[i][j];
                    minRow = i;
                    minCol = j;
                }
            }
        }

        // Вывод результатов
        System.out.println("Максимальное значение: " + maxValue + " (строка: " + maxRow + ", столбец: " + maxCol + ")");
        System.out.println("Минимальное значение: " + minValue + " (строка: " + minRow + ", столбец: " + minCol + ")");
    }
}

34. Разработайте программу, в которой создайте две коллекции с именами людей (строковые переменные). Результат сохранить в MySQL/PostgreSQL. Затем последовательно выводите в консоль имена.
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class SaveNamesToPostgreSQL {
   // JDBC URL, username and password of MySQL server
   private static final String URL = "jdbc:postgresql://localhost:5432/yourdatabase";
   private static final String USER = "postgres";
   private static final String PASSWORD = "postgres";

   public static void main(String[] args) {
       // Создаем две коллекции с именами людей
       List<String> namesList1 = new ArrayList<>();
       namesList1.add("Alice");
       namesList1.add("Bob");
       namesList1.add("Charlie");

       List<String> namesList2 = new ArrayList<>();
       namesList2.add("David");
       namesList2.add("Eve");
       namesList2.add("Frank");

       // Сохраняем имена в базу данных
       saveNamesToDatabase(namesList1);
       saveNamesToDatabase(namesList2);

       // Выводим имена в консоль
       printNamesFromDatabase();
   }

   private static void saveNamesToDatabase(List<String> names) {
       String sql = "INSERT INTO people (name) VALUES (?)";

       try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
            PreparedStatement pstmt = conn.prepareStatement(sql)) {

           for (String name : names) {
               pstmt.setString(1, name);
               pstmt.addBatch();
           }
           pstmt.executeBatch();

       } catch (SQLException e) {
           System.out.println(e.getMessage());
       }
   }

   private static void printNamesFromDatabase() {
       String sql = "SELECT name FROM people";

       try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(sql)) {

           while (rs.next()) {
               System.out.println(rs.getString("name"));
           }

       } catch (SQLException e) {
           System.out.println(e.getMessage());
       }
   }
}

35. Напишите программу, которая реализует класс Matrix и следующие методы:
a. Сложение и вычитание матриц.
b. Умножение матрицы на число.
c. Произведение двух матриц.
d. Транспонированная матрица.
e. Возведение матрицы в степень.
f. Если метод, возвращает матрицу, то он должен возвращать новый объект, а не менять базовый.

public class Matrix {
    private int[][] data;

    // Конструктор для создания матрицы
    public Matrix(int[][] data) {
        this.data = data;
    }

    // Метод для получения размеров матрицы
    public int getRows() {
        return data.length;
    }

    public int getCols() {
        return data[0].length;
    }

    // Метод для сложения двух матриц
    public Matrix add(Matrix other) {
        int rows = getRows();
        int cols = getCols();
        int[][] result = new int[rows][cols];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[i][j] = data[i][j] + other.data[i][j];
            }
        }
        return new Matrix(result);
    }

    // Метод для вычитания двух матриц
    public Matrix subtract(Matrix other) {
        int rows = getRows();
        int cols = getCols();
        int[][] result = new int[rows][cols];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[i][j] = data[i][j] - other.data[i][j];
            }
        }
        return new Matrix(result);
    }

    // Метод для умножения матрицы на число
    public Matrix multiply(int scalar) {
        int rows = getRows();
        int cols = getCols();
        int[][] result = new int[rows][cols];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[i][j] = data[i][j] * scalar;
            }
        }
        return new Matrix(result);
    }

    // Метод для произведения двух матриц
    public Matrix multiply(Matrix other) {
        int rows = getRows();
        int cols = other.getCols();
        int common = getCols();
        int[][] result = new int[rows][cols];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                for (int k = 0; k < common; k++) {
                    result[i][j] += data[i][k] * other.data[k][j];
                }
            }
        }
        return new Matrix(result);
    }

    // Метод для транспонирования матрицы
    public Matrix transpose() {
        int rows = getRows();
        int cols = getCols();
        int[][] result = new int[cols][rows];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result[j][i] = data[i][j];
            }
        }
        return new Matrix(result);
    }

    // Метод для возведения матрицы в степень
    public Matrix power(int exponent) {
        Matrix result = this;
        Matrix base = this;
        for (int i = 1; i < exponent; i++) {
            result = result.multiply(base);
        }
        return result;
    }

    // Метод для вывода матрицы
    public void print() {
        int rows = getRows();
        int cols = getCols();
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                System.out.print(data[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int[][] data1 = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        int[][] data2 = {
            {9, 8, 7},
            {6, 5, 4},
            {3, 2, 1}
        };

        Matrix matrix1 = new Matrix(data1);
        Matrix matrix2 = new Matrix(data2);

        System.out.println("Matrix 1:");
        matrix1.print();

        System.out.println("Matrix 2:");
        matrix2.print();

        System.out.println("Matrix 1 + Matrix 2:");
        matrix1.add(matrix2).print();

        System.out.println("Matrix 1 - Matrix 2:");
        matrix1.subtract(matrix2).print();

        System.out.println("Matrix 1 * 2:");
        matrix1.multiply(2).print();

        System.out.println("Matrix 1 * Matrix 2:");
        matrix1.multiply(matrix2).print();

        System.out.println("Transpose of Matrix 1:");
        matrix1.transpose().print();

        System.out.println("Matrix 1 ^ 2:");
        matrix1.power(2).print();
    }
}
37. Написать приложение для сложения, вычитания, умножения, деления, возведения в степень логарифмов. Программа должна выполнять ввод данных, проверку правильности введенных данных, выдачу сообщений в случае ошибок. Результат выводится на экран и записывается в файл.
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Scanner;

public class Calculator {
   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);
       String fileName = "results.txt";

       try (PrintWriter writer = new PrintWriter(new FileWriter(fileName, true))) {
           while (true) {
               System.out.println("Выберите операцию:");
               System.out.println("1. Сложение");
               System.out.println("2. Вычитание");
               System.out.println("3. Умножение");
               System.out.println("4. Деление");
               System.out.println("5. Возведение в степень");
               System.out.println("6. Логарифм");
               System.out.println("7. Выход");

               int choice = scanner.nextInt();

               if (choice == 7) {
                   break;
               }

               double result = 0;
               String operation = "";

               switch (choice) {
                   case 1:
                       result = add(scanner);
                       operation = "Сложение";
                       break;
                   case 2:
                       result = subtract(scanner);
                       operation = "Вычитание";
                       break;
                   case 3:
                       result = multiply(scanner);
                       operation = "Умножение";
                       break;
                   case 4:
                       result = divide(scanner);
                       operation = "Деление";
                       break;
                   case 5:
                       result = power(scanner);
                       operation = "Возведение в степень";
                       break;
                   case 6:
                       result = logarithm(scanner);
                       operation = "Логарифм";
                       break;
                   default:
                       System.out.println("Неверный выбор. Пожалуйста, попробуйте снова.");
                       continue;
               }

               System.out.println("Результат: " + result);
               writer.println(operation + ": " + result);
           }
       } catch (IOException e) {
           System.out.println("Ошибка записи в файл: " + e.getMessage());
       }

       scanner.close();
   }

   private static double add(Scanner scanner) {
       System.out.print("Введите первое число: ");
       double a = scanner.nextDouble();
       System.out.print("Введите второе число: ");
       double b = scanner.nextDouble();
       return a + b;
   }

   private static double subtract(Scanner scanner) {
       System.out.print("Введите первое число: ");
       double a = scanner.nextDouble();
       System.out.print("Введите второе число: ");
       double b = scanner.nextDouble();
       return a - b;
   }

   private static double multiply(Scanner scanner) {
       System.out.print("Введите первое число: ");
       double a = scanner.nextDouble();
       System.out.print("Введите второе число: ");
       double b = scanner.nextDouble();
       return a * b;
   }

   private static double divide(Scanner scanner) {
       System.out.print("Введите первое число: ");
       double a = scanner.nextDouble();
       System.out.print("Введите второе число: ");
       double b = scanner.nextDouble();
       if (b == 0) {
           System.out.println("Ошибка: деление на ноль.");
           return 0;
       }
       return a / b;
   }

   private static double power(Scanner scanner) {
       System.out.print("Введите основание: ");
       double base = scanner.nextDouble();
       System.out.print("Введите показатель: ");
       double exponent = scanner.nextDouble();
       return Math.pow(base, exponent);
   }

   private static double logarithm(Scanner scanner) {
       System.out.print("Введите число: ");
       double number = scanner.nextDouble();
       if (number <= 0) {
           System.out.println("Ошибка: логарифм от неположительного числа не определен.");
           return 0;
       }
       return Math.log(number);
   }
}

38. Разработать программу шифровки-дешифровки по алгоритму AES-128. Данные берутся из файла, зашифрованные данные сохраняются в указанный файл.
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.security.NoSuchAlgorithmException;
import java.util.Base64;

public class AES128Encryption {

    // Метод для генерации ключа AES-128
    public static SecretKey generateKey() throws NoSuchAlgorithmException {
        KeyGenerator keyGen = KeyGenerator.getInstance("AES");
        keyGen.init(128);
        return keyGen.generateKey();
    }

    // Метод для шифрования данных
    public static byte[] encrypt(byte[] data, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.ENCRYPT_MODE, key);
        return cipher.doFinal(data);
    }

    // Метод для дешифрования данных
    public static byte[] decrypt(byte[] data, SecretKey key) throws Exception {
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.DECRYPT_MODE, key);
        return cipher.doFinal(data);
    }

    // Метод для чтения данных из файла
    public static byte[] readFile(String filePath) throws IOException {
        return Files.readAllBytes(Paths.get(filePath));
    }

    // Метод для записи данных в файл
    public static void writeFile(String filePath, byte[] data) throws IOException {
        Files.write(Paths.get(filePath), data);
    }

    public static void main(String[] args) {
        try {
            // Генерация ключа
            SecretKey key = generateKey();

            // Чтение данных из файла
            String inputFilePath = "input.txt";
            byte[] inputData = readFile(inputFilePath);

            // Шифрование данных
            byte[] encryptedData = encrypt(inputData, key);

            // Сохранение зашифрованных данных в файл
            String encryptedFilePath = "encrypted.txt";
            writeFile(encryptedFilePath, encryptedData);

            // Дешифрование данных
            byte[] decryptedData = decrypt(encryptedData, key);

            // Сохранение дешифрованных данных в файл
            String decryptedFilePath = "decrypted.txt";
            writeFile(decryptedFilePath, decryptedData);

            System.out.println("Шифрование и дешифрование завершены успешно.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

39. Разработать программу нахождения наибольшего общего делителя двух натуральных чисел. Требуется реализовать рекурсивный и без рекурсии варианты. Результат сохранить в MySQL/PostgreSQL.

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class GCDCalculator {
   // JDBC URL, username and password of PostgreSQL server
   private static final String URL = "jdbc:postgresql://localhost:5432/yourdatabase";
   private static final String USER = "postgres";
   private static final String PASSWORD = "postgres";

   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);

       System.out.print("Введите первое натуральное число: ");
       int a = scanner.nextInt();
       System.out.print("Введите второе натуральное число: ");
       int b = scanner.nextInt();

       int gcdRecursive = gcdRecursive(a, b);
       int gcdIterative = gcdIterative(a, b);

       System.out.println("НОД (рекурсивный метод): " + gcdRecursive);
       System.out.println("НОД (итеративный метод): " + gcdIterative);

       saveResultToDatabase(a, b, gcdRecursive, gcdIterative);

       scanner.close();
   }

   // Рекурсивный метод для нахождения НОД
   private static int gcdRecursive(int a, int b) {
       if (b == 0) {
           return a;
       }
       return gcdRecursive(b, a % b);
   }

   // Итеративный метод для нахождения НОД
   private static int gcdIterative(int a, int b) {
       while (b != 0) {
           int temp = b;
           b = a % b;
           a = temp;
       }
       return a;
   }

   // Метод для сохранения результатов в базу данных
   private static void saveResultToDatabase(int a, int b, int gcdRecursive, int gcdIterative) {
       String sql = "INSERT INTO gcd_results (a, b, gcd_recursive, gcd_iterative) VALUES (?, ?, ?, ?)";

       try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
            PreparedStatement pstmt = conn.prepareStatement(sql)) {

           pstmt.setInt(1, a);
           pstmt.setInt(2, b);
           pstmt.setInt(3, gcdRecursive);
           pstmt.setInt(4, gcdIterative);
           pstmt.executeUpdate();

       } catch (SQLException e) {
           System.out.println(e.getMessage());
       }
   }
}

CREATE TABLE gcd_results (
    id SERIAL PRIMARY KEY,
    a INT NOT NULL,
    b INT NOT NULL,
    gcd_recursive INT NOT NULL,
    gcd_iterative INT NOT NULL
);


Сложные: 
1. Условие: «Реализовать программу для выполнения следующих математических операций с целочисленным, байтовым и вещественным типами данных: сложение, вычитание, умножение, деление, деление по модулю (остаток), модуль числа, возведение в степень. Все данные вводятся с клавиатуры (класс Scanner, System.in, nextint).» По данному условию необходимо реализовать программу с интерактивным консольным меню, (т.е. вывод списка действий по цифрам. При этом при нажатии на цифру у нас должно выполняться определенное действие). При этом в программе данные пункты должны называться следующим образом:
1. Вывести все таблицы из MySQL.
2. Создать таблицу в MySQL.
3. Сложение чисел, результат сохранить в MySQL с последующим выводом в консоль.
4. Вычитание чисел, результат сохранить в MySQL с последующим выводом в консоль.
5. Умножение чисел, результат сохранить в MySQL с последующим выводом в консоль.
6. Деление чисел, результат сохранить в MySQL с последующим выводом в консоль.
7. Деление чисел по модулю (остаток), результат сохранить в MySQL с последующим выводом в консоль.
8. Возведение числа в модуль, результат сохранить в MySQL с последующим выводом в консоль.
9. Возведение числа в степень, результат сохранить в MySQL с последующим выводом в консоль.
10. Сохранить все данные (вышеполученные результаты) из MySQL в Excel и вывести на экран. (https://www.geeksforgeeks.org/working-with-microsoft-excel-using-apache-poi-and-jexcel-api-with-a-maven-project-in-java/)
Объяснение некоторых методов и типов: 
1) ResultSet возвращает результаты выполнения SQL-запроса над базой данных. Он представляет собой таблицу данных, где каждая строка представляет запись, а каждый столбец — поле в базе данных. Используется для возвращения метаданных бд. Метод getTables из класса DatabaseMetaData возвращает информацию о таблицах в базе данных. Синтаксис:
ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types), где 
catalog: Каталог базы данных. Если не нужно фильтровать по каталогу, можно передать null.
schemaPattern: Шаблон схемы базы данных. Если фильтр не нужен, тоже можно передать null.
tableNamePattern: Шаблон названия таблицы. Символ % означает «все таблицы» (аналогично LIKE '%' в SQL).
types: Массив строк, указывающий, какие типы объектов нужны. Например, "TABLE" для таблиц, "VIEW" для представлений.
Первое null: Мы не фильтруем по каталогу, поэтому указываем null.
Второе null: Мы не фильтруем по схеме, поэтому тоже указываем null.
\"%\": Указывает, что мы хотим получить все таблицы (аналог SELECT *).
new String[]{\"TABLE\"}: Указывает, что нас интересуют только объекты типа «таблицы».
2) Использование BinaryOperator. это функциональный интерфейс в Java, который представляет операцию, принимающую два параметра и возвращающую одно значение. Оба параметра и тип возврата должны быть одного типа.
.apply() — это абстрактный метод функционального интерфейса BinaryOperator из Java, который применяется для выполнения операции над двумя однотипными аргументами и возвращает результат того же типа. Лямбда-функции: (один из параметров метода apply) (a, b) -> a * b;


package org.example;

import java.sql.*;
import java.util.Scanner;

public class MathOperations {

   private static final String URL = "jdbc:postgresql://localhost:5434/exam";
   private static final String USER = "postgres";
   private static final String PASSWORD = "root";

   public static void main(String[] args) {
       try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD);
            Scanner scanner = new Scanner(System.in)) {

           System.out.println("Подключение к базе данных установлено.");
           boolean running = true;

           while (running) {
               System.out.println("\nВыберите действие:");
               System.out.println("1. Вывести все таблицы");
               System.out.println("2. Создать таблицу");
               System.out.println("3. Сложение чисел");
               System.out.println("4. Вычитание чисел");
               System.out.println("5. Умножение чисел");
               System.out.println("6. Деление чисел");
               System.out.println("7. Деление по модулю");
               System.out.println("8. Модуль числа");
               System.out.println("9. Возведение в степень");
               System.out.println("0. Выход");

               int choice = scanner.nextInt();
               switch (choice) {
                   case 1:
                       listTables(connection);
                       break;
                   case 2:
                       createTable(connection);
                       break;
                   case 3:
                       performOperation(connection, scanner, "Сложение", Double::sum);
                       break;
                   case 4:
                       performOperation(connection, scanner, "Вычитание", (a, b) -> a - b);
                       break;
                   case 5:
                       performOperation(connection, scanner, "Умножение", (a, b) -> a * b);
                       break;
                   case 6:
                       performOperation(connection, scanner, "Деление", (a, b) -> a / b);
                       break;
                   case 7:
                       performOperation(connection, scanner, "Деление по модулю", (a, b) -> a % b);
                       break;
                   case 8:
                       performSingleOperation(connection, scanner, "Модуль", Math::abs);
                       break;
                   case 9:
                       performOperation(connection, scanner, "Возведение в степень", Math::pow);
                       break;
                   case 0:
                       running = false;
                       break;
                   default:
                       System.out.println("Некорректный выбор. Попробуйте снова.");
               }
           }
       } catch (SQLException e) {
           throw new RuntimeException(e);
       }
   }

   private static void listTables(Connection connection) throws SQLException {
       DatabaseMetaData metaData = connection.getMetaData();
       ResultSet tables = metaData.getTables(null, null, "%", new String[]{"TABLE"});
       System.out.println("Список таблиц в базе данных:");
       while (tables.next()) {
           System.out.println(tables.getString("TABLE_NAME"));
       }
   }
   private static void createTable(Connection connection) throws SQLException {
       String createTableSQL = "CREATE TABLE IF NOT EXISTS math_results ("
               + "id SERIAL PRIMARY KEY,"
               + "operation VARCHAR(50),"
               + "operand1 NUMERIC,"
               + "operand2 NUMERIC,"
               + "result NUMERIC"
               + ");";
       try (Statement statement = connection.createStatement()) {
           statement.execute(createTableSQL);
           System.out.println("Таблица math_results успешно создана (или уже существует).");
       }
   }

   private static void saveResult(Connection connection, String operationName, Double operand1, Double operand2, Double result) throws SQLException {
       String insertSQL = "INSERT INTO math_results (operation, operand1, operand2, result) VALUES (?, ?, ?, ?);";
       try (PreparedStatement preparedStatement = connection.prepareStatement(insertSQL)) {
           preparedStatement.setString(1, operationName);
           preparedStatement.setObject(2, operand1);
           preparedStatement.setObject(3, operand2);
           preparedStatement.setObject(4, result);
           preparedStatement.executeUpdate();
       }
   }

   private static void performOperation(Connection connection, Scanner scanner, String operationName, BinaryOperator operation) throws SQLException {
       System.out.println("Введите первое число:");
       double operand1 = scanner.nextDouble();
       System.out.println("Введите второе число:");
       double operand2 = scanner.nextDouble();
       double result = operation.apply(operand1, operand2);

       saveResult(connection, operationName, operand1, operand2, result);
       System.out.println(operationName + " результат: " + result);
   }

   private static void performSingleOperation(Connection connection, Scanner scanner, String operationName, UnaryOperator operation) throws SQLException {
       System.out.println("Введите число:");
       double operand = scanner.nextDouble();
       double result = operation.apply(operand);

       saveResult(connection, operationName, operand, null, result);
       System.out.println(operationName + " результат: " + result);
   }

   @FunctionalInterface
   interface BinaryOperator {
       double apply(double a, double b);
   }

   @FunctionalInterface
   interface UnaryOperator {
       double apply(double a);
   }
}

pom.xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>

   <groupId>org.example</groupId>
   <artifactId>Exam</artifactId>
   <version>1.0-SNAPSHOT</version>

   <properties>
       <maven.compiler.source>21</maven.compiler.source>
       <maven.compiler.target>21</maven.compiler.target>
       <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   <dependencies>
       <!-- https://mvnrepository.com/artifact/org.postgresql/postgresql -->
       <dependency>
           <groupId>org.postgresql</groupId>
           <artifactId>postgresql</artifactId>
           <version>42.7.3</version>
       </dependency>
   </dependencies>
</project>

4. Написать калькулятор для строковых выражений вида "<число> <операция> <число>", где <число> - положительное целое число меньшее 10, записанное словами, например, "четыре", <арифметическая операция> - одна из операций "плюс", "минус", "умножить". Результат выполнения операции вернуть в виде текстового представления числа. Пример: "пять плюс четыре" --> "девять".
import java.util.*;

public class Main {
   static int number = 0;
   static String[] numbers = new String[]{"ноль", "один", "два", "три", "четыре", "пять", "шесть", "семь", "восемь", "девять"};
  static Map<String, String> numberWords = new HashMap<>();
   public static int getNumber(String num) {
       for (int i = 0; i < 10; i++) {
           if (numbers[i].equals(num)) {
               return i;
           }
       }
       System.out.println("Такого числа нет!");
       return -1;

   }

   public static void getResult(int result, String num1, String num2, String oper){
       if (result > 20) {//если больше 20 так как потом едет сложение 20 и 1 = 21 30 и 5 =35
           char[] nums = Integer.toString(result).toCharArray(); //разбиваем число на цифры - первое деястки
           String firstNum = nums[0] + "0"; //прибавляем к строке с десятком ноль ->  получаем 20, 30 и тд
           String secondNum = String.valueOf(nums[1]); // цифру сохраянем как есть, 4, 5 или 9
           String firstN = numberWords.get(firstNum);
           String secondN = numberWords.get(secondNum);
           System.out.println(num1 + " " + oper + " на " + num2 + " = " + firstN + " " + secondN);
       } else {
           String resultStr = Integer.toString(result);
           String res = numberWords.get(resultStr);
           System.out.println(num1 + " " + oper + " на " + num2 + " = " + res);
       }
   }


   public static void main(String[] args) {

       int result = 0;

       numberWords.put("0", "ноль");
       numberWords.put("1", "один");
       numberWords.put("2", "два");
       numberWords.put("3", "три");
       numberWords.put("4", "четыре");
       numberWords.put("5", "пять");
       numberWords.put("6", "шесть");
       numberWords.put("7", "семь");
       numberWords.put("8", "восемь");
       numberWords.put("9", "девять");
       numberWords.put("10", "десять");
       numberWords.put("11", "одиннадцать");
       numberWords.put("12", "двенадцать");
       numberWords.put("13", "тринадцать");
       numberWords.put("14", "четырнадцать");
       numberWords.put("15", "пятнадцать");
       numberWords.put("16", "шестнадцать");
       numberWords.put("17", "семнадцать");
       numberWords.put("18", "восемнадцать");
       numberWords.put("19", "девятнадцать");
       numberWords.put("20", "двадцать");
       numberWords.put("30", "тридцать");
       numberWords.put("40", "сорок");
       numberWords.put("50", "пятьдесят");
       numberWords.put("60", "шестьдесят");
       numberWords.put("70", "семьдесят");
       numberWords.put("80", "восемьдесят");

       Scanner scanner = new Scanner(System.in);
       System.out.println("Введите первое число(строчно)");
       String num1 = scanner.nextLine().toLowerCase();
       System.out.println("Введите второе число(строчно)");
       String num2 = scanner.nextLine().toLowerCase();
       System.out.println("Введите операнда:");
       String oper = scanner.nextLine().toLowerCase();

       int numberOne = getNumber(num1);
       int numberTwo = getNumber(num2);

       if (Objects.equals(oper, "умножить")) {
           result = numberOne * numberTwo; // получаем числовой резалт
           getResult(result, num1, num2, oper);
       }
       if (Objects.equals(oper, "плюс")) {
           result = numberOne + numberTwo; // получаем числовой резалт
           getResult(result, num1, num2, oper);
       }
       if (Objects.equals(oper, "минус")) {
           result = numberOne - numberTwo; // получаем числовой резалт
           if (result < 0) {
               System.out.println("С минусами не работаем.");
           } else {
               getResult(result, num1, num2, oper);
           }
       }
   }
}


16. Создать интерфейс Progress c методами вычисления любого элемента прогрессии и суммы прогрессии. Разработать классы арифметической и геометрической прогрессии, которые имплементируют интерфейс Progress.
17. Разработать интерфейс InArray, в котором предусмотреть метод сложения двух массивов. Создать класс ArraySum, в котором имплементируется метод сложения массивов. Создать класс OrArray, в котором метод сложения массивов имплементируется как логическая операция ИЛИ между элементами массива.
InArray:
public interface InArray {
   int[] addArrays(int[] array1, int[] array2);
}

OrArray:
public class OrArray implements InArray {
   @Override
   public int[] addArrays(int[] array1, int[] array2) {
       int length = Math.min(array1.length, array2.length);
       int[] result = new int[length];
       for (int i = 0; i < length; i++) {
           result[i] = array1[i] | array2[i];
       }
       return result;
   }
}

ArraySum:
public class ArraySum implements InArray {
   @Override
   public int[] addArrays(int[] array1, int[] array2) {
       int length = Math.min(array1.length, array2.length);
       int[] result = new int[length];
       for (int i = 0; i < length; i++) {
           result[i] = array1[i] + array2[i];
       }
       return result;
   }
}

Main:
public class Main {
   public static void main(String[] args) {
       int[] array1 = {1, 2, 3};
       int[] array2 = {4, 5, 6};

       // ArraySum
       InArray sumImpl = new ArraySum();
       int[] sumResult = sumImpl.addArrays(array1, array2);
       System.out.println("Результат сложения массивов:");
       for (int num : sumResult) {
           System.out.print(num + " ");
       }

       System.out.println();

       // OrArray
       InArray orImpl = new OrArray();
       int[] orResult = orImpl.addArrays(array1, array2);
       System.out.println("Результат побитового сложения:");
       for (int num : orResult) {
           System.out.print(num + " ");
       }
   }
}
21. Разработать программу для игры «Угадайка». Программа загадывает случайное число от 1 до 10, требуется его отгадать с трех попыток. После каждой попытки, если результат неверен, игроку выводится сообщение, меньше или больше названное игроком число, чем загаданное. Сет заканчивается или если игрок угадывает число, или если исчерпывает три попытки, не угадав. Игра должна быть выполнена в бесконечном цикле, и продолжается до тех пор, пока на предложение «Сыграем еще раз?» игрок не напишет «Нет».
import java.util.Random;
import java.util.Scanner;

public class GuessingGame {

   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);
       Random random = new Random();
       String playAgain;

       do {
           int secretNumber = random.nextInt(10) + 1; // Генерация случайного числа от 1 до 10
           int attempts = 3;
           boolean guessedCorrectly = false;

           System.out.println("Я загадал число от 1 до 10. Попробуй угадать его за 3 попытки.");

           for (int i = 0; i < attempts; i++) {
               System.out.print("Попытка " + (i + 1) + ": Введите ваше предположение: ");
               int guess = scanner.nextInt();

               if (guess == secretNumber) {
                   System.out.println("Поздравляю! Вы угадали число!");
                   guessedCorrectly = true;
                   break;
               } else if (guess < secretNumber) {
                   System.out.println("Загаданное число больше.");
               } else {
                   System.out.println("Загаданное число меньше.");
               }
           }

           if (!guessedCorrectly) {
               System.out.println("К сожалению, вы не угадали число. Загаданное число было: " + secretNumber);
           }

           System.out.print("Сыграем еще раз? (Введите 'Нет' для выхода): ");
           playAgain = scanner.next();

       } while (!playAgain.equalsIgnoreCase("Нет"));

       System.out.println("Спасибо за игру! До свидания!");
       scanner.close();
   }
}

22. Разработайте программу-генератор рабочего календаря. Слесарь механосборочного цеха работает сутки через трое. Если смена попадает на воскресенье, то переносится на понедельник. По введенной дате программа должна генерировать расписание из дат на текущий месяц на 2022 год.
public class WorkScheduleGenerator {
   public static void main(String[] args) {
       Scanner scanner = new Scanner(System.in);
       System.out.print("Введите дату (в формате ГГГГ-ММ-ДД): ");
       String inputDate = scanner.nextLine();

       // Парсим введенную дату
       LocalDate startDate = LocalDate.parse(inputDate);
       int year = 2022; // Устанавливаем год на 2022
       Month month = startDate.getMonth();

       // Генерируем расписание
       List<LocalDate> schedule = generateWorkSchedule(year, month);

       // Выводим расписание
       System.out.println("Рабочий календарь на " + month + " " + year + ":");
       for (LocalDate date : schedule) {
           System.out.println(date);
       }

       scanner.close();
   }

   private static List<LocalDate> generateWorkSchedule(int year, Month month) {
       List<LocalDate> schedule = new ArrayList<>();
       LocalDate currentDate = LocalDate.of(year, month, 1);

       // Находим последний день месяца
       LocalDate lastDate = currentDate.withDayOfMonth(currentDate.lengthOfMonth());

       // Начинаем с первого рабочего дня
       LocalDate workDay = currentDate;

       while (!workDay.isAfter(lastDate)) {
           // Если это воскресенье, переносим на понедельник
           if (workDay.getDayOfWeek() == DayOfWeek.SUNDAY) {
               workDay = workDay.plusDays(1);
           }

           // Добавляем рабочий день в расписание
           schedule.add(workDay);

           // Переходим к следующему рабочему дню (через 3 дня)
           workDay = workDay.plusDays(3);
       }

       return schedule;
   }
}

24. Создайте класс Form - оболочку для создания и ввода пароля. Он должен иметь методы input, submit, password. Создайте класс SmartForm, который будет наследовать от Form и сохранять значения password.
public class Form {
   private String input; // Поле для хранения ввода
   private String password; // Поле для хранения пароля

   //Метод для ввода данных
   public void input(String data) {
       this.input = data;
       System.out.println("Введенные данные: " + this.input);
   }

   //Метод для установки пароля
   public void password(String password) {
       this.password = password;
       System.out.println("Пароль установлен.");
   }

   //Метод для отправки формы
   public void submit() {
       System.out.println("Форма отправлена с данными: " + this.input);
   }
}



import java.util.ArrayList;
import java.util.List;

public class SmartForm extends Form {
   private List<String> savedPasswords; //Список для хранения паролей

   public SmartForm() {
       savedPasswords = new ArrayList<>(); //Инициализация списка
   }

   @Override
   public void password(String password) {
       super.password(password); //Вызов метода родительского класса
       savedPasswords.add(password); //Сохранение пароля в список
       System.out.println("Пароль сохранен: " + password);
   }

   //Метод для получения сохраненных паролей
   public List<String> getSavedPasswords() {
       return savedPasswords;
   }
}




public class Main {
   public static void main(String[] args) {
       Form form = new Form();
       form.input("Пример ввода");
       form.password("12345");
       form.submit();

       System.out.println();

       SmartForm smartForm = new SmartForm();
       smartForm.input("Данные для умной формы");
       smartForm.password("password1");
       smartForm.password("password2");
       smartForm.submit();

       System.out.println("Сохраненные пароли: " + smartForm.getSavedPasswords());
   }
}

36. Разработать программу для поочередной обработки текстовых файлов. Файлы созданы со следующими именами: n.txt, где n – натуральное число. В файлах записаны: в первой строке одно число с плавающей запятой, во второй строке – второе число. Пользователь вводит название файла и требуемую операцию над числами (сложение, умножение, разность). Результат выводится на экран и файл n_out.txt.
40. Напишите программу, которая каждые 5 секунд отображает на экране данные о времени, прошедшем от начала запуска программы, а другой её поток выводит сообщение каждые 7 секунд. Третий поток выводит на экран сообщение каждые 10 секунд. Программа работает одну минуту, затем останавливается. Все результаты после вывода необходимо сохранить в MySQL/PostgreSQL.
CREATE TABLE results (
    id SERIAL PRIMARY KEY,
    message VARCHAR(255),
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class MultiThreadedApp {

    private static final String DB_URL = "jdbc:postgresql://localhost:5432/result";
    private static final String DB_USER = "postgres";
    private static final String DB_PASSWORD = "postgres";

    public static void main(String[] args) {
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(3);

        // Выводит время каждые 5 секунд
        scheduler.scheduleAtFixedRate(() -> {
            long currentTime = System.currentTimeMillis() - startTime;
            String message = "Время прошло: " + currentTime / 1000 + " секунд";
            System.out.println(message);
            saveToDatabase(message);
        }, 0, 5, TimeUnit.SECONDS);

        // Выводит сообщение каждые 7 секунд
        scheduler.scheduleAtFixedRate(() -> {
            String message = "Сообщение каждые 7 секунд";
            System.out.println(message);
            saveToDatabase(message);
        }, 0, 7, TimeUnit.SECONDS);

        // Выводит сообщение каждые 10 секунд
        scheduler.scheduleAtFixedRate(() -> {
            String message = "Сообщение каждые 10 секунд";
            System.out.println(message);
            saveToDatabase(message);
        }, 0, 10, TimeUnit.SECONDS);

        // Останавливаем программу через 1 минуту
        scheduler.schedule(() -> {
            scheduler.shutdown();
            System.out.println("Программа остановлена");
        }, 60, TimeUnit.SECONDS);
    }

    private static long startTime = System.currentTimeMillis();

    private static void saveToDatabase(String message) {
        String sql = "INSERT INTO results (message) VALUES (?)";
        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setString(1, message);
            pstmt.executeUpdate();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

45. Разработка веб-MVC приложения на основе Spring Boot. Приложение должно генерировать последовательность из 1000 случайных чисел в диапазоне, заданном пользователем, и выводит эти числа на экран и вычисляет их среднее арифметическое.
Основной класс:
package org.example.thousandgeneration;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ThousandGenerationApplication {

   public static void main(String[] args) {
       SpringApplication.run(ThousandGenerationApplication.class, args);
   }

}

Контроллер:
package org.example.thousandgeneration;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

import java.util.Random;

@Controller
public class RandomNumberController {

   @GetMapping("/")
   public String index() {
       return "index";
   }

   @GetMapping("/generate")
   public String generateRandomNumbers(@RequestParam int min, @RequestParam int max, Model model) {
       int[] randomNumbers = new int[1000];
       Random random = new Random();
       double sum = 0;

       for (int i = 0; i < 1000; i++) {
           randomNumbers[i] = random.nextInt((max - min) + 1) + min;
           sum += randomNumbers[i];
       }

       double average = sum / 1000;

       model.addAttribute("randomNumbers", randomNumbers);
       model.addAttribute("average", average);

       return "result";
   }
}

index.html:
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <title>Генератор случайных чисел</title>
</head>
<body>
<h1>Генератор случайных чисел</h1>
<form action="/generate" method="get">
   <label for="min">Нижняя граница:</label>
   <input type="number" id="min" name="min" required><br><br>
   <label for="max">Верхняя граница:</label>
   <input type="number" id="max" name="max" required><br><br>
   <input type="submit" value="Сгенерировать">
</form>
</body>
</html>
result.html:
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <title>Результат генерации</title>
</head>
<body>
<h1>Сгенерированные числа</h1>
<p>Среднее: <span th:text="${average}"></span></p>
<ul>
   <li th:each="number : ${randomNumbers}" th:text="${number}"></li>
</ul>
<a href="/">Generate New Numbers</a>
</body>
</html>

46. Разработать приложение для работы с локальной базой данных MySQL. Создайте базу данных мобильных телефонов (не менее 10 позиций), со следующими полями: производитель, модель, год выпуска, диагональ экрана. Напишите методы для выполнения запросов к базе данных. Все данные должны выводиться в консоли на экран.

CREATE DATABASE mobile_store;

USE mobile_store;

CREATE TABLE mobile_phones (
    id SERIAL PRIMARY KEY,
    manufacturer VARCHAR(50),
    model VARCHAR(50),
    release_year INT,
    screen_size DECIMAL(3,1)
);

INSERT INTO mobile_phones (manufacturer, model, release_year, screen_size) VALUES
('Apple', 'iPhone 14', 2022, 6.1),
('Samsung', 'Galaxy S23', 2023, 6.2),
('Xiaomi', 'Mi 11', 2021, 6.8),
('Google', 'Pixel 7', 2022, 6.3),
('OnePlus', '10 Pro', 2022, 6.7),
('Sony', 'Xperia 1 IV', 2022, 6.5),
('Huawei', 'P50 Pro', 2021, 6.6),
('Nokia', 'G60', 2022, 6.6),
('Realme', 'GT 2 Pro', 2022, 6.7),
('Asus', 'ROG Phone 6', 2022, 6.8);

Это просто код для постгреса, чтобы были данные

package org.example;

import java.sql.*;

public class PhonesBD {

   private static final String URL = "jdbc:postgresql://localhost:5434/exam";
   private static final String USER = "postgres";
   private static final String PASSWORD = "root";

   public static void main(String[] args) {
       try (Connection connection = DriverManager.getConnection(URL, USER, PASSWORD)) {
           System.out.println("Соединение с базой данных установлено!");

           // Вывод всех записей из таблицы
           printAllPhones(connection);

           // Добавление нового телефона
           addPhone(connection, "Motorola", "Edge 30", 2022, 6.55);

           // Обновление записи
           updatePhone(connection, 1, "Apple", "iPhone 15", 2023, 6.7);

           // Удаление записи
           deletePhone(connection, 2);

           // Повторный вывод всех записей
           printAllPhones(connection);

       } catch (SQLException e) {
           System.err.println("Ошибка при работе с базой данных: " + e.getMessage());
       }
   }

   // Вывод всех телефонов
   public static void printAllPhones(Connection connection) throws SQLException {
       String query = "SELECT * FROM mobile_phones";
       try (Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery(query)) {

           System.out.println("Список мобильных телефонов:");
           while (resultSet.next()) {
                       int id = resultSet.getInt("id");
                       String manf = resultSet.getString("manufacturer");
                       String model = resultSet.getString("model");
                       int year = resultSet.getInt("release_year");
                       double size = resultSet.getDouble("screen_size");
               System.out.println("ID:" + id + " Производитель: " + manf + " Модель: " + model + " Год выпуска: " + year + " Диагональ: "+ size);
           }
       }
   }

   // Добавление нового телефона
   public static void addPhone(Connection connection, String manufacturer, String model, int releaseYear, double screenSize) throws SQLException {
       String query = "INSERT INTO mobile_phones (manufacturer, model, release_year, screen_size) VALUES (?, ?, ?, ?)";
       try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
           preparedStatement.setString(1, manufacturer);
           preparedStatement.setString(2, model);
           preparedStatement.setInt(3, releaseYear);
           preparedStatement.setDouble(4, screenSize);
           preparedStatement.executeUpdate();
           System.out.println("Телефон добавлен: " + manufacturer + " " + model);
       }
   }

   // Обновление записи
   public static void updatePhone(Connection connection, int id, String manufacturer, String model, int releaseYear, double screenSize) throws SQLException {
       String query = "UPDATE mobile_phones SET manufacturer = ?, model = ?, release_year = ?, screen_size = ? WHERE id = ?";
       try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
           preparedStatement.setString(1, manufacturer);
           preparedStatement.setString(2, model);
           preparedStatement.setInt(3, releaseYear);
           preparedStatement.setDouble(4, screenSize);
           preparedStatement.setInt(5, id);
           preparedStatement.executeUpdate();
           System.out.println("Телефон обновлён: ID " + id);
       }
   }

   // Удаление записи
   public static void deletePhone(Connection connection, int id) throws SQLException {
       String query = "DELETE FROM mobile_phones WHERE id = ?";
       try (PreparedStatement preparedStatement = connection.prepareStatement(query)) {
           preparedStatement.setInt(1, id);
           preparedStatement.executeUpdate();
           System.out.println("Телефон с ID " + id + " удалён.");
       }
   }
}

18. Создать класс Binary для работы с двоичными числами фиксированной длины. Число должно быть массивом тип char, каждый элемент которого принимает значение 0 или 1. Младший бит имеет младший индекс. Отрицательные числа представляются в дополнительном коде. Дополнительный код получается инверсией всех битов с прибавлением 1 к младшему биту. Например, +1 – это в двоичном коде будет выглядеть, как 0000 0001. А -1 в двоичном коде будет выглядеть, как 1111 1110 + 0000 0001 = 1111 1111. Создать методы конвертации десятичного числа в массив и обратно.
public class Main {

   public static void main(String[] args) {
       Binary binaryNumber = new Binary(8); // Длина числа — 8 бит

       int decimalNumber = -5;

       binaryNumber.fromDecimal(decimalNumber);

       System.out.println("Двоичное представление: " + binaryNumber.display());

       int convertedBackToDecimal = binaryNumber.toDecimal(); // Предполагается, что метод toDecimal реализован

       System.out.println("Преобразованное обратно в десятичное: " + convertedBackToDecimal);

   }
}

public class Binary  {

   int length;
   char[] number;


   public Binary(int length) {
       this.length = length;
       this.number = new char[length];
   }

   public char[] fromDecimal(int num) {

       boolean isNegative = num < 0;
       if (isNegative) {
           num = Math.abs(num);
       }

       for (int i = 0; i < length; i++) {
           number[i] = (char) ('0' + (num % 2)); // Остаток от деления на 2 (0 или 1)
           num /= 2; // Делим число на 2
       }

       if (isNegative) {
           toTwoComplement();
       }
       return number;
   }

   public int toDecimal() {
       int decimal = 0;

       // Проверяем, является ли число отрицательным (старший бит равен '1')
       boolean isNegative = number[length - 1] == '1';

       // Если число отрицательное, преобразуем из дополнительного кода
       if (isNegative) {
           fromTwoComplement(); // Преобразуем из дополнительного кода
       }

       // Вычисляем десятичное значение
       for (int i = length - 1; i >= 0; i--) {
           decimal = decimal * 2 + (number[i] - '0'); // Умножаем на основание (2) и добавляем текущий бит
       }

       // Если число было отрицательным, возвращаем его с минусом
       return isNegative ? -decimal : decimal;
   }
   private void toTwoComplement() {
       // Инверсия всех битов
       for (int i = 0; i < length; i++) {
           number[i] = (number[i] == '0') ? '1' : '0';
       }

       // Прибавляем 1 к младшему биту
       for (int i = 0; i < length; i++) {
           if (number[i] == '0') {
               number[i] = '1';
               break;
           } else {
               number[i] = '0'; // Переносим единицу дальше
           }
       }
   }
   private void fromTwoComplement() {
       // Прибавляем 1 к числу
       for (int i = 0; i < length; i++) {
           if (number[i] == '1') {
               number[i] = '0';
           } else {
               number[i] = '1';
               break;
           }
       }

       // Инверсия всех битов
       for (int i = 0; i < length; i++) {
           number[i] = (number[i] == '0') ? '1' : '0';
       }
   }
   public String display() {
       StringBuilder sb = new StringBuilder();
       for (int i = length - 1; i >= 0; i--) { // Обратный порядок для отображения
           sb.append(number[i]);
       }
       return sb.toString();
   }
}

26. Создайте класс ColorModel для определения цветовой модели. Разработайте подклассы RGBconverter и CMYKconverter для конвертации цвета из одной модели в другую. Конвертация CMYK в RGB производится по следующим формулам: R = 255 × (1-C) × (1-K), G = 255 × (1-M) × (1-K), B = 255 × (1-Y) × (1-K) (где R – red, G – green, B – black, C – Cyan, M - Magenta, Y - Yellow, K- Black))
 Базовый класс ColorModel
public abstract class ColorModel {
   public abstract void convert();
}
Подкласс RGBconverter
public class RGBconverter extends ColorModel {
   private int red;
   private int green;
   private int blue;

   public RGBconverter(int red, int green, int blue) {
       this.red = red;
       this.green = green;
       this.blue = blue;
   }

   @Override
   public void convert() {
       double r = red / 255.0;
       double g = green / 255.0;
       double b = blue / 255.0;

       double k = 1 - Math.max(Math.max(r, g), b);
       double c = (1 - r - k) / (1 - k);
       double m = (1 - g - k) / (1 - k);
       double y = (1 - b - k) / (1 - k);

       System.out.println("CMYK: C=" + c + ", M=" + m + ", Y=" + y + ", K=" + k);
   }
}
Подкласс CMYKconverter
public class CMYKconverter extends ColorModel {
   private double cyan;
   private double magenta;
   private double yellow;
   private double black;

   public CMYKconverter(double cyan, double magenta, double yellow, double black) {
       this.cyan = cyan;
       this.magenta = magenta;
       this.yellow = yellow;
       this.black = black;
   }

   @Override
   public void convert() {
       int r = (int) (255 * (1 - cyan) * (1 - black));
       int g = (int) (255 * (1 - magenta) * (1 - black));
       int b = (int) (255 * (1 - yellow) * (1 - black));

       System.out.println("RGB: R=" + r + ", G=" + g + ", B=" + b);
   }
}

28. Разработать класс Neuron для реализации нейронной сети из двух нейронов и одного выхода. Сделать функцию прямого распространения с функцией активации в виде сигмоиды.
41. Условие задачи: «Ввести две строки (не менее 50 символов каждая) с клавиатуры. Необходимо вывести на экран две введенных ранее строки, подсчитать и вывести размер длины каждой строки, объединить данные строки в одну, сравнить данные строки и результат сравнения вывести на экран». По данному условию необходимо реализовать программу с интерактивным консольным меню, (т.е. вывод списка действий по цифрам. При этом при нажатии на цифру у нас должно выполняться определенное действие). При этом в программе данные пункты должны называться следующим образом:
1. Вывести все таблицы из MySQL.
2. Создать таблицу в MySQL.
3. Ввести две строки с клавиатуры, результат сохранить в MySQL с последующим выводом в консоль.
4. Подсчитать размер ранее введенных строк, результат сохранить в MySQL с последующим выводом в консоль.
5. Объединить две строки в единое целое, результат сохранить в MySQL с последующим выводом в консоль.
6. Сравнить две ранее введенные строки, результат сохранить в MySQL с последующим выводом в консоль.
7. Сохранить все данные (выше полученные результаты) из MySQL в Excel и вывести на экран.
package org.example;

import java.sql.*;
import java.util.Scanner;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import java.io.FileOutputStream;

public class Main {
   private static final String DB_URL = "jdbc:postgresql://localhost:5432/postgres";
   private static final String DB_USER = "postgres";
   private static final String DB_PASSWORD = "postgres";
   private static final Scanner scanner = new Scanner(System.in);

   public static void main(String[] args) {
       while (true) {
           System.out.println("\nВыберите действие:");
           System.out.println("1. Вывести все таблицы из PostgreSQL");
           System.out.println("2. Создать таблицу в PostgreSQL");
           System.out.println("3. Ввести две строки с клавиатуры, результат сохранить в PostgreSQL с выводом");
           System.out.println("4. Подсчитать длины строк, результат сохранить в PostgreSQL с выводом");
           System.out.println("5. Объединить строки, результат сохранить в PostgreSQL с выводом");
           System.out.println("6. Сравнить строки, результат сохранить в PostgreSQL с выводом");
           System.out.println("7. Сохранить данные из PostgreSQL в Excel и вывести");
           System.out.println("0. Выход");

           int choice = scanner.nextInt();
           scanner.nextLine();

           switch (choice) {
               case 1 -> showTables();
               case 2 -> createTable();
               case 3 -> insertStrings();
               case 4 -> calculateStringLengths();
               case 5 -> concatenateStrings();
               case 6 -> compareStrings();
               case 7 -> saveToExcel();
               case 0 -> {
                   System.out.println("Выход из программы.");
                   System.exit(0);
               }
               default -> System.out.println("Неверный выбор. Попробуйте снова.");
           }
       }
   }

   // 1. Вывести все таблицы из PostgreSQL
   private static void showTables() {
       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery(
                    "SELECT table_name FROM information_schema.tables WHERE table_schema = 'public'")) {

           System.out.println("Список таблиц:");
           while (resultSet.next()) {
               System.out.println(resultSet.getString(1));
           }
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 2. Создать таблицу в PostgreSQL
   private static void createTable() {
       String createTableSQL = """
               CREATE TABLE IF NOT EXISTS strings_data (
                  id SERIAL PRIMARY KEY,
                  string1 TEXT,
                  string2 TEXT,
                  length1 INT,
                  length2 INT,
                  concatenated_string TEXT,
                  comparison_result TEXT
               )
               """;

       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement()) {

           statement.execute(createTableSQL);
           System.out.println("Таблица создана или уже существует.");
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 3. Ввести две строки с клавиатуры, результат сохранить в PostgreSQL с выводом
   private static void insertStrings() {
       System.out.print("Введите первую строку (не менее 50 символов): ");
       String string1 = scanner.nextLine();
       System.out.print("Введите вторую строку (не менее 50 символов): ");
       String string2 = scanner.nextLine();

       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            PreparedStatement statement = connection.prepareStatement(
                    "INSERT INTO strings_data (string1, string2) VALUES (?, ?)")) {

           statement.setString(1, string1);
           statement.setString(2, string2);
           statement.executeUpdate();

           System.out.println("Строки успешно сохранены в PostgreSQL.");
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 4. Подсчитать длины строк, результат сохранить в PostgreSQL с выводом
   private static void calculateStringLengths() {
       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery("SELECT * FROM strings_data ORDER BY id DESC LIMIT 1")) {

           if (resultSet.next()) {
               String string1 = resultSet.getString("string1");
               String string2 = resultSet.getString("string2");
               int length1 = string1.length();
               int length2 = string2.length();

               System.out.println("Длина первой строки: " + length1);
               System.out.println("Длина второй строки: " + length2);

               PreparedStatement updateStatement = connection.prepareStatement(
                       "UPDATE strings_data SET length1 = ?, length2 = ? WHERE id = ?");
               updateStatement.setInt(1, length1);
               updateStatement.setInt(2, length2);
               updateStatement.setInt(3, resultSet.getInt("id"));
               updateStatement.executeUpdate();
           }
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 5. Объединить строки, результат сохранить в PostgreSQL с выводом
   private static void concatenateStrings() {
       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery("SELECT * FROM strings_data ORDER BY id DESC LIMIT 1")) {

           if (resultSet.next()) {
               String concatenated = resultSet.getString("string1") + resultSet.getString("string2");
               System.out.println("Объединенные строки: " + concatenated);

               PreparedStatement updateStatement = connection.prepareStatement(
                       "UPDATE strings_data SET concatenated_string = ? WHERE id = ?");
               updateStatement.setString(1, concatenated);
               updateStatement.setInt(2, resultSet.getInt("id"));
               updateStatement.executeUpdate();
           }
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 6. Сравнить строки, результат сохранить в PostgreSQL с выводом
   private static void compareStrings() {
       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery("SELECT * FROM strings_data ORDER BY id DESC LIMIT 1")) {

           if (resultSet.next()) {
               String string1 = resultSet.getString("string1");
               String string2 = resultSet.getString("string2");
               String comparisonResult = string1.equals(string2) ? "Равны" : "Не равны";

               System.out.println("Результат сравнения строк: " + comparisonResult);

               PreparedStatement updateStatement = connection.prepareStatement(
                       "UPDATE strings_data SET comparison_result = ? WHERE id = ?");
               updateStatement.setString(1, comparisonResult);
               updateStatement.setInt(2, resultSet.getInt("id"));
               updateStatement.executeUpdate();
           }
       } catch (SQLException e) {
           e.printStackTrace();
       }
   }

   // 7. Сохранить данные из PostgreSQL в Excel
   private static void saveToExcel() {
       String excelFilePath = "strings_data.xlsx";

       try (Connection connection = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery("SELECT * FROM strings_data");
            Workbook workbook = new XSSFWorkbook();
            FileOutputStream outputStream = new FileOutputStream(excelFilePath)) {

           Sheet sheet = workbook.createSheet("Данные строк");
           Row header = sheet.createRow(0);

           header.createCell(0).setCellValue("ID");
           header.createCell(1).setCellValue("Строка 1");
           header.createCell(2).setCellValue("Строка 2");
           header.createCell(3).setCellValue("Длина 1");
           header.createCell(4).setCellValue("Длина 2");
           header.createCell(5).setCellValue("Объединенная строка");
           header.createCell(6).setCellValue("Результат сравнения");

           int rowIndex = 1;
           while (resultSet.next()) {
               Row row = sheet.createRow(rowIndex++);
               row.createCell(0).setCellValue(resultSet.getInt("id"));
               row.createCell(1).setCellValue(resultSet.getString("string1"));
               row.createCell(2).setCellValue(resultSet.getString("string2"));
               row.createCell(3).setCellValue(resultSet.getInt("length1"));
               row.createCell(4).setCellValue(resultSet.getInt("length2"));
               row.createCell(5).setCellValue(resultSet.getString("concatenated_string"));
               row.createCell(6).setCellValue(resultSet.getString("comparison_result"));
           }

           workbook.write(outputStream);
           System.out.println("Данные успешно сохранены в " + excelFilePath);
       } catch (Exception e) {
           e.printStackTrace();
       }
   }
}
POM.XML
<dependencies>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.7.5</version>
        </dependency>
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi-ooxml</artifactId>
            <version>5.3.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.23.1</version>
        </dependency>
    </dependencies>

42. Написать на основе Spring Boot клиент-серверное приложение MyUser, в котором можно управлять данными пользователей из базы данных через веб-интерфейс: имя, фамилия, возраст, номер группы. База данных может быть любой – MySQL, PostgreSQL и т.д. При этом должна быть доступна возможность добавления/удаления/редактирования пользователей.
Зависимости в spring проекте: Spring Web, Spring Data JPA, PostgreSQL Driver.

1.	Создать бд в postgresql myuserdb
2.	application.properties
spring.application.name=user
spring.datasource.url=jdbc:postgresql://localhost:5432/myuserdb
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
3.	Код
@Entity
@Table(name = "my_user")
public class User {
   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   private Long id;
   private String firstName;
   private String lastName;
   private int age;
   private String groupNumber;

   // Getters and Setters
   public Long getId() {
       return id;
   }

   public void setId(Long id) {
       this.id = id;
   }

   public String getFirstName() {
       return firstName;
   }

   public void setFirstName(String firstName) {
       this.firstName = firstName;
   }

   public String getLastName() {
       return lastName;
   }

   public void setLastName(String lastName) {
       this.lastName = lastName;
   }

   public int getAge() {
       return age;
   }

   public void setAge(int age) {
       this.age = age;
   }

   public String getGroupNumber() {
       return groupNumber;
   }

   public void setGroupNumber(String groupNumber) {
       this.groupNumber = groupNumber;
   }
}

@SpringBootApplication
public class UserApplication {

   public static void main(String[] args) {
      SpringApplication.run(UserApplication.class, args);
   }

}

@RestController
@RequestMapping("/api/users")
public class UserController {
   @Autowired
   private UserService userService;

   @GetMapping
   public List<User> getAllUsers() {
       return userService.getAllUsers();
   }

   @GetMapping("/{id}")
   public Optional<User> getUserById(@PathVariable Long id) {
       return userService.getUserById(id);
   }

   @PostMapping
   public User createUser(@RequestBody User user) {
       return userService.saveUser(user);
   }

   @PutMapping("/{id}")
   public User updateUser(@PathVariable Long id, @RequestBody User userDetails) {
       User user = userService.getUserById(id).orElseThrow();
       user.setFirstName(userDetails.getFirstName());
       user.setLastName(userDetails.getLastName());
       user.setAge(userDetails.getAge());
       user.setGroupNumber(userDetails.getGroupNumber());
       return userService.saveUser(user);
   }

   @DeleteMapping("/{id}")
   public void deleteUser(@PathVariable Long id) {
       userService.deleteUser(id);
   }
}

public interface UserRepository extends JpaRepository<User, Long> {
}

@Service
public class UserService {
   @Autowired
   private UserRepository userRepository;

   public List<User> getAllUsers() {
       return userRepository.findAll();
   }

   public Optional<User> getUserById(Long id) {
       return userRepository.findById(id);
   }

   public User saveUser(User user) {
       return userRepository.save(user);
   }

   public void deleteUser(Long id) {
       userRepository.deleteById(id);
   }
}

4.	В папке resources/static 
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>MyUser App</title>
   <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
   <style>
       .user-item {
           margin-bottom: 10px;
       }
       .user-item button {
           margin-left: 10px;
       }
   </style>
</head>
<body>
<h1>User Management</h1>
<div>
   <h2>Add User</h2>
   <form id="add-user-form">
       <input type="text" id="firstName" placeholder="First Name" required><br>
       <input type="text" id="lastName" placeholder="Last Name" required><br>
       <input type="number" id="age" placeholder="Age" required><br>
       <input type="text" id="groupNumber" placeholder="Group Number" required><br>
       <button type="submit">Add User</button>
   </form>
</div>
<div id="user-list"></div>

<script>
   function loadUsers() {
       axios.get('/api/users')
           .then(response => {
               const users = response.data;
               const userList = document.getElementById('user-list');
               userList.innerHTML = '';
               users.forEach(user => {
                   const userDiv = document.createElement('div');
                   userDiv.className = 'user-item';
                   userDiv.innerHTML = `
                       <p>${user.firstName} ${user.lastName} - ${user.age} - ${user.groupNumber}</p>
                       <button onclick="editUser(${user.id})">Edit</button>
                       <button onclick="deleteUser(${user.id})">Delete</button>
                   `;
                   userList.appendChild(userDiv);
               });
           })
           .catch(error => {
               console.error('There was an error fetching the users!', error);
           });
   }

   function addUser(event) {
       event.preventDefault();
       const firstName = document.getElementById('firstName').value;
       const lastName = document.getElementById('lastName').value;
       const age = document.getElementById('age').value;
       const groupNumber = document.getElementById('groupNumber').value;

       axios.post('/api/users', {
           firstName: firstName,
           lastName: lastName,
           age: age,
           groupNumber: groupNumber
       })
       .then(response => {
           loadUsers();
           document.getElementById('add-user-form').reset();
       })
       .catch(error => {
           console.error('There was an error adding the user!', error);
       });
   }

   function editUser(id) {
       const firstName = prompt('Enter new first name:');
       const lastName = prompt('Enter new last name:');
       const age = prompt('Enter new age:');
       const groupNumber = prompt('Enter new group number:');

       axios.put(`/api/users/${id}`, {
           firstName: firstName,
           lastName: lastName,
           age: age,
           groupNumber: groupNumber
       })
       .then(response => {
           loadUsers();
       })
       .catch(error => {
           console.error('There was an error editing the user!', error);
       });
   }

   function deleteUser(id) {
       axios.delete(`/api/users/${id}`)
           .then(response => {
               loadUsers();
           })
           .catch(error => {
               console.error('There was an error deleting the user!', error);
           });
   }

   document.getElementById('add-user-form').addEventListener('submit', addUser);

   loadUsers();
</script>
</body>
</html>

5.	Запускать по адресу http://localhost:8080
43. Написать на основе Spring Boot Security форму для авторизации и регистрации пользователя. При этом после авторизации пользователя должно быть перенаправление на главную страницу. Главная страница должна содержать запись «Hello World!». При этом до авторизации главная страница не должна быть доступна для пользователя.
//CustomUserDetailsService

package org.example.task_43;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;


@Service
public class CustomUserDetailsService implements UserDetailsService {
    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        return userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User not found: " + username));
    }
}

```
```
// Task43Application

package org.example.task_43;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Task43Application {

    public static void main(String[] args) {
        SpringApplication.run(Task43Application.class, args);
    }

}

```
```
//UserController

package org.example.task_43;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;

@Controller
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/login")
    public String login() {
        return "login";
    }

    @GetMapping("/register")
    public String registerForm(Model model) {
        model.addAttribute("user", new Users());
        return "register";
    }

    @PostMapping("/register")
    public String register(Users user) {
        userService.register(user);
        return "redirect:/login";
    }

    @GetMapping("/")
    public String home() {
        return "home";
    }
}
```
```
// UserRepository

package org.example.task_43;

import org.springframework.data.jpa.repository.JpaRepository;
import java.util.Optional;

public interface UserRepository extends JpaRepository<Users, Long> {
    Optional<Users> findByUsername(String username);
}

```
```
// Users

package org.example.task_43;

import jakarta.persistence.*;
import lombok.*;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.Collection;
import java.util.List;

@Data
@Entity
public class Users implements UserDetails {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, unique = true)
    private String username;

    @Column(nullable = false)
    private String password;

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return List.of();
    }
}

```
```
//UserService

package org.example.task_43;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Autowired
    private UserRepository repo;
    @Autowired
    private PasswordEncoder passwordEncoder;


    public void register(Users user) {
        user.setPassword(passwordEncoder.encode(user.getPassword()));
        repo.save(user);
    }
}

```
```
// WebSecurityConfig

package org.example.task_43;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configurers.AbstractHttpConfigurer;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.beans.factory.annotation.Autowired;


@Configuration
@EnableWebSecurity
public class WebSecurityConfig {
    @Autowired
    private UserDetailsService userDetailsService;

    @Bean
    public static PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .csrf(AbstractHttpConfigurer::disable) // Отключение CSRF для простоты (не рекомендуется для production)
                .authorizeHttpRequests(authorize -> authorize
                        .requestMatchers("/register", "/login").permitAll() // Доступ к этим URL без авторизации
                        .anyRequest().authenticated() // Остальные запросы требуют авторизации
                )
                .formLogin(form -> form
                        .loginPage("/login")
                        .defaultSuccessUrl("/", true)
                        .permitAll()
                )
                .logout(logout -> logout
                        .logoutUrl("/logout") // URL для выхода
                        .logoutSuccessUrl("/login") // Перенаправление после выхода
                        .permitAll()
                );
        return http.build();
    }

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
                .userDetailsService(userDetailsService)
                .passwordEncoder(passwordEncoder());
    }
}

```
```
HOME

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Home</title>
</head>
<body>
<h1>Hello World!</h1>
<a th:href="@{/logout}">Logout</a>
</body>
</html>

```
```
LOGIN

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Login</title>
</head>
<body>
<form th:action="@{/login}" method="post">
    <div>
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required>
    </div>
    <div>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
    </div>
    <button type="submit">Login</button>
</form>
<p>Don't have an account? <a th:href="@{/register}">Register here</a></p>
</body>
</html>


```
```
REGISTER

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Register</title>
</head>
<body>
<form th:action="@{/register}" method="post">
    <div>
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
    </div>
    <div>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password">
    </div>
    <button type="submit">Register</button>
</form>
</body>
</html>


```
```
// application.properties

spring.application.name=task_43

spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=admin
spring.datasource.password=1234

spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect

spring.jpa.hibernate.ddl-auto=update


#spring.security.user.name=root
#spring.security.user.password=root
#spring.security.user.roles=manager


spring.cache.type=none
spring.thymeleaf.cache=false

spring.web.resources.add-mappings=true
server.port=5000
