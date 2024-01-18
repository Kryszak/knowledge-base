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
