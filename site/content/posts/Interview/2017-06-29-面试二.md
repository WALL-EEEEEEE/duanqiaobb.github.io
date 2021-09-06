- [面试的公司](#org2517451)
- [面试中体现的问题](#org8de2e65)
- [解决和提升的方法](#orgd2bbb1c)
- [面试官问的问题](#org01000b8)
  - [PHP基础题1：](#orgb6f266c)
  - [PHP基础题2:](#orge971d76)
  - [PHP基础题3:](#orge20b334)
  - [PHP基础题4：](#org49af6d8)

第二次面试的公司是一家游戏公司，总公司在上海，公司的办公室在酒店里，挺不错的。我对这家公司比较满意，同时也很希望进入这家公司。进入公司后，首先是在人事妹子那拿了份面试题和面试需要填写的资料填了。 面试题都是十分简单的PHP题目，但是由于几乎我半年没碰PHP了，我答得十分不好（作为一个写了两年PHP的我，羞愧捂脸）。


<a id="org2517451"></a>

# 面试的公司

上海邑世游戏公司


<a id="org8de2e65"></a>

# 面试中体现的问题

-   基础知识不足


<a id="orgd2bbb1c"></a>

# 解决和提升的方法

-   过一下基础知识，同时兼顾刷下常见的面试题目


<a id="org01000b8"></a>

# 面试官问的问题

面试我的是一个比较年轻的哥们，比较实在,问的问题都是根据做的面试题来的。


<a id="orgb6f266c"></a>

## PHP基础题1：

```php
$a = 10;
$b = &a;
++a;
unset($a);
echo $b;
```

```example
11
```

这里考到了PHP中的引用，和unset函数对引用操作的问题。首先需要明白,PHP中的引用并不等价与C中的指针 `unset` 函数对引用的操作仅仅是断开了引用和值之间的联系，这并不意味这变量中的内容被销毁了。所以题 中的变量 `a` 的内容经过 `unset` 操作并没有被销毁。所以 `$b` 的值为 `11` 。


<a id="orge971d76"></a>

## PHP基础题2:

假设从数据库中读取总共有 `$total` 条记录， 每一页有 \(perpage\) 条记录，请问总共要分多少页？

```php
$pages =
```

这道题考的是简单的分页计算，答案是:

```php
$pages = $total%$perpage == 0 ? (int)($total/$perpage):(int)($total/$perpage+1);
```


<a id="orge20b334"></a>

## PHP基础题3:

通过给定的年份和月份，计算出该年该月的最后一天的日期。

```php
function DateofYearMonth($year,$month){
  $date = 
  return $date;
}
```

这道题主要考的PHP对日期的操作，可以使用 `date` 和 `strtotime` 函数来实现，思路是

-   首先得到该年该月的第一天
-   然后将上面的结果加上一个月，再减去一天得到该年该月的最后一天的日期

```php
function DateofYearMonth($year,$month) {
  $firstdate = date("Y-m-01",strtotime("$year-$month"));
  return date('Y-m-d',strtotime("$firstdate+1 month - 1 day"));
}
```


<a id="org49af6d8"></a>

## PHP基础题4：

匹配并输出以下字符串中的所有数字， `'Abc_37_jk_3'`

该题主要是考了PHP中的正则表达式的知识。

```php
```
