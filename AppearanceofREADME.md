# Requirements SplitBlock
- Language / C++ 10.0.5
- OS / macOS BigSur
- IDE / Xcode (推奨 ※Xcode以外では動作しない可能性大)
- File / SplitBlock.hpp (定義) , SplitBlock.cpp (実装)
- ClassName / SplitBlock
- AccessPermission / private , public

以下Classの全関数と全変数。構造について明記する。
各変数及び関数はもっと良い実装方法があると思うので、逐次変更予定。  
詳しい使い方や例は4.に網羅的に書こうと思います。

- [1.変数の説明](#anchor1)
- [2.関数の説明](#anchor2)
- [3.コンストラクタ、デストラクタの説明](#anchor3)
- [4.クラスの構造の説明](#anchor4)


<a id="anchor1"></a>
***
# 1.変数の説明　private:
変数の説明と主なアクセス方法の説明
## Vector2次元配列型 Pixel data;
実際の画像ファイルのデータをRGBで保存する。
Pixel構造体は
```cpp
      struct Pixel{
            double r;
            double g;
            double b;
                };
```
というdouble形の変数r,g,bを持っている。
このPixel型変数をvectorで2次元配列で表したもの。  
Vector型なのでサイズは自由

## string SplitNumber
文字列型の変数で、分割画像の位置を保存する。最大で00 ~ FF  
アクセス方法の例
```cpp
       a.getSplitNumber();
```
## string up , string bottom , string left , string right
分割画像の隣接画像の保存関数  
アクセス方法の例
```cpp
       a.getup();
       a.getbottom();
       a.getleft();
       a.getright();
```
隣接画像がない場合は"-1"で保存してあり、初期値も-1

## int upAP , int bottomAP , int leftAP , int rightAP
分割画像の隣接画像の類似度。0 - 100の範囲で示す予定  
アクセス方法の例
```cpp
       a.getupAP();
       a.getbottomAP();
       a.getleftAP();
       a.getrightAP();
```
類似度の判別は関数によって行うのが現実的だと思うが、方法は未定。

## int direction
分割画像の向き。0,1,2,3で0,90,180,270を表す。  
アクセス方法の例
```cpp
       a.getdirection();
```
初期値は当然0。

## bool completeRestore
分割画像の隣接画像の保存関数4つに値が入っているかどうかを示す関数。(true : false)で表す。  
アクセス方法の例
```cpp
       a.getcompleteRestore();
```
保存関数4つとはstring up , string bottom , string left , string rightのこと。

## int type
分割画像の種類を示す。　例（角 : 3, 辺 : 2, 内部 : 1)とかがいいかも。  
アクセス方法の例
```cpp
       a.gettype();
```

<a id="anchor2"></a>
***
# 2.関数の説明 public:

## void set~(~);
値を代入する用の関数。set+変数名。全変数分ある。

引数には代入したい値を入れる。

※使用例
```cpp
            a.setSplitNumber("FF")
            //aクラスの分割画像の位置をFFに変更
```   

## ~ get~();
値を参照するときに使う関数。set+変数名。全変数分ある。引数はなし。

return this->~ で戻り値で値を参照できる。

※使用例
```cpp
            a.setSplitNumber("FF")
            std::cout << a.getSplitNumber;
```
実行結果は

            FF
になる。


<a id="anchor3"></a>
***
# 3.コンストラクタ、デストラクタの説明
実際に実装している所
```cpp
            SplitBlock::SplitBlock(string SplitNumber,vector<vector<Pixel>> data){
                         this->data = data;
                         this->SplitNumber = SplitNumber;
                         this->up = "-1";
                         this->bottom = "-1";
                         this->left = "-1";
                         this->right = "-1";
                         this->upAP = 0;
                         this->bottomAP = 0;
                         this->leftAP = 0;
                         this->rightAP = 0;
                         this->direction = 0;
                         this->completeRestore = false;
                         this->type = 0;
            }
```
基本的に初期化しかしていない。dataとSplitNumberは不変なので組み込んでいるか、データの入力時に大変なので無くすと思う。

デストラクタは必要に応じて実装する。









<a id="anchor4"></a>
***
# 4.クラスの構造の説明
まず実際の使用方法としてはこのSplitBlockClassを2次元配列として扱う。
```cpp
      #include <iostream>
      #include <vector>
      #include "SplitBlock.hpp"

      using namespace std;

      int main(){
            vector<vector<SplitBlock>> _data();
      }
```
のように使用することが想定される。






`参考`
>https://siv3d.github.io/ja-jp/

>https://gist.github.com/mignonstyle/083c9e1651d7734f84c99b8cf49d57fa
