## Задание 1. Калькулятор

public class Main {
    public static void main(String[] args) {

        Calculator calc = Calculator.instance.get();

        int a = calc.plus.apply(1, 2);
        int b = calc.minus.apply(1,1);
        int c = calc.devide.apply(a, b); // Деление на ноль.

        /* я предлагаю обернуть ошибку в блок try,
         я думаю, это лучше сделать в классе Calculator
         */

        calc.println.accept(c);
    }
}

import java.util.function.*;

public class Calculator {
    static Supplier<Calculator> instance = Calculator::new;

    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x * y;
    BinaryOperator<Integer> devide = (x, y) -> x / y;

    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;

    Predicate<Integer> isPositive = x -> x > 0;

    Consumer<Integer> println = System.out::println;

}

## Задание 2. Рабочий

public class Main {
    public static void main(String[] args) {
        Worker.OnTaskDoneListener listener = System.out::println;
        Worker worker = new Worker(listener);
        worker.start();
    }
}

public class Worker {
    @FunctionalInterface
    public interface OnTaskDoneListener {
        void onDone(String result);
    }
    private OnTaskDoneListener callback;

    public Worker(OnTaskDoneListener callback) {
        this.callback = callback;
    }

    public void start() {
        for (int i = 0; i < 100; i++) {
            callback.onDone("Task " + i + " is done");
        }
    }
}

