For a completely stateless utility class in Java, I suggest the class be declared `public` and `final`, and have a private constructor to prevent instantiation. The `final` keyword prevents sub-classing and can improve efficiency at runtime.

The class should contain all `static` methods and should not be declared `abstract` (as that would imply the class is not concrete and has to be implemented in some way).

The class should be given a name that corresponds to its set of provided utilities (or "Util" if the class is to provide a wide range of uncategorized utilities).

The class should not contain a nested class unless the nested class is to be a utility class as well (though this practice is potentially complex and hurts readability).

Methods in the class should have appropriate names.

Methods only used by the class itself should be private.

The class should not have any non-final/non-static class fields.

The class can also be statically imported by other classes to improve code readability (this depends on the complexity of the project however).

Example:

```java
public final class ExampleUtilities {
    // Example Utility method
    public static int foo(int i, int j) {
        int val;

        //Do stuff

        return val;
    }

    // Example Utility method overloaded
    public static float foo(float i, float j) {
        float val;

        //Do stuff

        return val;
    }

    // Example Utility method calling private method
    public static long bar(int p) {
        return hid(p) * hid(p);
    }

    // Example private method
    private static long hid(int i) {
        return i * 2 + 1;
    }
}
```

Perhaps most importantly of all, the documentation for each method should be precise and descriptive. Chances are methods from this class will be used very often and its good to have high quality documentation to complement the code.