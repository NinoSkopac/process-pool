PHP Process Pool
================

[![Latest Version](https://img.shields.io/github/release/andersondanilo/process-pool.svg?style=flat-square)](https://github.com/andersondanilo/process-pool/releases)
[![Build Status](https://img.shields.io/travis/andersondanilo/process-pool.svg?style=flat-square)](https://travis-ci.org/andersondanilo/process-pool)

PHP Process Pool is a simple process pool using symfony process

```php
use ProcessPool\ProcessPool;
use Symfony\Component\Process\Process;

function processGenerator($count) {
    for ($i = 0; $i < $count; $i++) {
        yield new Process(['sleep', $i]);
    }
}

$processes = processGenerator(10);
$pool = new ProcessPool($processes);
$pool->setConcurrency(2);
$pool->wait();
```

# Getting output example
```php
$pool->onProcessFinished(function(ProcessFinished $processFinished) {
    print trim($processFinished->getProcess()->getOutput());
});
```
