# Is volatile necessary in Singleton Pattern?

## Overall

In this article will discuss the following topics:

1. what is volatile?
2. what is singleton Pattern?
3. How does DCL plays a role in singleton pattern?
4. how does a class initializes itself?
5. What is inner static class?



## 1. What is volatile?

volatile is a keyword in Java, usually it has two abilities: guarantees visibility and prevents instruction reordering.

guarantees visibility means the threads would not keep a copy of the value in each's memory, but read the value only from the main memory. So when a thread try to change the value, the others would know.

volatile prevents instruction reordering, ensuring that the read always happens after write. For example, suppose thread A wants to initialize a volatile value V with an instance of  Class C. In JVM this action is split into 3 steps. first allocate memory, then initialize object C, finally set V to the reference of the object. Without volatile, step3 could be executed before step2. This could cause error in a multithreaded situation. thread B maybe read a not fully initialized object, even it adds a null check.

## 2.What is singleton Pattern?

Singleton Pattern ensures that some specific classes only has one instance in all project and global access. Such as logger, configuration. To these classes , one instance is always enough and best.

But usually, when multithreads use one singleton pattern class, it cause the error in topic one.

## 3.How does DCL plays a role in singleton pattern?

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {                  // first check
            synchronized (Singleton.class) {	//get locker
                if (instance == null) {          // second check
                    instance = new Singleton(); 
                }
            }
        }
        return instance;
    }
}

```

DCL always looks like this. The first check help return the instance quickly,and the second check ensures only one instance would be initialized after one thread get locker. With Volatile it can good work.

