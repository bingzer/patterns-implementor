# patterns-implementor
Simple patterns that forces the uses of `Interfaces` rather than concrete classes.
Given:
``` java
public interface Shape { ... }
public interface Rectangle extends Shape { ... }
public interface Circle extends Shape { ... }
```
Implementations:
``` java
/* package */ class RectangleImpl implements Rectangle { ... }
/* package */ class CircelImpl implements Circle { ... }
```
Create the implementor:
``` java
public class ShapeFactory extends ImplementorFactory<Shape> { 
  public ShapeFactory() throws ImplementorException {
    addImplementation(CircleImpl.class);
    addImplementation(RectangleImpl.class);
  }
  
  @Override
  protected <E extends Shape> E newInstance(Class<E> clazz) throws InstantiationException, IllegalAccessException {
    return clazz.newInstance();
  }
}
```
Then use it
``` java
...
ShapeFactory factory = new ShapeFactory();

Circle circle = factory.getImplementation(Circle.class);
// circle is CircleImpl.class

Rectangle rect = factory.getImplementation(Rectangle.class);
// rect is RectangleImpl.class
...
```

# Gradle
``` groovy
dependencies {
    compile 'com.bingzer.android.patterns:implementor:1.0.0'
}
```
