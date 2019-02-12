# PHP・Python・Ruby書き方簡易まとめ

## 変数
### PHP
```php
$varaible
```
### Python
```python
variable
```
### Ruby
* 素の変数
    ```ruby
    variable
    ```
* クラス変数
    ```ruby
    @@classVariable
    ```
* インスタンス変数
    ```ruby
    @instanceVariable
    ```


## コメントアウト
### PHP
```php
// 一行コメント

/*
複数行コメント
*/
```
### Python
```python
# コメント
```
### Ruby
```ruby
# 一行コメント

=begin
複数行コメント
=end
```

## 文字列の結合
### PHP
```php
'A'.'B' // .で結合

$str1 = 'A';
$str2 = 'B';
$str = $str1 . $str2 // 変数の場合も同様。.の前後に半角スペースがあっても良い
```
### Python
```python
'A' + 'B'  # 基本は結合演算子 + を使う
s = 'A''B''C'  # 変数ではないナマの文字列だと + 不要。\による改行も無視される
s = 'A' + 1  # これはだめ。型が違うやつはエラーになる
s = 'A' + '1'  # これはおｋ
```
[こっち](https://note.nkmk.me/python-string-concat/)も参照
### Ruby
```ruby
```


## 関数の定義と呼び出し
### PHP
```php
function functionName($varaiables){
    ...
}

// 呼び出し
functionName(values)
```
### Python
```python
def functionName(varaiables, defaultVaraibles = defValue)
    ...  # 必ず字下げが必要（Pythonでは字下げが意味を持つ）

# 呼び出し
functionName(values [, values])
```
デフォルト値`defValue`を持つデフォルト引数(`defaultVarialbes`)を設定可能。
* デフォルト引数は通常の引数よりも後ろに置くこと。
* 関数呼び出し時に省略可能だが、値を指定するとそちらが使用される。

例：
```python
def summation(i, f, p = 1)
    tot = 0
    for(int j = i; j <= f; j++)
        tot += j ** p # j^p

summation(1, 10)
# 55
```
### Ruby
```ruby
def functionName(variables)
    ...
end

# 呼び出し
functionName(values)
```


## クラスについての諸々
クラスの定義と継承、コンストラクタ、メソッド、インスタンス化などなど
### PHP
```php
Class ClassName Extends ParentClassName {
    // コンストラクタ
    function __construct($constructerVariables){
        ...
    }
    
    // メソッド
    function methodName($variables){
        ...
    }
}

// インスタンス化
$instance = new ClassName(constructerVariables);

// インスタンスの変数のsetとget
$instance->instanceVariableName = setValue; // set
$instance->instanceVariableName // get
```
### Python
```python
class ClassName(ParentClassName):
    # コンストラクタ
    def __init__(self, contructerVariables):  # インスタンス自信を指すselfは必須！
        ...
    
    # メソッド
    def methodName(self, variables):  # やはりselfは必須
        ...

# 字下げがなくなった地点で「クラスの定義が終了した」と自動的に認識される

# インスタンス化
instance = ClassName(constructerVariables)

# メソッドの使用
instance.methodName(variables)
```
### Ruby
```ruby
class ClassName < ParentClassName
    # クラス変数
    @@classVariable # このクラスから作られた全てのインスタンスで共通

    # 定数
    Constant = 1
        # 一度定義すると変更できない
        # 定数の名前は必ず大文字から
        # メソッド内では定義できない
        # 参照はClassName::Constant

    # コンストラクタ（Rubyではinitializeメソッドと呼称）
    def initialize(constructerVariables)
        ... 
    end

    # メソッド
    def methodName(methodVariables)
        @instanceVariable # インスタンスごとに独立
    end
end

# インスタンス化
instance = ClassName.new(constructerVariables)

# メソッドの使用
instance.methodName(methodVaraibles)

# ↑と等価
instance::methodName(methodVariables)
```

クラス変数とインスタンス変数の例：
```ruby
class Character
    @@numchara = 0

    def initialize(charaname = "")
        @name = charaname
        @@numchara += 1
    end

    def getName()
        return @name
    end

    def getCount()
        return @@numchara
    end
end

hero = Character.new("Hero") # ここで @@numchara = 1 に
warrior = Character.new("Warrior") # ここで @@numchara = 2 に
magician = Character.new("Magician") # ここで @@numchara = 3 に
monk = Character.new("Monk") # ここで @@numchara = 4 に

print("パーティーの人数は", hero.getCount(), "人です")
# パーティーの人数は4人です  ←heroインスタンスから取得したにもかかわらず、ちゃんと「4人」を返せる
print(hero.getName())
# Hero
print(warrior.getName())
# Warrior
```


