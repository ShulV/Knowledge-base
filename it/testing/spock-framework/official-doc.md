
### Подпись не только у самого метода, но и у логических блоков
```groovy
given: "open a database connection" // code goes here 
and: "seed the customer table" // code goes here 
and: "seed the product table" // code goes here
```

> **and** помогает описывать разные части одного блока


### Вынесение логики в отдельный метод:

#### helper method
```groovy
def "offered PC matches preferred configuration"() { 
	when: 
	def pc = shop.buyPc() 
	
	then: 
	matchesPreferredConfiguration(pc) 
} 

def matchesPreferredConfiguration(pc) { 
	pc.vendor == "Sunny" 
	&& pc.clockRate >= 2333 
	&& pc.ram >= 4096 
	&& pc.os == "Linux" 
}
```


####  assert выражение
Можно красивее:
```groovy
void matchesPreferredConfiguration(pc) { 
	assert pc.vendor == "Sunny" 
	assert pc.clockRate >= 2333 
	assert pc.ram >= 4096 
	assert pc.os == "Linux" 
}
```

#### verifyAll()
А можно заюзать конструкцию:
```groovy
def "offered PC matches preferred configuration"() { 
	when: 
	def pc = shop.buyPc() 
	
	then: 
	verifyAll(pc) { 
		vendor == "Sunny" 
		clockRate >= 2333 
		ram >= 406 
		os == "Linux" 
	} 
}
```

### with выражение

можно не писать название объекта, на котором были вызваны методы, а указать его в with:
```groovy
def service = Mock(Service) // has start(), stop(), and doWork() methods 
def app = new Application(service) // controls the lifecycle of the service

when:
app.run() 

then: with(service) { 
	1 * start() 
	1 * doWork() 
	1 * stop() }
```


### Директивы
|               |                                                                                                                                                                                                                                                                                                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `@Timeout`    | Sets a timeout for execution of a feature or fixture method.                                                                                                                                                                                                                                                                                                       |
| `@Ignore`     | Ignores any feature method carrying this annotation.                                                                                                                                                                                                                                                                                                               |
| `@IgnoreRest` | Any feature method carrying this annotation will be executed, all others will be ignored. Useful for quickly running just a single method.                                                                                                                                                                                                                         |
| `@FailsWith`  | Expects a feature method to complete abruptly. `@FailsWith` has two use cases: First, to document known bugs that cannot be resolved immediately. Second, to replace exception conditions in certain corner cases where the latter cannot be used (like specifying the behavior of exception conditions). In all other cases, exception conditions are preferable. |
| `@Retry`      |                                                                                                                                                                                                                                                                                                                                                                    |
| ...           |                                                                                                                                                                                                                                                                                                                                                                    |

### Сравнение с JUnit
|Spock|JUnit|
|---|---|
|Specification|Test class|
|`setup()`|`@Before`|
|`cleanup()`|`@After`|
|`setupSpec()`|`@BeforeClass`|
|`cleanupSpec()`|`@AfterClass`|
|Feature|Test|
|Feature method|Test method|
|Data-driven feature|Theory|
|Condition|Assertion|
|Exception condition|`@Test(expected=…​)`|
|Interaction|Mock expectation (e.g. in Mockito)|
