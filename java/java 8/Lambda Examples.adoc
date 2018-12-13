```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;
import java.util.stream.Collectors;

public class LambdaExamples {
    private static final List<String> NUMBERS = Arrays.asList("2", "5", "1", "8", "4");
    private static final List<String> CITIES = Arrays.asList("Pune", "Dilli", "Mumbai", "Nagpur", "Kharadi", "Mumbai");
    public static void main(String[] args) {
        System.out.println("#Print Hello");
        {
            Supplier supplier = () -> "Hello";
            System.out.println(supplier.get());
        }
        System.out.println("#Print Hello to User name provided as input");
        {
            Function<String, String> function = (String greet) -> "Hello " + greet;
            System.out.println(function.apply("Sumit"));
        }
        System.out.println("#Print Hello to User name provided as input then greet");
        {
            Function<String, String> name = (String user) -> "Hello " + user;
            Function<String, String> greet = (String message) -> message + " Welcome";
            System.out.println(name.compose(greet).apply("Sumit"));
        }
        System.out.println("#Print True only if all characters are in upper case. Input - Sumit");
        {
            Predicate<String> predicate = (String name) -> name.equals(name.toUpperCase());
            System.out.println(predicate.test("Sumit"));
        }
        System.out.println("#Check if all characters are in upper case. If yes check if length is 5. Input - SUMIT");
        {
            Predicate<String> upper = (String name) -> name.equals(name.toUpperCase());
            Predicate<String> length = (String name) -> name.length() == 5;
            Predicate<String> predicate = upper.and(length);
            System.out.println(predicate.test("SUMIT"));
        }
        System.out.println("#Print message when called.");
        {
            Consumer<String> consumer = (String name) -> System.out.println("Hello");
            consumer.accept("Sumit");
        }
        System.out.println("String List to integer list: " + NUMBERS);
        {
            List<Integer> integers = NUMBERS.stream().map(Integer::parseInt).collect(Collectors.toList());
            System.out.println(integers);
        }
        System.out.println("String List to uppercase + # list: " + CITIES);
        {
            List<String> upper = CITIES.stream().map(city -> city.toUpperCase() + "#").collect(Collectors.toList());
            System.out.println(upper);
        }

        System.out.println("String List to distinct + # list: " + CITIES);
        {
            List<String> distinct = CITIES.stream().distinct().collect(Collectors.toList());
            System.out.println(distinct);
        }
        System.out.println("Get 2 elements from list" + CITIES);
        {
            List<String> limit = CITIES.stream().limit(2).collect(Collectors.toList());
            System.out.println(limit);
        }

        System.out.println("Get all elements from list except twot" + CITIES);
        {
            List<String> limit = CITIES.stream().skip(2).collect(Collectors.toList());
            System.out.println(limit);
        }

        System.out.println("Check if all cities starts with M" + CITIES);
        {
            System.out.println(CITIES.stream().allMatch(city -> city.startsWith("M")));
        }

        System.out.println("Check if any cities starts with M" + CITIES);
        {
            System.out.println(CITIES.stream().anyMatch(city -> city.startsWith("M")));
        }
        
        System.out.println("Employee(id, List<String(name)>) => Find all distinct subjects");
        {
            Employee employee = new Employee();
            employee.subjects = Arrays.asList("English", "Maths");

            Employee employee2 = new Employee();
            employee2.subjects = Arrays.asList("Hindi", "Maths");
            List<Employee> employees = Arrays.asList(employee, employee2);
            List<String> subjects = employees.stream().map(emp -> emp.subjects).flatMap(sub -> sub.stream()).distinct().collect(Collectors.toList());
            System.out.println(subjects);
        }
    }

    private static class Employee{
        public List<String> subjects = new ArrayList();
    }
}
```