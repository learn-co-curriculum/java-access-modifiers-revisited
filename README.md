# Access Modifiers Revisited

## Learning Goals

- Review Access Modifiers
- Differentiate between encapsulation and data hiding

## Access Modifiers 

Recall that an **access modifier** in Java
controls the visibility of a class, field, constructor, or method.
When an access modifier is not specified, the visibility defaults
to the `package` level.


| Modifier        | Class | Package  | Subclass In<br>Another Package  | World |
|-----------------|-------|----------|---------------------------------|-------|
| public          | Y     | Y        | Y                               | Y     | 
| protected       | Y     | Y        | Y                               | N     | 
| default/package | Y     | Y        | N                               | N     | 
| private         | Y     | N        | N                               | N     | 


### Encapsulation vs Data Hiding

**Encapsulation** is a technique of wrapping the data (variables)
and the code to access and modify the data (methods) together as a single unit
defined in a Java class.

For example, the `Dog` class encapsulates the data about each dog
in the instance variables and provides methods that model
the behavior of a dog to access and modify the data.

```java
public class Dog {
    private String name;
    private int weight;
    private boolean isWaggingTail;
    private boolean likesBaths;

    public void giveTreat() {
        isWaggingTail = true;
        weight++;
    }

    public void giveBath() {
        isWaggingTail = likesBaths;
    }

    @Override
    public String toString() {
        return "name='" + name + '\'' +
                ", weight=" + weight +
                ", isWaggingTail=" + isWaggingTail +
                ", likesBaths=" + likesBaths;
    }
}
```

**Data hiding** is a separate concept that is often
associated with encapsulation. Data hiding is important
when we develop applications that involve multiple classes.
Instance variables are hidden from other classes by declaring them `private`.
We provide `public` methods  to access
and modify the values stored in the variables.

For example, the `Product` class declares private
instance variables and public getter/setter methods:


```java
public class Product {
    private String name;
    private double price;
    private int quantity;

    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {return name;}

    public double getPrice() {return price;}

    public int getQuantity() {return quantity;}

    public void setName(String name) {this.name = name;}

    public void setPrice(double price) {this.price = price;}

    public void setQuantity(int quantity) {this.quantity = quantity;}

    @Override
    public String toString() {
        return "name='" + name + '\'' +
                ", price=" + price +
                ", quantity=" + quantity;
    }
}
```

The `ProductDriver` class can't directly access the private instance variable `name`
of the `Product` class. Thus, the conditional statement in the `lookupProduct`
method must call the public `getName()` method to retrieve the value.


```java
import java.util.Scanner;

public class ProductDriver {

    ...
    
    //helper method to search array for Product with matching name
    public static Product lookupProduct(Product[] products, String searchName) {
        // Loop through array
        for (Product product : products) {
            // Compare next array element's name with the parameter
            if (product.getName().equals(searchName)) {
                return product;
            }
        }
        // No product with matching name in the array, return null.
        return null;
    }
}

```

If we tried to change the conditional statement to directly
access the private `name` instance variable, the compiler
would warn us that we have an error in the code:

```java
if (product.name.equals(searchName)) {
```

![compiler_error_privateaccess](https://curriculum-content.s3.amazonaws.com/6676/java-multipleclasses/privatecompilererror.png)


## Conclusion

To follow standard practices of data hiding, we will declare instance variables
as `private`, and provide `public` methods to access and modify the variables.

## Resources

[Controlling access to a member of a class](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html)