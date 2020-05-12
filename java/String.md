# String

* String被final修饰：不允许被继承，内部细节不允许被改变
* String创建后即不能修改


# StringBuffer

* 线程安全
* final类，不允许被继承
* 大多数方法进行了同步处理，包括常用的append等（synchronized）
* 其中toString方法进行对象缓存，减少元素复制开销
```
public synchronized String toString() {
	if (toStringCache == null) {
		toStringCache = Arrays.copyOfRange(value, 0, count);
	}
	return new String(toStringCache, true);
}
```

# StringBuilder

* 非线程安全
* 方法除了没用synchronized，与StringBuffer均类似
* 其中toString方法直接返回一个新对象
```
public String toString() {
	// Create a copy, don’t share the array
	return new String(value, 0, count);
}
```