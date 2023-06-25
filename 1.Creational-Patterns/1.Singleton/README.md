# Singleton Pattern

## Basic Singleon


```java
public class Singleton {
    private static Singleton INSTANCE;
    private Singleton(){
    }
    public static Singleton getInstance() {
        if (INSTANCE == null ) {
            INSTANCE = new Singleton();
        }
        return INSTANCE;
    }
}

```
### Notes
- Doesn't work in a Multithreaded Environment

## Adding Synchronized

```java
public class Singleton {
    private static Singleton INSTANCE;
    private Singleton(){
    }
    public static synchronized Singleton getInstance() {
        if (INSTANCE == null ) {
            INSTANCE = new Singleton();
        }
        return INSTANCE;
    }
}
```

### Notes
- Solves the multithreading problem
- Not very optimized , everytime getInstance() it waits for the previous thread to finish.
- Slow

## 2-Step Check / Double checked locking


```java
public class Singleton {
    private static Singleton INSTANCE;
    private Singleton(){
    }
    public static Singleton getInstance() {
        if (INSTANCE == null ) {
            synchronized (Singleton.class) {
                if(INSTANCE == null) {
                    INSTANCE = new Singleton();
                }
            }
        }
        return INSTANCE;
    }
}
```
### Notes
- Solves the multithreading problem
- optimized so that only first call to getInstance() hits the synchronized block.
- Solves the problem

## Nested Class

```java
public class NestedSingleton {
    private NestedSingleton(){
    }
    private static final class SingletonHolder {
        private static final NestedSingleton INSTANCE = new NestedSingleton();
    }
    public static NestedSingleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```
### Notes
- JVM loads the class and it loads it executes all the static blocks thus initializing the singleton instance (NestedSingleton)
- When getInstance() is called it simply returns the Instance .
- Since this Singleton implementation is natively implemented byJVM. It is the fastest.


