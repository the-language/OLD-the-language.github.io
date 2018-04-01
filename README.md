# 語

zaoqi

```racket
 #lang lang package: [lang](https://pkgs.racket-lang.org/package/lang)
```

## 1. 物

```racket
(等？ 甲 乙) -> 陰陽？
  甲 : 物？       
  乙 : 物？       
```

返回`甲`是否等於`乙`。

```racket
(首-尾？ 甲) -> 陰陽？
  甲 : 物？       
```

返回`甲`是否是`(首-尾 之首 之尾)`。

```racket
(首-尾 首 尾) -> 首尾？
  首 : 物？        
  尾 : 列？        
```

沒有強制類型限制。

```racket
(首-尾.首 甲) -> 物？
  甲 : 首-尾？     
```

若`甲`是`(首-尾 之首 之尾)`，返回`之首`。

```racket
(首-尾.尾 甲) -> 物？
  甲 : 首-尾？     
```

若`甲`是`(首-尾 之首 之尾)`，返回`之尾`。

```racket
(空？ 甲) -> 陰陽？
  甲 : 物？     
```

返回`甲`是否是`()`。

```racket
空 : 空？ = ()
```

```racket
列 : 機？ = [入 甲 甲]
```

```racket
(文？ 甲) -> 陰陽？
  甲 : 物？     
```

返回`甲`是否是字符。

```racket
(名/文？ 甲) -> 陰陽？
  甲 : 物？       
```

```racket
(名/文 列) -> 名-文？
  列 : (列 文？)   
```

沒有強制類型限制。

```racket
(名/文-1 甲) -> (列 文？)
  甲 : 名/文？         
```

```racket
(名/構？ 甲) -> 陰陽？
  甲 : 物？       
```

```racket
(名/構 名 列) -> 陰陽？
  名 : 名？        
  列 : 列？        
```

沒有強制類型限制。

```racket
(名/構.名 甲) -> 名？
  甲 : 名/構？     
```

```racket
(名/構.列 甲) -> 列？
  甲 : 名/構？     
```

```racket
(名？ 甲) -> 陰陽？
  甲 : 物？     
```

```racket
(映？ 甲) -> 陰陽？
  甲 : 物？     
```

```racket
映/空 : 映？
```

空映射。

```racket
(映.增 映 名 物) -> 映？
  映 : 映？         
  名 : 物？         
  物 : 物？         
```

```racket
(映.改 映 名 者) -> 映？
  映 : 映？         
  名 : 物？         
  者 : (-> 物？ 物？) 
```

```racket
(映.增-改 映 名 物) -> 映？
  映 : 映？           
  名 : 物？           
  物 : 物？           
```

返回創建或修改了的映射。

```racket
(映.取 映 名) -> 物？
  映 : 映？       
  名 : 物？       
```

```racket
(映.含？ 映 名) -> 陰陽？
  映 : 映？         
  名 : 物？         
```

```racket
(映.删 映 名) -> 映？
  映 : 映？       
  名 : 物？       
```

必須有

```racket
(映→列 映) -> (listof (cons/c any/c any/c))
  映 : 映？                                
```

```racket
(！式 甲 ...)
```

使用一個`引機？`。可以寫作`{甲 ...}`。

```racket
(機？ 甲) -> 陰陽？
  甲 : 物？     
```

```racket
(機 形 物) -> 機？
  形 : 物？     
  物 : 未算？    
```

```racket
(用 機 形) -> 物？
  機 : 機？     
  形 : 列？     
```

用`形`應用`機`。 `(算 (機.物 機) 境)`。 `境`只包含用`機.形`和`形`得到的。

```racket
(機.形 機) -> 物？
  機 : 機？     
```

類似Scheme。

```racket
(機.物 -機) -> 未算？
  -機 : 機？      
```

```racket
陰 : 陰陽？
```

```racket
陽 : 陰陽？
```

```racket
(若 甲 乙 丙) -> 物？
  甲 : 陰陽？      
  乙 : 物？       
  丙 : 物？       
```

若`甲`是`陽`，則返回`乙`，否則返回`丙`。

```racket
(引-機？ 甲) -> 陰陽？
  甲 : 物？       
```

```racket
(引-機 機) -> 引機？          
  機 : (-> 映？ 未算？ ... 物？)
```

沒有強制類型限制。 first-class的宏和特殊形式。

```racket
(引-機-1 甲) -> (-> 映？ 未算？ ... 物？)
  甲 : 引-機？                     
```

`引-機`的反函數。

```racket
引 : 引機？ = (引機 {入 (境 物) 物})
```

```racket
(誤？ 甲) -> 陰陽？
  甲 : 值？     
```

```racket
(誤 甲) -> 誤？
  甲 : 值？   
```

內置的函數可以產生`(誤 (構 (列→名 (列 [引 界] [引 誤] [引 -名])) -列))`。 `-名`是函數的名字。
`-列`一般是參數。

```racket
(誤-1 甲) -> 物？
  甲 : 誤？     
```

```racket
(算 未算 境) -> 物？
  未算 : 未算？    
  境 : 映？      
```

```racket
{境.命名-今 名 物}
```

把現在的環境命名爲`名`，返回`物`。

```racket
{境.改 新境 物}
```

```racket
境/空 : 映？
```

```racket
{命名 ((標識符 之物) ...) 物}
```

`letrec`

```racket
(構？ 甲) -> 陰陽？
  甲 : 物？     
```

返回`甲`是否是`(構 名 列)`。

```racket
(構 名 列) -> 構？
  名 : 名？     
  列 : 列？     
```

沒有強制類型限制。

```racket
(構.名 甲) -> 物？
  甲 : 構？     
```

若`甲`是`(構 名 列)`，返回`名`。

```racket
(構.列 甲) -> 物？
  甲 : 構？     
```

若`甲`是`(構 名 列)`，返回`列`。

```racket
(取 名) -> 物
  名 : 名？  
```

獲取一個包
