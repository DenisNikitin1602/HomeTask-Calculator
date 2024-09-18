# HomeTask-Calculator

public class Main {
    public static void main(String[] args) {
        Calculator calc = Calculator.instance.get();

        int a = calc.plus.apply(1, 2);
        int b = calc.minus.apply(1,1);
        int c = calc.divide.apply(a, b);//нельзя делить на ноль, добавил исключение
        calc.println.accept(c);
    }
}

import java.util.function.*;

public class Calculator {

    // Статическая переменная типа Supplier, которая возвращает экземпляр Calculator
    public static Supplier<Calculator> instance = Calculator::new;

    // Конструктор класса
    public Calculator() {
        System.out.println("Calculator instance created.");
    }

    // Переменные для математических операций
    public static BinaryOperator<Integer> plus = (a, b) -> a + b;
    public static BinaryOperator<Integer> minus = (a, b) -> a - b;
    public static BinaryOperator<Integer> multiply = (a, b) -> a * b;
    public static BinaryOperator<Integer> divide = (a, b) -> {
        if (b == 0) {
            throw new ArithmeticException("Division by zero");
        }
        return a / b;
    };

    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;

    Predicate<Integer> isPositive = x -> x > 0;

    Consumer<Integer> println = System.out::println;
}
