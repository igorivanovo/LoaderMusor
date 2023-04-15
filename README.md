# LoaderMusor
```java
   public class JvmComprehension {   //  Application ClassLoader берёт class JvmComprehension и загружает данные о нём в Metaspace
                                     // (имя, методы, поля и др.),константы - далее управление на
                                     // Platform ClassLoader, Bootstrap ClassLoader и ищут упомянутые данные по очереди и в обратном порядке 

    public static void main(String[] args) {      // работа с main - создаётся его фрейм в Stack Memory
        int i = 1;                      // 1      Stack Memory int i = 1;
        Object o = new Object();        // 2      heap (куча)Object, new возврат адресса - в Stack Memory создаётся o и записывается ссылка
        Integer ii = 2;                 // 3      heap (куча)Integer 2, new - в Stack Memory создаётся ii и записывается ссылка
        printAll(o, i, ii);             // 4      создаётся ещё фрейм printAll над main c созданными переменными
        System.out.println("finished"); // 7      новый фрейм println, печатает и завершается и метод main и фрейм завершается. всё забирается сборщиком мусора
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5   heap (куча)Integer 700, new - в Stack Memory создаётся  uselessVar и записывается ссылка
        System.out.println(o.toString() + i + ii);  // 6  новый фрейм toString , считается выражение , закрывается и фрейм println , печатается и закрывается
                                                    // Integer 700 теряет ссылку и может быть удален
    }
}

