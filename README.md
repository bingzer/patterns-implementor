# patterns-implementor
Simple patterns that forces the uses of `Interfaces` rather than concrete classes.
Given:
```
public interface Shape { ... }
public interface Rectangle extends Shape { ... }
public interface Circle extends Shape { ... }
```
Implementations:
```
/* package */ class RectangleImpl implements Rectangle { ... }
/* package */ class CircelImpl implements Circle { ... }
```
Create the implementor:
```
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
...
```
Then use it
```
ShapeFactory factory = new ShapeFactory();
Circle circle = factory.getImplementation(Circle.class);
```

# Gradle
``` groovy
dependencies {
    compile 'com.bingzer.android.patterns:implementor:1.0.0'
}
```
