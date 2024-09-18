
public class Main {
    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);

        // Создаем список для положительных чисел
        List<Integer> positiveEvenNumbers = new ArrayList<>();

        // Проходим по каждому элементу списка
        for (Integer number : intList) {
            // Проверяем, что число положительное и четное
            if (number > 0 && number % 2 == 0) {
                positiveEvenNumbers.add(number);
            }
        }

        // Сортируем список по возрастанию
        Collections.sort(positiveEvenNumbers);

        // Выводим результат на экран
        System.out.println(positiveEvenNumbers);
    }
}

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Stream;

public class StreamMain {
    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);

        Stream<Integer> stream = intList.stream();
                stream.filter(x -> x > 0)
                .filter(x -> x % 2 == 0)
                .sorted(Comparator.naturalOrder())
                .forEach(System.out::println);
    }
}
