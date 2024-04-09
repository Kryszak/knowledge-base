## casting to primitive
```java
(int) (Integer) null
/// NullPointerException
```

## integer cache
```java
class Scratch {
    public static void main(String[] args) {
        Integer first = 100;
        Integer second = 100;

        System.out.println("First == second " + (first == second)); // true

        Integer third = 5000;
        Integer fourth = 5000;

        System.out.println("Third == fourth " + (third == fourth)); // false
    }
}
```

## ordered locking to avoid deadlocks
```kotlin
class Bank(private val balanceStore: HashTable<UUID, Balance>) {
   fun transfer(fromUserId: UUID, toUserId: UUID, amount: BigDecimal) {
        val (minId, maxId) = orderIds(fromUserId, toUserId)
        synchronized(balanceStore[minId] ?: throw RuntimeException()) {
            synchronized(balanceStore[maxId] ?: throw RuntimeException())) {
                balanceStore[fromUserId]?.decrementBy(amount)
                balanceStore[toUserId]?.incrementBy(amount)
            }
        }
   }

   private fun orderIds(fromUserId: UUID, toUserId: UUID): Pair<UUID, UUID> {
    return Pair(minOf(fromUserId, toUserId), maxOf(fromUserId, toUserId))
   }
}

class Balance(var amount: BigDecimal) {
    fun incrementBy(amount: BigDecimal) {
        this.amount += amount
    }

    fun decrementBy(amount: BigDecimal) {
        if (this.amount < amount) throw RuntimeException()
        this.amount -= amount
    }
}
```

## Grouping bs
```java
import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.Stack;

/*
W stringu możesz zadeklarować 3 rodzaje grup () [] {}
Grupy mogą się zagnieżdżać, ale muszą być odpowiednio zamknięte i otwarte
    poprawne:
    ()
    ([])
    ([]{})
    [({})()]
    niepoprawne:
    )
    )[]
    (])
    ({}])

Zaimplementuj metodę, która sprawdza czy podany string ma git grupy, testy już napisane
 */

class Solution {

    private static final Set<Character> groupOpenCharacters = Set.of('(', '[', '{');

    private static final Set<Character> groupCloseCharacters = Set.of(')', ']', '}');

    private static final Map<Character, Character> groups = Map.of(
            ')', '(',
            ']', '[',
            '}', '{'
    );

    public static void main(String[] args) {
        var correctlyGrouped = List.of(
                "()",
                "([])",
                "([]{})",
                "[({})()]"
        );
        var wronglyGrouped = List.of(
                ")",
                ")[]",
                "(])",
                "({}])"
        );

        System.out.println("Correct strings:");
        correctlyGrouped.forEach(s -> System.out.printf("%s : %s%n", s, isCorrectlyGrouped(s)));
        System.out.println();
        System.out.println("Wrong strings:");
        wronglyGrouped.forEach(s -> System.out.printf("%s : %s%n", s, isCorrectlyGrouped(s)));
    }

    private static boolean isCorrectlyGrouped(String testString) {
        var stack = new Stack<Character>();

        for (var character : testString.toCharArray()) {
            if (groupOpenCharacters.contains(character)) {
                stack.push(character);
            }
            if (groupCloseCharacters.contains(character)) {
                if (stack.isEmpty()) {
                    return false;
                }
                var previouslyOpen = stack.pop();
                if (!groups.get(character).equals(previouslyOpen)) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
