## Debugging PHP

I am trying to understand why a PDO operation is silently failing.

```
ob_start();
$stmt->debugDumpParams();
$r = ob_get_contents();
ob_end_clean();
$this->oLogger->Write($r);
```

Everytime I debug PHP, I die a little inside.
