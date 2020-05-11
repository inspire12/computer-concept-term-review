# Top 10 Easy Performance Optimisations in Java

# Big O Notation

## Use StringBuilder 

## Avoid regular expressions 

## Do not use iterator()
 iterator instance 를 생성함 
 
## Don't call that method 
 - ResultSet

## Use primitives and stack 
// Goes to the heap
 Integer i = 817598;

// Stays on the stack
 int i = 817598;

## Avoid recursion 
 
## Use entrySet() 
 When you want to iterate through a Map, 
```$xslt
for (K key : map.keySet()) {
    V value : map.get(key);
}
```
```$xslt
for (Entry<K, V> entry : map.entrySet()) {
    K key = entry.getKey();
    V value = entry.getValue();
}
```

## Use EnumSet or EnumMap 
```$xslt
private transient Object[] vals;
public V put(K key, V value) {
    // ...
    int index = key.ordinal();
    vals[index] = maskNull(value);
    // ...
}
```

## Optimise your hashCode() and equals() methods
If you cannot use an EnumMap, at least optimise your hashCode() and equals() methods.

## Think in sets, not in individual elements




* Reference 
[Top 10 Easy Performance Optimisations in Java](https://blog.jooq.org/2015/02/05/top-10-easy-performance-optimisations-in-java/)