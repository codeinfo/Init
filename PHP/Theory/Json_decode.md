[Json_decode](http://cn2.php.net/json_decode)
---
### 说明
	mixed json_decode ( string $json [, bool $assoc = false [, int $depth = 512 [, int $options = 0 ]]] )
### 参数
#### json
  待解码的 json string 格式的字符串。
  This function only works with UTF-8 encoded data.
#### assoc
当该参数为 TRUE 时，将返回 array 而非 object 。
#### depth 递归深度
User specified recursion depth.
#### options
Bitmask of JSON decode options. Currently only JSON_BIGINT_AS_STRING is supported (default is to cast large integers as floats)

### int 
	<?php
	 $json = '12345678901234567890';
	 var_dump(json_decode($json));
	 var_dump(json_decode($json, false, 512, JSON_BIGINT_AS_STRING));
	?> 
