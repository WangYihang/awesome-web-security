# 文件包含漏洞

#### 1. 典型代码案例

```
<?php
    $file = $_GET['file'];
    include($file);
    // require($file);
    // include_once($file);
    // require_once($file);
?>
```



