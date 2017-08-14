## Swoole server

### Common problems

#### Four types of callback functions

`Closure`
```php
$server->on('request', function($request, $response){
	echo "hello world\n";
});
```

`Static method`
```php
class A
{
	static function test($request, $response)
	{
		echo "hello world\n";
	}
}
$server->on('request', 'A::test');
$server->on('request', array('A', 'test'));
```

`Function`
```php
function my_onResquest($request, $response)
{
	echo "hello world\n";
}
$server->on('request', "my_onResquest");
```

`Class method`
```php
class A
{
	function test($request, $response)
	{
		echo "hello world\n";
	}
}
$object = new A();
$server->on('request', array($object, 'test'));
```
