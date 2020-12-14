---
title: BoostCake
author: PipisCrew
date: 2015-04-20
categories: []
toc: true
---

Is a plugin for CakePHP using Bootstrap..

[http://slywalker.github.io/cakephp-plugin-boost_cake/](http://slywalker.github.io/cakephp-plugin-boost_cake/)

or

[http://github.com/slywalker/cakephp-plugin-boost_cake](http://github.com/slywalker/cakephp-plugin-boost_cake)

* * *

> How to Run custom sql query in CakePHP 3.0

source - [http://agalaxycode.blogspot.in/2015/04/run-custom-sql-query-in-cakephp-30.html](http://agalaxycode.blogspot.in/2015/04/run-custom-sql-query-in-cakephp-30.html)

```js
//File : src\Model\Table\ArticlesTable.php
<?php namespace="" app\model\table;="" use="" cake\orm\table;="" use="" cake\datasource\connectionmanager;="" class="" articlestable="" extends="" table="" {="" var="" $conn;="" public="" function="" initialize(array="" $config)="" {="" $this-=""?>conn = ConnectionManager::get('default');
    }
    function get_all_users($id) {
        $stmt = $this->conn->prepare('SELECT * from users WHERE id>= :id');
        $stmt->bind( ['id' => $id], ['id' => 'integer']);
        $stmt->execute();
        return $stmt->fetchAll('assoc');
     }  
}
?>

//File: src\Controller\ArticlesController.php 
<?php namespace="" app\controller;="" use="" cake\core\configure;="" use="" cake\network\exception\notfoundexception;="" use="" cake\view\exception\missingtemplateexception;="" use="" cake\orm\tableregistry;="" use="" cake\datasource\connectionmanager;="" use="" myclass\myclass;="" use="" mylib\utilclass;="" class="" articlescontroller="" extends="" appcontroller="" {="" public="" $helpers="array('Html'," 'form');="" public="" function="" index()="" {="" }="" public="" function="" showarticles(){="" $data="$this-"?>Articles->get_all_users(3);
         $this->set('data',$data);
    }
}

//File: src\Template\Articles\showarticles.ctp
<?php foreach="" ($data="" as="" $row){="" echo=""?>  
'.$row['username']. '-------' . $row['password'];
         }
?>
```

origin - http://www.pipiscrew.com/?p=2353 php-boostcake