# 第二章 基本語法

本章說明 C 語言的基本程式架構、輸入輸出、變數的宣告和使用以及各種基本運算。

## 2-1 程式架構

一個最基本的 C 語言程式，長得大概像這樣：

```c=
#include <stdio.h>

int main()
{
    printf("Hello World!");
    return 0;
}
```

執行後輸出結果如下：

```
Hello World!
```

我們接著來解釋一下這個程式的內容。

第 1 列，#include 這個詞，主要用來指示：在程式檔中引入一個標頭檔 (header file)。在 C 語言裡面，以 # 開頭的指令，都由前置處理器 (pre-processor) 處理。所謂的前置處理，指的是在程式編譯之前，先對程式檔進行一些處理，處理完後才交給編譯器翻譯成機器碼。什麼事要在編譯前處理呢？例如引入標頭檔案、巨集展開、條件編譯等，這些內容現在不了解沒關係，以後慢慢學習就會越來越清楚。

那什麼是標頭檔呢？標頭檔其實也是一個檔案，裡面放的通常都是一些函數或變數的宣告，以及巨集的定義等，這些內容在往後的章節會陸續介紹。那麼這邊使用 <> 括號來括住這個標頭檔，我們可以把 <> 稱為角括號。角括號裡面的檔案，一般是指編譯系統提供的檔案，會到編譯系統的安裝目錄裡面去尋找，找到後把它引進這個檔案裡。

這裡引入的檔案是 stdio.h。std 是 standard 的縮寫，就是標準的意思，io 則是 input/output，也就是輸入和輸出的縮寫，最後的 .h 是標頭檔專用的副檔名，用來表示這個檔案是 C 的標頭檔。所以這一列的目的，主要是引入 stdio.h 這個檔案，其中會把標準輸入和標準輸出的一些相關函數、巨集等宣告引入進來。例如在這個程式中，我們所用到的輸出函數 printf，就是在 stdio.h 裡面宣告的。如果我們把這一列拿掉，編譯的時候，就會產生錯誤，內容大概是 "printf not declared" 之類的，也就是說，printf 這個函數沒有宣告的意思。有了這一個標頭檔，編譯器就能理解 printf 這個函數，以及它的使用方式。

第 2 列是空白列，基本上沒有什麼特別的意義，就算沒有這一列也沒有關係。在 C 語言裡面，只要符合語法規則，可以在程式碼中任意加上空白，而不會影響程式碼的執行結果。一般我們在寫程式的時候，都會把程式碼依流程架構做適當的排版，使得程式碼看起更加清爽而容易理解。這其中也有許多不同的排格風格，有興趣的讀者可以自行上網查詢，做進一步的了解。

第 3 列到第 7 列是 main 函數，也是 C 程式規定的執行進入點。基本上 C 程式由一個或更多的函數構成，如果要產生出一個完整的應用程式，一定要有 main 函數。main 前面的 int，是說這個函數執行完之後，會得到一個整數值，這邊 int 就是整數 (integer) 的意思。main 後面的括號，是用來指明函數所需的輸入參數，現在括號裡面是空白，說明目前不需要使用到任何傳入的參數，這種情形也可以在括號中加上 void，void 是空的意思，也就是沒有參數的意思。一般來說，函數是可以傳入參數的，例如計算三角函數 sin 的值，可能必須給一個實數，而函數執行完之後，也會回傳一個實數。

第 4 列和第 7 列的大括號，用來括住函數的執行內容。一般在 C 程式裡面，用大括號括起來的，可以看成是一個程式區塊，函數就是用一個程式區塊來定義它的執行內容。

第 5 列使用了 printf 函數，這個函數是基本的標準輸出函數，可以把一些訊息輸出到螢幕上。printf 函數最基本的使用方式，就是給它一個字串當作參數，然後 printf 函數就會把這個字串輸出到螢幕上。這邊要輸出的是 "Hello World!" 這個字串，也是我們丟給 printf 函數的參數。基本上用兩個雙引號「" "」括起來的是字串，字串可以由零到任意多個字元構成。在第 5 列最後出現的是分號「;」。基本上，C 語言中每個指令的最後都要加上一個分號。

第 6 列是 return 指令，用來結束函數的執行流程，並且把執行結果設定為 0。在 return 指令之後，如果函數裡還有其他的指令，基本上都不會執行，因為碰到 return，函數的執行就結束了。那麼為什麼把執行結果設定為 0 呢？剛才提到第 3 列，main 函數前的 int，就是說明函數執行之後，必須回傳一個整數的結果，那實際上回傳任何整數都可以，不過一般來說，如果程式執行過程沒有遇到任何特殊情況，也就是正常的結束，那我們習慣使用 0 做為回傳結果。所謂的特殊情況，例如在做除法的時候，碰到了除以 0 的情形，這個時候，程式會產生錯誤 (error) 或者例外 (exception)。一個好的程式設計師，可能要針對這種情形做特別處理，譬如印出訊息並且結束程式，而且通常會回傳一個自己定義的非 0 值來表達這種特別情況的發生。

##### 註解

所謂的註解，指的是寫給人看，而編譯器不會加以理會和處理的說明文字。在程式碼中加入註解是一個好習慣，可以幫助讀者理解程式碼的意義。一個比較長或比較複雜的程式碼，如果沒有加以說明，有時候很難了解其意義，即使寫的人自己很清楚，但時間久了，寫的人自己可能也會忘記或搞不清楚，所以比較有經驗的程式設計師，通常都會在程式碼中加上註解，甚至還有專門的說明文件。

在 C 程式中如何加上註解呢？基本上有兩種型式。第一種是單行的註解，使用「//」符號。「//」符號可以出現在程式碼的任何位置，出現的地方一直到該行結束，編譯器都會忽略。例如：

```c
printf("Hello World!"); // 這是單行的註解文字
```

另外一種是使用「/*」符號做為開頭，並使用「*/」符號做為結束。兩個符號之間不論間隔多遠，中間的所有文字都會被編譯器忽略，所以這種形式的註解可以跨越很多行。例如：

```c
/**********************************************
  這種形式的註解可以跨越很多行，
  通常會放在程式檔案最開頭的位置。
**********************************************/
#include <stdio.h>
int main()
{
    printf("Hello World!");
    return 0;
}
```



## 2-2 標準輸出

一個應用程式，為了達成某些功能，通常都會有輸入和輸出。輸入的方式，最常見的是從鍵盤或檔案輸入；而輸出的部份，一般最常見的，是直接輸出文字到螢幕上，或者使用圖形介面來呈現在畫面上。另外我們也可以把輸出存成檔案，或者把它列印出來。在學習 C 程式的時候，一般我們從文字介面的程式開始，這時標準輸入指的是鍵盤，而標準輸出指的是螢幕，也就是從鍵盤讀入資料，並且把結果輸出到螢幕上。

C 語言最基本的輸入函數是 scanf，而基本的輸出函數則是 printf。使用標準輸入和輸出函數的時候，要先引入標頭檔 <stdio.h>。以下先介紹輸出函數 printf 的用法，等介紹過變數的使用之後，接著再介紹輸入函數 scanf 的用法。

C 語言使用 printf 函數將訊息列印至標準輸出，除了列印字串，也可以列印各種型態的變數，執行後會回傳所列印的字元數。printf 函數至少要有一個參數，而且第一個參數一定是一個格式字串，表示要輸出到螢幕的字串內容，例如：

```c
printf("format string");
```

其輸出結果如下：

```
format string
```

輸出之後，並不會換行，如果我們繼續輸出其他的訊息，就會直接接在後面。所以我們也可以使用以下的方式，來產生同樣的結果。

```c
printf("format");
printf(" string");
```

那如果我們想要換行的話，必須加上特殊的跳脫字元 \n，例如：

```c
printf("format\nstring");
```

其輸出結果如下：

```
format
string
```

注意 string 直接接在 \n 後面，表示換行之後接著輸出 string 字串。

除了 \n 這個跳脫字元，還有許多其他的跳脫字元，以下列出幾個比較常見的跳脫字元。

| 跳脫字元 |           功能            |
| :------: | :-----------------------: |
|    \t    | 移到下一定位，即 Tab 鍵功能 |
|    \n    |    移到下一行開頭位置     |
|   \\"    |        插入 " 字元        |
|   \\'    |        插入 ' 字元        |
|   \\\    |        插入 \ 字元        |

除了跳脫字元之外，我們還可以在字串中加上格式說明符號 (format specifier)，用來指明要列印的變數或數值格式。基本上字串中出現幾個格式說明符號，後面就必須加上相對應個數的參數。先看一個簡單的例子：

```c
printf("The number is %d", 10*3);
```

會產生如下的輸出結果：

```
The number is 30
```

這邊字串中所出現的 %d 就是格式說明符號，表示要在這個位置插入一個整數。那麼要插入什麼整數呢？ printf 會接著到格式字串之後找尋第二個參數。函數的輸入參數如果超過一個，必須用逗點分隔開來。所以這邊找到的參數就是 10*3，也就是 30，所以就把 30 插入到字串的 %d 的位置，而輸出了以上的結果。

我們也可以在 printf 的第一個字串中插入更多的格式說明符號。例如：

```c
printf("%d x %d = %d", 7, 9, 7*9);
```

會產生如下的輸出結果：

```
7 x 9 = 63
```

除了插入整數之外，還有很多代表不同意義的其他格式說明符號。一般來說，假如我們插入了 n 個格式說明符號，那麼在字串後就必須另外提供 n 個相對應的插入內容。以下表列出幾個比較簡單而常見的格式說明符號，以及說明其相對應的意義。

| 格式說明符號 |              功能              |
| :----------: | :----------------------------: |
|      %c      |          插入一個字元          |
|      %d      |          插入一個整數          |
|      %f      | 插入一個浮點數（有小數點的數） |
|      %s      |          插入一個字串          |
|      %%      |          插入 % 字元           |

以下舉出一個簡單的程式及其執行結果，方便讀者對照了解一些格式說明符號的功能。

```c=
#include <stdio.h>

int main() 
{
	printf("Display a character: %c\n", 'A'); // 'A' is a character
	printf("Display an integer: %d\n", 3456);
	printf("Display a float number: %f\n", 345.6);
	printf("Display a string: %s\n", "This is a string");
	printf("Display the %% character\n");
	return 0;
}
```

執行結果：

```
Display a character: A
Display an integer: 3456
Display a float number: 345.600000
Display a string: This is a string
Display the % character
```

> __練習__
>
> 請在螢幕上輸出以下的字串："The program uses 34% CPU resource."



## 2-3 變數宣告

一般的程式都會有輸入和輸出，輸入的資料通常用變數儲存起來，以便在程式中進行一些必要的運算，等最後得到我們所要的結果之後，再把它輸出到螢幕上。一般來說，變數是存放在電腦的記憶體裡面，我們可以把它想像成一個箱子，裡面可以用來存放一些內容，譬如整數、字元、實數，乃至其他一些更複雜的型態。以下先以最基本的整數型態，來說明變數的宣告和使用。

整數變數的宣告使用 int，後面必須有空格，然後再接變數的名稱。變數的名稱可以使用 a-z， A-Z，_， 0-9 等字元拼成的字串，但是不可用數字起頭。舉例而言，a3 是有效的變數名稱，但是 3a 卻是無效的。另外大小寫是有分別的，所以 a3 和 A3 是兩個不同的變數。變數名稱的長短不會影響編譯出來的程式碼，所以可儘量取有意義而容易理解的名稱，例如，要把長方形的長和寬存放在變數裡面，使用width 和 height 當作變數名程，程式讀起來會更容易理解。當然，如果我們只用 w 和 h 來命名，其實也很容易理解，但是當程式越來越大的時候，取個有意義的名稱，會是比較好的習慣。以下的語法敘述宣告一個整數變數 x：

```c
int x;
```

宣告之後就可以使用它來存放整數值，例如，要把 10 存放在 x 裡面，或者說，我們要把 x 設成 10，可以使用以下的敘述：

```c
x = 10;
```

上面兩個敘述，也可以合成一個，也就是在宣告的時候，同時設定變數的初始值：

```c
int x = 10;
```

如果我們要使用更多的整數變數，例如兩個整數變數 x 和 y，我們可以使用兩個敘述來宣告：

```c
int x;
int y;
```

但也可以把兩個敘述合成一個，像這樣：

```c
int x, y;
```

基本上只要使用逗號分開，在一行程式碼裡面可以同時宣告很多個變數。例如以下的範例，同時宣告 5 個整數變數，其中三個設定了啟始值：

```c
int x, y=5, z=3, s, t=8;
```

不過上面的使用方式並不建議，因為對語法不夠清楚的人，很容易會以為是同時把 x 和 y 都設成5，同時把 s 和 t 都設成 8，但實際上，只有 y、z 和 t 三個變數設定啟始值而已。



## 2-4 標準輸入

C 語言使用 scanf 函數從標準輸入來讀取變數的值，也就是讓使用者從鍵盤輸入變數值。scanf 的第一個參數必須是一個格式字串，通常裡面都會放格式說明符號，表示要讀入的變數的型態，這邊所說的格式說明符號和 printf 用的是一樣的。例如，假設我們要輸入一個整數到變數 x，相對應的程式碼如下：

```c
int x; // x is an integer variable
scanf("%d", &x); // input x value
```

這邊第 1 列是宣告 x 為一個整數變數，第 2 列則讓使用者輸入變數 x 的值。程式執行到 scanf 的時候，會停住，等待使用者從鍵盤輸入一個整數，然後把整數存入 x 之後，再繼續執行。

scanf 函數的使用方式和 printf 函數有點像，不過有兩個地方必須加以說明：

1. 和 printf 一樣，格式字串中出現幾個格式說明符號，後面也要額外加上同樣個數的參數，而參數放的是**變數地址**。
2. 變數前必須加上「&」符號，實際上這是取得**變數地址**的意思，也就是說，我們要把變數的地址傳到 scanf 函數裡面。我們在使用 printf 的時候，變數前並沒有加上「&」符號，表示傳進 printf 函數的是變數的值，而不是變數的地址。這一點非常重要，如果少了這個「&」符號，執行結果就會不正確，甚至會讓程式當掉。關於這個部份，更詳細的原因，會在指標的章節裡面說明，讀者可以先把它看成是一個規則：使用 printf 輸出變數的時候，變數名稱前不加「&」符號；但使用 scanf 輸入變數的時候，變數名稱前必須加上「&」符號。

如果我們要分別讀取整數到變數 x 和 y，對應的程式碼如下：

```c
int x, y; // x and y are integer variables
scanf("%d", &x);
scanf("%d", &y);
```

我們也可以把第 2 列和第 3 列合併，改寫如下：

```c
int x, y;
scanf("%d %d", &x, &y);
```

程式執行的時候，會等使用者輸入兩個整數，然後才繼續執行。兩個輸入的整數，必須使用一些空格分開。這邊所謂的空格，不管是空白鍵、定位鍵或者換行鍵都可以，不論輸入多少空格，都會被忽略掉，只有數字的部份才會被讀取進來。一般來說，scanf 讀取變數的時候，預設會把空格當成是輸入變數值之間的分隔符號，如果我們在格式字串中，沒有使用空白其實也沒有關係。所以上面的程式碼，很多人會把它寫成：

```c
int x, y;
scanf("%d%d", &x, &y);
```

注意上面的程式中，兩個 %d 之間是相連在一起的，沒有任何空白字元。

以下舉一個簡單的程式例子，由使用者輸入兩個整數，然後把它們的乘積列印出來。

```c=
#include <stdio.h>

int main()
{
    int x, y;
    scanf("%d%d", &x, &y);
    printf("%d x %d = %d\n", x, y, x*y);
    return 0;
}
```

> __練習__
> 
> 輸入長方體的長、寬、高，然後利用程式把該長方體的體積和表面積印出來。



## 2-5 變數型態

我們前面已經介紹過整數的宣告和使用，實際上 C 語言裡面還有很多其他的變數型態。這一節將說明一些 C/C++ 裡面基本而常見的變數型態。

### 2-5-1 整數型態

整數型態，除了前面提過的 int 型態之外，還有許多不同的變型，以下簡列幾個比較常見的整數變型。

| 名稱     | 宣告方式                   | 格式說明符號 | 說明                                                         |
| -------- | -------------------------- | ------------ | ------------------------------------------------------------ |
| 整數     | int                        | %d           | 一般使用 4 個位元組，共 32 位元，其中第 1 個位元表示正負號，負數以 2 的補數形式表示，可以表示的整數範圍從 $-2^{31}$ 到 $2^{31}-1$ 。 |
| 長長整數 | long long 或 long long int | %I64d 或 %lld，依編譯器而定         | 一般使用 8 個位元組，共 64 位元，其中第 1 個位元表示正負號，負數以 2 的補數形式表示，可以表示的整數範圍從 $-2^{63}$ 到 $2^{63}-1$ 。 |
| 字元     | char                       | %c           | 使用 1 個位元組，共 8 位元。一般字元的編號是依照 ASCII 標準。也可以算是一種整數，不過範圍只從 -128 到 127。 |
| 無號整數 | unsigned 或 unsigned int   | %u           | 使用 4 個位元組，共 32 位元，沒有正負號位元，可以表示的整數範圍從 $0$ 到 $2^{32}-1$ 。 |

上表中，最後一個無號整數，是在整數型態詞 int 前面加上 unsigned 關鍵字，表示這個整數是沒有符號位元的，因此也可以看成是非負整數。一般在計算個數的時候，可以用無號整數，但如果大小不會超過整數的範圍，通常都直接使用整數來處理。另外，unsigned 關鍵字也可以放在 long long 前面，或者 char 前面，但因為相對比較少用，這邊就沒有特別列出來了，如果讀者有需要使用到的話，可以再上網查詢。

一般會使用到 long long 整數的原因，主要是因為數字太大，使用一般的整數已經無法容納，因而會產生所謂的**溢位**的問題，這時只好使用更大的長長整數的型態來處理。舉例而言，觀察以下的程式代碼：

```cpp
#include <stdio.h>

int main()
{
    int a = 2；
    a = a * a；
    printf("%d\n"， a)； // ==> 4
    a = a * a；
    printf("%d\n"， a)； // ==> 16
    a = a * a；
    printf("%d\n"， a)； // ==> 256
    a = a * a；
    printf("%d\n"， a)； // ==> 65536
    a = a * a；
    printf("%d\n"， a)； // ==> 0
    return 0；
}
```

注意這個程式執行的結果，最後一個輸出會是 0，實際上，應該是要輸出 $2^{32}=4294967296$，但是 $2^{32}$ 是一個 1 加上 32 個 0，而整數只能容納 32 個位元，結果最前面的 1 就不見了，因而產生錯誤的結果，這就是所謂的溢位。在這個例子中，如果我們把 int 變成 long long，並且把 %d 改成 %l64d，就不會產生溢位的問題。當然，如果我們再繼續乘下去的話，仍然會超出 long long 的範圍而產生溢位。讀者在使用變數的時候，特別當數目字很大時，必須要關注是否會發生溢位的問題。

### 2-5-2 字元型態

在上面的表格中，我們也看到了字元的型態，基本上在 C 語言中，字元可以看成是一個位元組的整數，不過更多時候，字元是被拿來當作文字使用，所以另外在這個段落加以說明。所謂的字元，指的是用一個位元組儲存的字元符號，像一般的英文字母、數字、鍵盤上的各種符號等都算。一般字元符號，通常會遵循 ASCII 標準的位元組編碼順序。所謂的 ASCII 標準，指的是美國資訊交換標準代碼 (American Standard Code for Information Interchange)，其中針對各種常用字元，制定了相關的字元編碼，例如一般常見的鍵盤上的字元，其編碼如下：

![](https://imgur.com/DtrfXvQ.png)

這個表只是幫助我們對於 ASCII 的字元編碼有一些了解，實際使用時，通常不需要去記憶這些編碼，因為在 C 語言裡面，我們可以使用單引號來直接使用字元，例如 'A'， 'B'...。當然，如果我們知道這些字元的編碼，我們也可以直接使用它們所對應的編碼整數，例如以下程式碼：

```c=
#include <stdio.h>

int main()
{
    printf("Char %c => ASCII %d\n", 'a', 'a');
    printf("Char %c => ASCII %d\n", 97, 97);
    return 0;
}
```

輸出結果為：

```
Char a => ASCII 97
Char a => ASCII 97
```

從上面的結果可以看出來，'a' 和 97 其實是相同的，另外列印時，用 %c 時輸出會變成字元，用 %d 時則會變成整數。

> __例題__
>
> 輸入一個小寫字元，將其變成大寫字元後再輸出到螢幕上。

解答：

小寫字元從 'a' 到 'z' 編碼是連續的，另外大寫字元從 'A' 到 'Z' 也是連續的。那麼怎麼把小寫的 'a' 變成大寫的 'A' 呢？答案就是把它加上 'A' - 'a'，這其實顯而易見，因為 'a' + 'A' - 'a' = 'A'。如果我們知道 'A' - 'a' = 65 - 97 = -32，那麼也可以直接減掉 32 就可以了。不過我們通常不會去記憶字元的編碼，所以通常還是把它加上 'A' - 'a'。那麼如何把小寫的 'm' 變成大寫的 'M' 呢？同樣加上 'A' - 'a' 就可以了，因為 'm' + 'A' - 'a' = ('m' - 'a') + 'A' = ('M' - 'A') + 'A' = 'M'。這邊用到一個概念，就是 'm' 和 'a' 的差距其實和 'M' 和 'A' 的差距是一樣的。了解之後，程式碼就很容易寫了：

```c=
#include <stdio.h>

int main()
{
    char ch;
    scanf("%c", &ch);
    printf("%c", ch + 'A' - 'a');
    return 0;
}
```

> __練習__
>
> 輸入三個大寫字元，將它們變成小寫字元後輸出到螢幕上。

### 2-5-3 浮點數型態

所謂的浮點數，就是一般我們所謂的實數，更明確一點講，就是帶有小數的數。實數因為可能會有無限的位數，而在電腦中我們只能儲存有限的位數，所以會有精確度的問題，通常儲存的只是一個近似值而已。在 C 語言中，常見的浮點數型態有兩種，簡列如下：

| 名稱         | 宣告方式 | 格式說明符號 | 說明                                                         |
| ------------ | -------- | ------------ | ------------------------------------------------------------ |
| 單精度浮點數 | float    | %f           | 使用 4 個位元組，共 32 位元，其中包括正負號位元，以及基數和指數部份，可以表達的大小（不考慮正負號）約從 $1.2\times 10^{-38}$ to $3.4\times 10^{38}$，有效位數約 6 位。 |
| 倍精度浮點數 | double   | %lf          | 使用 8 個位元組，共 64 位元，其中包括正負號位元，以及基數和指數部份，可以表達的大小（不考慮正負號）約從 $2.3\times 10^{-308}$ to $1.7\times 10^{308}$，有效位數約 15 位。 |

實際使用時，可以根據我們的需要，選擇單精度浮點數或者倍精度浮點數。

> __例題__
>
> 輸入半徑，由程式計算圓面積並列印出來。

解答：

圓面積的公式是圓周率乘上半徑平方，假設使用倍精度浮點數，程式碼如下：

```c=
#include <stdio.h>

int main()
{
    double r;
    scanf("%lf", &r);
    printf("Area = %lf\n", 3.14159*r*r);
    return 0;
}
```

執行範例：

```
3.0
Area = 28.274310
```

> __練習__
>
> 輸入圓柱的半徑和高度，由程式計算其表面積並把它輸出到螢幕上。



## 2-6 基本運算

這一節介紹 C 語言中一些比較常見的基本運算，包括加、減、乘、除、求餘數、指派、遞增、遞減、比較等運算。以下分別說明。

### 2-6-1 加減乘除及餘數運算

針對兩個數之間的運算，最常看到的就是加減乘除四則運算，在 C 語言中，分別使用「+」、「-」、「*」、「/」四個符號來代表加減乘除。這裡要特別注意一點，就是 C 語言中，兩個整數的四則運算，得到的結果仍然是整數。這對於加減乘三種運算來說不會有問題，因為結果本來就是整數。但是對於除法來說，結果有可能不是整數，這樣一來，就可能和我們的想法有些出入。舉例而言，5/2 應該會得到 2.5，但是在 C 語言中，直接計算 5/2 卻會得到 2，以下程式可以驗證這一點：

```c=
#include <stdio.h>

int main()
{
    printf("5/2 = %d", 5/2);
    return 0;
}    
```

輸出結果：

```
5/2 = 2
```

那如果我們希望得到 2.5，應該怎麼做呢？應該要使用浮點數。我們可以把 5/2 改成 5.0 / 2.0，這樣的話，就可以得到我們希望的結果。

另外還有一點要注意，就是整數的四則運算，會遵照先乘除後加減的規則，例如以下的算式：

```
3 + 4 * 2
```

得到的結果是 3 + 8 = 11，因為乘法的運算優先權比加法來得高的緣故。

另外在一個算式中，如果出現的運算子優先權是一樣的，則式子會依序從左邊算到右邊，例如 3 * 5 / 6 會等於 15 / 6，最後得到的結果為 2。但是 3 * (5 / 6) 的結果為 3 * 0，得到的結果會是 0。兩者是不一樣的。

如果我們希望改變運算順序，可以使用小括號。例如：

```
(3 + 4) * 2
```

這樣，就會得到 7 * 2 = 14。這和我們以前學到的規則是一樣的。

兩個整數之間，還有一個常見的運算，就是求相除之後的餘數，在C語言中，使用 % 來求相除的餘數，例如：

```
11 % 3
```

得到的結果就是11除以3的餘數，也就是2。

### 2-6-2 指派運算

指派運算指的是「=」這個運算，它的右邊是一個數字或者運算式，左邊則是一個變數。執行的時候，會先把右邊的結果算出來，再把它存到左邊的變數裡面。例如：

```c
x = 3；
y = 5 + 2*8；
z = x + y；
t = t + 1；
```

注意上面的第 4 列，t=t+1，這種形式就數學上來說是不可能成立的，但程式語言裡面用得卻非常的多。它的意思是先把 t 的值加上 1，算完之後再把這個值指定給 t，這樣一來，t 就等於原來的值再加上 1。另外有一點要注意的，初學的同學有時會把 = 兩邊寫反，例如 x=3 寫成 3=x，這樣會引起編譯上的錯誤，因為我們不能把 x 的值存到 3 裡面，3 只是一個常數而已。

接下來有一類運算子，是把上一節提到的運算符號和「=」結合，而構成新的指派運算子，例如：「+=」、「-=」、「*=」、「/=」、「%=」。此處先以「+=」為例來做說明，其餘的可以同理類推。

「+=」的運算過程，一樣先把右邊的運算式算出來，然後把這個值加上左邊的變數值之後，再存放到左邊的變數。所以一般而言，下面兩種寫法，其執行結果會是一樣的：

```c
x += 3;
x = x + 3;
```

了解「+=」的意義之後，其他幾個類似的也可以了解。例如  `x *= 3`，就是把 x 乘上 3 之後，再把結果存回 x 變數。
有的同學會把 x ?= y 簡單記成 x = x ? y，這邊 ? 指的是「+」、「-」、「*」、「/」之類的運算子。這個概念基本上是對的，但如果 y 是一個運算式，必須先把它算完，才套這個公式，否則會有問題。例如：

```c
x *= 3 + 2;
```

解讀的時候，應該是  `x *= 5`  或者  `x = x * 5`。但如果我們直接展開的話，則會變成  `x = x * 3 + 2`，因為先乘除後加減的緣故，上面的結果就會變成原來的值乘以 3，再加上 2 的結果，這和實際想得到的計算結果是有出入的，所以這一點要特別注意。

> __例題__
>
> 寫出一段程式碼，將兩整數 x 和 y 的值互相交換。

解答：

把兩個數互相交換的應用很多，而交換的方法也很多。一般比較常見的方法，是宣告一個暫存的變數，然後把 x 的值放到暫存變數裡，接著設 x 的值為 y，再把 y 的值設成暫存變數的值。程式碼如下：

```c
int t；
t = x；		x = y；		y = t；
```

如果還不能理解這段程式碼，可以想像有兩個獨臂俠 x 和 y 要交換珍貴的禮物，那麼 x 先把禮物放在桌上 (t)，然後 x 空出手來就可以拿取 y 的禮物，最後 y 再從桌上拿走 x 的禮物。這種交換變數值的方法很普遍，讀者應該要牢牢記住。

### 2-6-3 遞增、遞減運算

在程式中，x = x+1 或 x = x-1 這樣的運算用得很多，也就是把一個整數變數加上 1 或者減掉 1 的運算。雖然我們可以把它寫為 x += 1 或者 x -= 1，但這樣還是不夠精簡。C 語言中定義了遞增運算子 ++ 和遞減運算子 --，可以用來達成同樣的目的。不過這裡面還有分前置和後置的差異，以 ++ 為例，先看下面程式碼：

```c
x = x+1;
x += 1;
x++;
++x;
```

上面的 4 列程式碼，如果只執行其中任何一列，其運算意義都是相同的，都是把 x 變數加上 1 的意思。其中第 3 列把 ++ 放在變數後面，算是後置，而第 4 列把 ++ 放在變數前面，算是前置。這裡不論是前置或後置，運算的結果是沒有差別的。

不過遞增和遞減運算子除了單獨出現，也可以放在一個表達式中，這時前置和後置就有差別了。前置的時候，要先把變數的值加 1，然後再計算整個表達式。反過來，後置的時候，要先計算整個表達式，算完之後再把變數加 1。舉例來說：

```c
int x = 3;
int y = 5 + ++x;
```

在上面程式中第 2 列出現的 ++，因為是前置，所以會先把 x 變成 4，然後才計算 y = 5 + x 的表達式，所以算完之後，y 的值會變成 9。如果我們把它改成

```c
int x = 3;
int y = 5 + x++;
```

這樣一來，「++」變成是後置運算，所以會先計算 y = 5 + x 表達式的結果，算出來 y 是 8，接下來才把 x 加 1。兩個不同的寫法，計算出來的結果，x 都是相同的，但 y 卻是不相同的。

我們來看一個稍微複雜一點點的例子：

```c
int x=3, y=4, z;
z = x++ * --y;
```

這個例子中，同時出現前置和後置的情況，根據以上的原則，前置的在表達式前要先計算，後置的在表達式之後計算，所以第 2 列可以把它拆解成以下三個部份：

```c
--y;	    // y becomes 4-1=3
z = x * y;  // z becomes 3*3＝9
x++;	    // x becomes 3+1=4
```

所以計算出來的結果：x=4, y=3, z=9。

### 2-6-4 比較運算

比較運算通常是用來比較大小，或者相不相等的運算，如果比較結果是成立的，則得到 1 的結果，如果是不成立的，則得到 0 的結果。一般我們把 1 當作邏輯上的真值，把 0 當作邏輯上的假值，這在後面的分支和迴圈指令裡面，會經常使用到。有一點必須注意：在判斷真假值的時候，除了 0 是邏輯上的假值之外，其餘的數值都會被視為真值。換句話說，不僅 1 被當作真值，只要不是 0 的值，也都被當成是真值。

以下列出常見的比較運算子及其意義：

| 運算符號 | 意義       | 範例   | 範例結果 |
| -------- | ---------- | ------ | -------- |
| >        | 大於       | 5 > 3  | 1        |
| \>=      | 大於或等於 | 5 >= 3 | 1        |
| <        | 小於       | 5 < 3  | 0        |
| <=       | 小於或等於 | 5 <= 3 | 0        |
| ==       | 相等       | 5 == 3 | 0        |
| !=       | 不等       | 5 != 3 | 1        |

在進行比較運算的時候，有時候會需要更複雜的判斷情況，這時還有以下三個運算子可以加進來使用，表列如下：

| 運算符號 | 意義                                 | 範例             | 範例結果 |
| -------- | ------------------------------------ | ---------------- | -------- |
| &&       | 邏輯的且，兩邊的值都是真值的時候成立 | (5>3) && (4>6)   | 0        |
| \|\|     | 邏輯的或，兩邊的值只要存在真值就成立 | (5>3) \|\| (4>6) | 1        |
| !        | 邏輯的反值，把右邊的真假值反過來     | ! (5>3)          | 0        |

一般來說，C語言已經根據最常使用的情況，定出各種運算子的優先順序，例如 5>3 && 4>6，會先計算 5>3 和 4>6 的結果，再把這兩個結果做邏輯且的運算。不過有時候，可能式子很複雜，或者我們也不記得運算子的順序，所以適當地加上一些小括號，來說明希望的運算順序會是一個比較好的習慣，就像上面的範例一樣，我們把 5>3 && 4>6 寫成 (5>3) && (4>6) ，這樣不僅容易閱讀，也比較不容易出錯。

### 2-6-5 轉型運算

轉型運算指的是把一種資料型態轉變成另一種資料型態，例如把整數型態轉變成浮點數型態，或者把浮點數型態轉變成整數型態。以整數的除法為例，我們上面提到過，整數除以整數仍然為整數，所以 5/2 會得到 2 而不是 2.5，假設我們有 x 和 y 兩個整數變數，其中 x 為 5，而 y 為 2，那麼我們要如何做才能讓 x / y 變成 2.5 而不是 2 呢？這時候就必須使用轉型運算了。

轉型的方式有兩種，一種是隱式的 (implict)，就是沒有特別在表達式中寫出來，但卻會有自動轉型的效果。例如：

```c
float x = 3 / 5.0;
```

在上面的式子中，x 的值被指定為 3/5.0，這邊 3 是整數，而 5.0 是浮點數，在計算的時候，3 會先被自動轉型成浮點數，然後再計算兩個浮點數的除法。一般來說，一個算式中，如果同時有整數和浮點數出現，那麼整數會被自動轉型成浮點數。不過我們仍然必須注意運算的優先順序，舉例而言：

```c
x = 1/2 + 0.5;
```

在上面的算式中，1/2 會先被計算，算完之後才會再加上 0.5。注意 1/2 的運算中，兩個都是整數，所以得到的值是 0，最後加上 0.5 時，才會把 0 轉成浮點數，這時已經來不及了，最後得到的結果變成 0.5。如果我們希望得到的是 1.0，可以把它改寫如下：

```c
x = 1.0/2 + 0.5;
```

另外一種轉型的方式是顯式的 (explict)，就是直接把希望轉變成的型態用小括號括住，再放到要轉型的資料前面，例如：

```c
x = (float)1 / 2;
```

這裡 1 會先被轉型成浮點數，然後才除以 2，結果 2 也會被轉成浮點數再做運算，最後得到 0.5 的結果。注意上面的式子中，不能寫成 x = (float)(1/2)，如果這樣寫的話，1/2 會先得到整數 0，最後再轉型就變成 0.0 了。

一般來說，從整數轉型成浮點數比較不會有問題，因為浮點數的數目範圍比整數來得大，所以是可以容納的，但如果整數的位數很多，也有可能會喪失一些精確度。反過來說，如果把浮點數轉型成整數，那麼就要注意是否會超過整數的範圍，如果超過的話，就會產生比較大的問題，但如果不會超過的話，轉型時會直接把小數部份去掉，而不是做四捨五入的運算，這一點也是必須要注意的。舉例而言：

```c
int x = (int)2.9999;
```

得到的結果， x 值是 2 而不是 3。

> __練習__
>
> 由使用者輸入兩個整數，將其存到整數變數中，再計算它們的實數相除的商，例如輸入的值為 2 和 5，則輸出的結果應為 0.4。



## APCS 範例

##### 10503 觀念題 18

程式編譯器可以發現下列哪種錯誤？

(A) 語法錯誤    (B) 語意錯誤    (C) 邏輯錯誤    (D) 以上皆是

解答：程式編譯器負責翻譯，只能發現語法的錯誤，故答案為 (A)。



##### 10510 觀念題 4

以下程式碼執行後輸出結果為何？

```c
int a=2, b=3;
int c=4, d=5;
int val;
val = b/a + c/b + d/b;
printf ("%d\n", val);
```

解答：

這邊全部的變數都是整數，所以運算時結果也只能取整數，所以 b/a = 3/2 = 1，c/b = 4/3 = 1，d/b = 5/3 = 1，最後得到 val = 1 + 1 + 1 = 3，所以輸出結果為 3。



##### 10510 觀念題 14

假設 x， y， z 為布林 (boolean) 變數，且 x=TRUE， y=TRUE， z=FALSE。請問下面各布林運算式的真假值依序為何？(TRUE 表真，FALSE 表假)

- !(y || z) || x
- !y || (z || !x)
- z || (x && (y || z))
- (x || x) && z

(A) TRUE FALSE TRUE FALSE

(B) FALSE FALSE TRUE FALSE

(C) FALSE TRUE TRUE FALSE

(D) TRUE TRUE FALSE TRUE

解答：

|| 是邏輯或，只要有一個為真，則結果為真。&& 是邏輯且，只要有一個為假，則結果為假。 ! 是相反運算，把真變成假，把假變成真。所以結果依次如下：

1. !(y || z) || x ==> TRUE (因為最後一項 x 為 TRUE)
2. !y || (z || !x) ==> FALSE || (FALSE || FALSE) ==> FALSE，實際上到這邊已可確定答案為 (A)
3. z || (x && (y || z)) ==> FALSE || (TRUE && (TRUE || FALSE)) ==> TRUE && TRUE ==> TRUE
4. (x || x) && z ==> TRUE && FALSE ==> FALSE

   

##### 10510 觀念題 19

下列程式碼是自動計算找零程式的一部分，程式碼中三個主要變數分別為 Total (購買總額)，Paid (實際支付金額)，Change (找零金額)。但是此程式片段有冗餘的程式碼，請找出冗餘程式碼的區塊。

```c
int Total, Paid, Change;
…
Change = Paid - Total;
printf ("500 : %d pieces\n", (Change-Change%500)/500);
Change = Change % 500;
printf ("100 : %d coins\n", (Change-Change%100)/100);
Change = Change % 100;
// A 區
printf ("50 : %d coins\n", (Change-Change%50)/50);
Change = Change % 50;
// B 區
printf ("10 : %d coins\n", (Change-Change%10)/10);
Change = Change % 10;
// C 區
printf ("5 : %d coins\n",(Change-Change%5)/5);
Change = Change % 5;
// D 區
printf ("1 : %d coins\n",(Change-Change%1)/1);
Change = Change % 1;
```

(A) 冗餘程式碼在 A 區		(B) 冗餘程式碼在 B 區

(C) 冗餘程式碼在 C 區		(D) 冗餘程式碼在 D 區

解答：

1. 這個程式依次計算需要幾個 500 元，餘數再用來計算有幾個 100 元，然後依次類推，計算 50， 10， 5， 1 元之個數。
2. 計算到 1 元幣值的時候，所餘的錢就是答案，不需要再求除以 1 的餘數和商，因為除以 1 的商會得到原來的值，除以 1 的餘數一定為 0，且除以 1 的餘數已經用不到，故 D 區是冗餘的程式碼。



##### 10510 觀念題 22

如果 $X_n$ 代表 $X$ 這個數字是 $n$ 進位，請問 $D02A_{16} + 5487_{10}$等於多少？

(A) $1100 0101 1001 1001_2$		(B) $162631_8$

(C) $58787_{16}$							  (D) $F599_{16}$

解答：

1. 這四個解答都是 2 進位、8 進位或 16 進位的數，所以先把唯一的十進位數轉成 16 進位，方便觀察。
2. $5487_{10} = 156F_{16}$
3. $D02A_{16} + 5487_{10} = D02A_{16} + 156F_{16} = E599_{16} = 1110 0101 1001 1001_{2} = 162631_{8}$，答案為 (B)。 



##### 10603 觀念題 11

若 A[1]、A[2]，和 A[3]分別為陣列 A[] 的三個元素(element)，下列那個程式片段可以將 A[1] 和 A[2] 的內容交換？

(A) A[1] = A[2]; A[2] = A[1];

(B) A[3] = A[1]; A[1] = A[2]; A[2] = A[3];

(C) A[2] = A[1]; A[3] = A[2]; A[1] = A[3];

(D) 以上皆可

解答：

雖然還沒有學到陣列，但我們可以把 A[1]、A[2]、A[3] 看成變數 A1， A2， A3。要交換兩個變數的值，我們在上面曾經提及，例如要交換 x 和 y 的值，一般會先宣告一個暫存變數 t，然後進行下面的運算：

```c
t = x;		x = y;		y = t;
```

這邊把 A1 當成 x，把 A2 當成 y，把 A3 當作暫存變數 t，很明顯答案為 (B)。



##### 10603 觀念題 12

若函式 rand() 的回傳值為一介於 0 和 10000 之間的亂數，下列那個運算式可產生介於 100 和 1000 之間的任意數(包含 100 和 1000)？

(A) rand() % 900 + 100		(B) rand() % 1000 + 1

(C) rand() % 899 + 101		(D) rand() % 901 + 100

解答：

1. 總共要產生的數字共有 1000-100+1 = 901，所以要有 901 種可能的狀況，依此就可以知道答案是 (D)。
2. rand() 除以 901 的餘數可能的範圍為 0...900，再加上 100，就變成 100...1000。
3. 一般求 a 到 b 的亂數，可以使用 rand() % (b-a+1) + a 來產生。



##### 10603 觀念題 22

若要邏輯判斷式 !(X1 || X2)計算結果為真(True)，則 X1 與 X2 的值分別應為何？

(A) X1 為 False，X2 為 False		(B) X1 為 True，X2 為 True

(C) X1 為 True，X2 為 False		 (D) X1 為 False，X2 為 True

解答：

因為 ! 是相反運算，所以最後結果為真，表示 X1 || X2 為假。又 || 是邏輯或的運算，只要有一邊為真，則結果為真，故若結果為假，則兩邊皆須為假。由以上分析，答案為 (A)。



##### 10603 觀念題 23

程式執行時，程式中的變數值是存放在

(A) 記憶體
(B) 硬碟
(C) 輸出入裝置
(D) 匯流排

解答：

程式中的變數值是存放在記憶體中，故答案為 (A)。



##### 10603 觀念題 24

程式執行過程中，若變數發生溢位情形，其主要原因為何？

(A) 以有限數目的位元儲存變數值
(B) 電壓不穩定
(C) 作業系統與程式不甚相容
(D) 變數過多導致編譯器無法完全處理

解答：

變數發生溢位，主要原因是因為變數所佔的位元組固定，只能用有限數目的位元儲存變數值，故答案為 (A)。



##### 10603 觀念題 25

若 a， b， c， d， e 均為整數變數，下列哪個算式計算結果與 a+b*c-e 計算結果相同？

(A) (((a + b) * c) - e)
(B) ((a + b) * (c - e))
(C) ((a + (b * c)) - e)
(D) (a + ((b * c) - e))

解答：

乘除的運算優先權高於加減，所以 b * c 會先計算。接下來加減的運算優先權是一樣的，所以會從左到右計算。依此原則，答案應該為 (C)。


