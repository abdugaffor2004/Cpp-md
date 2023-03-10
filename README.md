# Числа и строки

## Целые числа

Чтобы вывести на экран целое число 42, нужно написать:

```
#include <iostream>
using namespace std;
```
int main() { cout << 42 << endl; (^)
}
42 — **целочисленный литерал** , то есть целое число, записанное цифрами в коде
программы. Бывают литералы других типов. Например, ```"Hello, friend!"``` —
**строковый литерал** , который задаёт строку ```Hello, friend!```.


Чтобы объявить числовую переменную, нужно указать тип данных ```int```. Он
представляет целое число:

```
#include <iostream>
using namespace std;
int main() { 
  int x = 42; (^)
  cout << x << endl;
}
```

Тип переменной задают при её объявлении и не меняют. Такая программа не
скомпилируется, так как переменной целочисленного типа попытались присвоить
значение строки:

```
#include <iostream>
using namespace std;
int main() { 
  int x = 0; (^)
  x = "42"; // ошибка!
}
```

Переменные типа ```int``` хранят в себе положительные и отрицательные числа.
Переменные объявляются так:
```
#include <iostream>
using namespace std;
int main() { 
  int a; // Неинициализированная значением переменная. Её значение будет случайным числом. 
  int b = 1; 
  int c1 = 2, c2 = -3;
}

```
Над переменными и литералами можно выполнять арифметические действия:

```
#include <iostream>
using namespace std;

int main() { 
  int x = 1 + 2; (^)
  int y = x + 3; cout << x << endl // 3 (^)
  << y << endl // 6 << x * 10 << endl // 30 (^)
  << y / 4 << endl; // 1
}
```

## Вещественные числа

Вещественные числа представляет тип данных double:

```
#include <iostream>
using namespace std;

int main() { double pi = 3.14;}
```

Арифметические операции над вещественными числами производятся так же, как
над целыми:
```
#include <iostream>
using namespace std;
int main() {
  double x = 1;
  double y = 3; cout << x + y << endl // 4
  << x - y << endl // -2 << x * y << endl // 3
  << x / y << endl; // 0.333333
}
```
C++ умеет неявно преобразовывать численные типы друг к другу:

```
#include <iostream>
using namespace std;
int main() { 
int x = 42;
double y = x; // 42.0 
double z = -(x + y + 0.8); // -84.
int w = z; // -84, округление в сторону нуля, дробная часть отбрасывается
}
```

## Строки

Чтобы создать строковую переменную, нужно объявить переменную типа ```string``` и
положите в неё значение:

```
string news = "Great news!"s;// Переменная news содержит текст Great news!
```

Если просто объявить строковую переменную, не указав начальное значение, в
ней будет содержаться пустая строка:

```
int age; // В переменной age будет содержаться мусор (неопределённое значение)string name;
// В переменной name будет пустая строка
```
Строки можно склеить в одну. Для этого используется операция +:

```
string great = "Great "s;string news = "news!"s;
string design = great + news; // Получается "Great news!"
```
Чтобы просто последовательно вывести две строки, склеивать их не нужно.
Просто выведите строки одну за другой:

```
cout << great << news;
```
Операция += дописывает содержимое второй строки в конец первой:

```
string great = "Great "s;
string news = "news!"s;
string design;
design += great;
design += news;// Теперь в переменной design содержится строка "Great news!"
```

Из ```cin``` строка считывается до первого символа-разделителя: пробела, табуляции
или перевода строки. Пробелы между словами не считываются:

```
string name;
string surname;
cout << "Enter your name:"s << endl;cin >> name >> surname;
cout << "Hello, "s << name << " "s << surname << endl;
```

Если пользователь введёт строку John Doe, слово John будет прочитано в
переменную name, а слово Doe — в переменную surname.
Чтобы считать всю строку, а не только текущее слово, используют функцию
```getline```:

```
string full_name, address;getline(cin, full_name);
getline(cin, address);cout << "Hello, "s << full_name << " from "s << address << endl;
```

## Нюансы операций над строками

**Для сложения обычных строковых литералов** (без “”s) **нельзя
использовать +.**
Нужно использовать ""s-литералы, которые напрямую создают объект типа
string:

```
#include <iostream>
using namespace std;

int main() {
  cout << "I know "s + "C++"s << endl; // Следующие варианты также возможны 

  // cout << "I know"s + "C++" << endl; // cout << "I know" + "C++"s << endl;
}
```
  
**Строки и числа нельзя складывать.**
В C++ преобразование числа в строку и обратно должно выполняться явно. Для
этого служат функции:

* ```{{stoi}}```[be_translate_cpp_stoi];
*```{{stod}}```[be_translate_cpp_stod];
*```{{to_string}}```[be_translate_to string].

```
int x = stoi(x_str); // string -> intdouble y = stod(x_str); // string -> double (^)
string s = to_string(x); // int or double -> string
int z = 42;string t = "Hello"s + to_string(z); // В t будет значение "Hello42"
```

**Узнать размер строки можно функцией size.**
Синтаксис её вызова:

```
// Метод size вызывается у строки, созданного строковым литералом "Hello"s
  int length = "Hello"s.size(); // значение length равно 5

  string greeting = "Hi"s;
// Метод size вызывается у строки greeting
  int greeting_size = greeting.size(); // значение greeting_size равно 2
  greeting = "Bye"s;
  greeting_size = greeting.size(); // значение greeting_size
```

Такие функции называются «метод».
Размер строки, которую вернул метод ```size```, исчисляется в элементах типа ```char```:

```
cout << "Hello"s.size() << endl // 5 
<< "Привет"s.size() << endl // 12 — кириллица в UTF-8
<< "😊"s.size() << endl; // 8 — эмодзи
```


Если строка состоит только из латинских букв, цифр, пробела и основных знаков
препинания, её размер будет равен её длине.


# Условия и циклы 

## Условный оператор if

  Условный оператор ```if``` показывает, что команда выполнится при соблюдении
  некоторого условия или не выполнится, если условие не соблюдено:
  ```
    int a, b;
    cin >> a >> b;
    if (a == b)
      cout << "equal"s << endl;
  ```
  Ветка else указывает на команду, которая будет выполнена, если условие не
  соблюдается. Она всегда в паре с оператором if :

  ```
  int a, b;
  cin >> a >> b;
  if (a == b)
    cout << "equal"s << endl;
  else
    cout << "not equal"s << endl;
  ```

  Когда при выполнении условия после ```if``` или ```else``` должно быть несколько
  действий, эти действия нужно заключить внутрь фигурных скобок:

  ```
  int a, b;
  cin >> a >> b;
  if (a == b) {
    // Фигурные скобки нужны, когда надо выполнить несколько команд
    cout << "equal"s << endl;
    cout << a << endl;
  } else {
    cout << "not equal"s << endl;
    cout << a << " "s << b << endl;
  }
  ```

  Когда условий несколько, их можно соединить, не используя фигурные скобки. Для
  этого нужна конструкция ```else if``` :

  ```
  if ( <условие 1> ) {
  // ...
  } else if ( <условие 2> ) {
  // ...
  } else {
  // ...
  }
  ```

##Логические операции: сравнение
  Результат операции сравнения — логическое выражение. Логическими называют
  выражения, результат которых равен ```true``` или ```false``` .
  
  Операторы сравнения целых чисел:
  * ```==``` (равно),
  
  * ```!=``` (неравно),
  
  * ```<``` (меньше),
  
  * ```<=``` (меньше или равно),
  
  * ```>``` (больше),

  * ```>=``` (больше или равно).

  Целые числа можно сравнивать с вещественными. Перед сравнением целое
  число неявно будет преобразовано в соответствующее ему вещественное:
  
  ```
  int x = 1;
  double y = 1.2;
  x < 1;
  y >= 2.5;
  x == y;
  ```
  
  Строки сравниваются лексикографически — строка ```a``` меньше строки ```b``` , потому
  что буква “f“ стоит в английском алфавите раньше буквы “w“:
  
  ```
  #include <iostream>
  #include <string>
  using namespace std;
  int main() {
    string a = "fire"s;
    string b = "water"s;
    if (a < b) {
      cout << "a is less than b"s << endl;
    }
  }
  ```
  На экране появится сообщение “ ```a``` is less than ```b``` ”.
  Регистр символов имеет значение: например, строки "apple" и "APPLE" — разные.
  
  ## Логические операции «и», «или», «не»
  
  * ```&&``` (конъюнкция) — логическая операция «и». Выражение ```a & b``` возвращает
    ```true``` , если истинно и ```a``` , и ```b``` . В противном случае вернёт ```false``` .
    
  * ```||``` (дизъюнкция) — логическая операция «или». Выражение ```a || b```
    возвращает ```true``` , если истинно хотя бы одно из ```a``` и ```b``` . В противном случае
    вернёт ```false``` .
    
  * ```!``` (отрицание) — логическая операция «не». Выражение ```!a``` возвращает
    ```false``` , если ```a``` истинно. В противном случае вернёт ```true``` .


## Циклы while и do-while
  Чтобы программа выполняла действие, пока есть некоторое условие, используют
  цикл ```while``` :
  
  ```
  #include <iostream>
  using namespace std;
  int main() {
    int n;
    cin >> n;
    int sum = 0;
    int i = 1;
    while (i <= n) {
      sum += i;
      ++i;
    }
    cout << sum << endl;
  }
```

  В цикле ```while``` условие продолжения цикла проверяется в самом начале, поэтому
  тело цикла может не выполниться ни разу, если условие будет изначально
  ложным.
  
  В цикле ```do-while``` тело цикла выполняется хотя бы один раз, так как условие
  продолжения цикла выполняется в конце. 
  
## Цикл for
  
  Цикл ```for``` используется, когда вы точно знаете, сколько раз действие должно
  повториться.

  ```
  for (int i = 0; i != 3; i += 1) {
    cout << "Check the fridge"s << endl;
  }
  ```
  
  В записи шага цикла часто используют короткие варианты для ```i += 1``` :
  
  * ```++i``` — префиксный инкремент,
  * ```i++``` — постфиксный инкремент
  
  ## Выход из цикла
  
    Чтобы программа перешла на следующий шаг цикла , применяют оператор
    ```continue``` :

```
    string str = "Drawing indices for fun and profit"s;
    int num_iters = 0;
    // считаем с клавиатуры, сколько раз мы бы хотели повторить цикл
    cin >> num_iters;
    for (int i = 0; i < num_iters; ++i) {
      int index1, index2;
      // считаем индексы
      cin >> index1 >> index2;
      // если index1 отрицательный или больше, чем длина нашей строки,
      // то продолжать этот шаг цикла невозможно
      if (index1 < 0 || index1 >= str.size()) {
      // скомандовав continue, программист просит перейти на следующую итерацию,
      // не заканчивая текущую
      continue;
      }
      // аналогичная логика для второго индекса
      if (index2 < 0 || index2 >= str.size()) {
      continue;
      }
      // выведем результат сравнения символов строки по указанным индексам
      cout << (str[index1] == str[index2]) << endl;
    }

  ```
  
    Чтобы выйти из цикла досрочно, используют оператор ```break```:
    
    ```
    #include <iostream>
    #include <string>
    using namespace std;
    int main() {
      string animal;
      // считаем название животного
      cin >> animal;
      for (int i = 0; i < animal.size(); ++i) {
    // если текущая буква строки - а,
        if (animal[i] == 'a') {
          // то выведем индекс i на экран и закончим цикл
          cout << i << endl;
          break;
        }
      }
    
    cout << "Yes"s<< endl;
    }
```
