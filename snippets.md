## casting to primitive
```java
(int) (Integer) null
/// NullPointerException
```

## string pool
```java
public class Main
{
	public static void main(String[] args) {
		var first = new String("test");
		var second = new String("test");
		System.out.println(first == second); // false
		
		var third = "test";
		var fourth = "test";
		System.out.println(third == fourth); // true
	}
}
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

```java
class Bank {

    private final Map<UUID, Balance> balanceStore;

    public Bank(Hashtable<UUID, Balance> balanceStore) {
        this.balanceStore = balanceStore;
    }

    public void transfer(UUID fromUserId, UUID toUserId, BigDecimal amount) {
        UUID minId = fromUserId.compareTo(toUserId) < 0 ? fromUserId : toUserId;
        UUID maxId = fromUserId.compareTo(toUserId) < 0 ? toUserId : fromUserId;

        Balance minLock = balanceStore.get(minId);
        if (minLock == null) throw new RuntimeException();

        synchronized (minLock) {
            Balance maxLock = balanceStore.get(maxId);
            if (maxLock == null) throw new RuntimeException();

            synchronized (maxLock) {
                Balance from = balanceStore.get(fromUserId);
                Balance to = balanceStore.get(toUserId);

                if (from != null) from.decrementBy(amount);
                if (to != null) to.incrementBy(amount);
            }
        }
    }
}

class Balance {

    private BigDecimal amount;

    public Balance(BigDecimal amount) {
        this.amount = amount;
    }

    public synchronized void incrementBy(BigDecimal amount) {
        this.amount = this.amount.add(amount);
    }

    public synchronized void decrementBy(BigDecimal amount) {
        if (this.amount.compareTo(amount) < 0) {
            throw new RuntimeException();
        }
        this.amount = this.amount.subtract(amount);
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
String may contain 3 types of groups: () [] {}
Groups can be nested, but needs to be correctly opened and closed

Examples of correct grouping:
    ()
    ([])
    ([]{})
    [({})()]

Examples of incorrect grouping:
    )
    )[]
    (])
    ({}])

Implement method to check if provided string contains only correct groups
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
