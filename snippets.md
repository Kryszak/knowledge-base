```
(int) (Integer) null
/// NullPointerException
```

```
class Scratch {
    public static void main(String[] args) {
        Integer first = 100;
        Integer second = 100;

        System.out.println("First == second " + (first == second)); // true

        Integer third = 5000;
        Integer fourth = 5000;

        System.out.println("First == second " + (third == fourth)); // false
    }
}
```
