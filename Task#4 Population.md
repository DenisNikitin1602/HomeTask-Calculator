import java.util.*;
import java.util.stream.Collectors;


public class Main {
    public static void main(String[] args) {

        List<String> names = Arrays.asList("Jack", "Connor", "Harry", "George", "Samuel", "John");
        List<String> families = Arrays.asList("Evans", "Young", "Harris", "Wilson", "Davies", "Adamson", "Brown");
        Collection<Person> persons = new ArrayList<>();
        for (int i = 0; i < 10_000_000; i++) {
            persons.add(new Person(
                    names.get(new Random().nextInt(names.size())),
                    families.get(new Random().nextInt(families.size())),
                    new Random().nextInt(100),
                    Sex.values()[new Random().nextInt(Sex.values().length)],
                    Education.values()[new Random().nextInt(Education.values().length)])
            );
        }

        long minorsCount = persons.stream()
                .filter(person -> person.getAge() < 18)
                .count();
        System.out.println("Количество несовершеннолетних: " + minorsCount);

        List<String> recruits = persons.stream()
                .filter(person -> person.getSex() == Sex.MAN)   // Мужчины
                .filter(person -> person.getAge() >= 18 && person.getAge() <= 27)   // В возрасте от 18 до 27 лет
                .map(Person::getFamily)   // Преобразуем в список фамилий
                .collect(Collectors.toList());
        System.out.println("Список призывников: " + recruits);

        List<Person> workablePersons = persons.stream()
                .filter(person -> person.getEducation() == Education.HIGHER)   // Высшее образование
                .filter(person ->
                        (person.getSex() == Sex.MAN && person.getAge() >= 18 && person.getAge() <= 65) ||
                                (person.getSex() == Sex.WOMAN && person.getAge() >= 18 && person.getAge() <= 60)
                )   // Работоспособные
                .sorted(Comparator.comparing(Person::getFamily))   // Сортировка по фамилии
                .collect(Collectors.toList());
        System.out.println("Работоспособные люди с высшим образованием: " + workablePersons);
    }
}

public enum Sex {
    MAN,
    WOMAN
}

public enum Education {
    ELEMENTARY,
    SECONDARY,
    FURTHER,
    HIGHER
}

class Person {
    private String name;
    private String family;
    private Integer age;
    private Sex sex;
    private Education education;

    public Person(String name, String family, int age, Sex sex, Education education) {
        this.name = name;
        this.family = family;
        this.age = age;
        this.sex = sex;
        this.education = education;
    }

    public String getName() {
        return name;
    }

    public String getFamily() {
        return family;
    }

    public Integer getAge() {
        return age;
    }

    public Sex getSex() {
        return sex;
    }

    public Education getEducation() {
        return education;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", family='" + family + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                ", education=" + education +
                '}';
    }
}
