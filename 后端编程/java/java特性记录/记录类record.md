record:
```java
public record Point(int x, int y) {}
```

相当于：

```java
public final class Point extends Record {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int x() {
        return this.x;
    }

    public int y() {
        return this.y;
    }

    public String toString() {
        return String.format("Point[x=%s, y=%s]", x, y);
    }

    public boolean equals(Object o) {
        ...
    }
    public int hashCode() {
        ...
    }
}
```

注意：

1. 没有生成.getX()和.setX()方法，而是直接.x()
2. 成员变量只能通过构造声明
3. 不支持继承
