# Array

>Массив дар JavaScript рӯйхати тартибёфтаи элементҳо бо индекси муайян (калиди онҳо) мебошад. Вақте ки мо мехоҳем рӯйхати унсурҳои муайянро нигоҳ дорем ва сипас ба онҳо бо як тағирёбанда дастрасӣ пайдо кунем, ҳамон вақт мо массивро истифода мебарем. Баръакси забонҳои дигар, ки дар он массив истинод ба тағирёбандаҳои сершумор аст, дар JavaScript он ягона тағирёбандаест, ки метавонад унсурҳои сершуморро нигоҳ дорад.
>
>Массив в JavaScript — это упорядоченный список элементов с указанным индексом (ключом к ним). Когда мы хотим сохранить список определенных элементов, а затем получить к ним доступ с помощью одной переменной, именно тогда применяем массив. В отличие от остальных языков, где массив — это ссылка на несколько переменных, в JavaScript — это единственная переменная, в которой может храниться несколько элементов.

# Методы массивов

## Добавление/удаление элементов

>arr.push(...items) – добавляет элементы в конец arr.pop() – извлекает элемент из конца arr.shift() – извлекает элемент из начала arr.unshift(...items) – добавляет элементы в начало.

### splice

>Как удалить элемент из массива?

Так как массивы – это объекты, то можно попробовать delete:

>arr.splice(index[, deleteCount, elem1, ..., elemN]) let arr = ["Я", "изучаю", "JavaScript"];

arr.splice(1, 1); // начиная с позиции 1, удалить 1 элемент

alert( arr ); // осталось ["Я", "JavaScript"]

>let arr = ["Я", "изучаю", "JavaScript", "прямо", "сейчас"];

// удалить 3 первых элемента и заменить их другими arr.splice(0, 3, "Давай", "танцевать");

alert( arr ) // теперь ["Давай", "танцевать", "прямо", "сейчас"]

>let arr = ["Я", "изучаю", "JavaScript", "прямо", "сейчас"];

// удалить 2 первых элемента let removed = arr.splice(0, 2);

alert( removed ); // "Я", "изучаю" <-- массив из удалённых элементов

>let arr = ["Я", "изучаю", "JavaScript"];

// с позиции 2 // удалить 0 элементов // вставить "сложный", "язык" arr.splice(2, 0, "сложный", "язык");

alert( arr ); // "Я", "изучаю", "сложный", "язык", "JavaScript"

## slice

>Метод arr.slice намного проще, чем похожий на него arr.splice.

Его синтаксис:

arr.slice([start], [end]) Он возвращает новый массив, в который копирует элементы, начиная с индекса start и до end (не включая end). Оба индекса start и end могут быть отрицательными. В таком случае отсчёт будет осуществляться с конца массива.

Это похоже на строковый метод str.slice, но вместо подстрок возвращает подмассивы.

Например:

let arr = ["t", "e", "s", "t"];

alert( arr.slice(1, 3) ); // e,s (копирует с 1 до 3)

alert( arr.slice(-2) ); // s,t (копирует с -2 до конца) Можно вызвать slice и вообще без аргументов: arr.slice() создаёт копию массива arr. Это часто используют, чтобы создать копию массива для дальнейших преобразований, которые не должны менять исходный массив.

## concat

>Метод arr.concat создаёт новый массив, в который копирует данные из других массивов и дополнительные значения.

Его синтаксис:

arr.concat(arg1, arg2...)

## Перебор: forEach

>Метод arr.forEach позволяет запускать функцию для каждого элемента массива. ["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => { alert(${item}  ${index} ${array}); });

# Поиск в массиве

## indexOf/lastIndexOf и includes

>Методы arr.indexOf, arr.lastIndexOf и arr.includes имеют одинаковый синтаксис и делают по сути то же самое, что и их строковые аналоги, но работают с элементами вместо символов:

arr.indexOf(item, from) ищет item, начиная с индекса from, и возвращает индекс, на котором был найден искомый элемент, в противном случае -1. arr.lastIndexOf(item, from) – то же самое, но ищет справа налево. arr.includes(item, from) – ищет item, начиная с индекса from, и возвращает true, если поиск успешен.

>const arr = [NaN]; alert( arr.indexOf(NaN) ); // -1 (должен быть 0, но === проверка на равенство не работает для NaN) alert( arr.includes(NaN) );// true (верно)

# find и findIndex

>Представьте, что у нас есть массив объектов. Как нам найти объект с определённым условием?

Здесь пригодится метод arr.find.

Его синтаксис таков:

let result = arr.find(function(item, index, array) { // если true - возвращается текущий элемент и перебор прерывается // если все итерации оказались ложными, возвращается undefined }); Функция вызывается по очереди для каждого элемента массива:

item – очередной элемент. index – его индекс. array – сам массив. Если функция возвращает true, поиск прерывается и возвращается item. Если ничего не найдено, возвращается undefined.

>Например, у нас есть массив пользователей, каждый из которых имеет поля id и name. Попробуем найти того, кто с id == 1:

let users = [ {id: 1, name: "Вася"}, {id: 2, name: "Петя"}, {id: 3, name: "Маша"} ];

let user = users.find(item => item.id == 1);

alert(user.name); // Вася

# filter

>Метод find ищет один (первый попавшийся) элемент, на котором функция-колбэк вернёт true.

На тот случай, если найденных элементов может быть много, предусмотрен метод arr.filter(fn).

Синтаксис этого метода схож с find, но filter возвращает массив из всех подходящих элементов:

let results = arr.filter(function(item, index, array) { // если true - элемент добавляется к результату, и перебор продолжается // возвращается пустой массив в случае, если ничего не найдено }); Например:

let users = [ {id: 1, name: "Вася"}, {id: 2, name: "Петя"}, {id: 3, name: "Маша"} ];

// возвращает массив, состоящий из двух первых пользователей let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2 Преобразование массива Перейдём к методам преобразования и упорядочения массива.

# map

Метод arr.map является одним из наиболее полезных и часто используемых.

Он вызывает функцию для каждого элемента массива и возвращает массив результатов выполнения этой функции.

Синтаксис:

let result = arr.map(function(item, index, array) { // возвращается новое значение вместо элемента }); Например, здесь мы преобразуем каждый элемент в его длину:

let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length); alert(lengths); // 5,7,6

# Sort(fn)

>Вызов arr.sort() сортирует массив на месте, меняя в нём порядок элементов.

Он возвращает отсортированный массив, но обычно возвращаемое значение игнорируется, так как изменяется сам arr.

Например:

let arr = [ 1, 2, 15 ];

// метод сортирует содержимое arr arr.sort();

alert( arr ); // 1, 15, 2 Не заметили ничего странного в этом примере?

Порядок стал 1, 15, 2. Это неправильно! Но почему?

По умолчанию элементы сортируются как строки.

Буквально, элементы преобразуются в строки при сравнении. Для строк применяется лексикографический порядок, и действительно выходит, что "2" > "15".

Чтобы использовать наш собственный порядок сортировки, нам нужно предоставить функцию в качестве аргумента arr.sort().

Функция должна для пары значений возвращать:

function compare(a, b) { if (a > b) return 1; // если первое значение больше второго if (a == b) return 0; // если равны if (a < b) return -1; // если первое значение меньше второго } Например, для сортировки чисел:

function compareNumeric(a, b) { if (a > b) return 1; if (a == b) return 0; if (a < b) return -1; }

let arr = [ 1, 2, 15 ];

arr.sort(compareNumeric);

alert(arr); // 1, 2, 15 Теперь всё работает как надо.

Давайте возьмём паузу и подумаем, что же происходит. Упомянутый ранее массив arr может быть массивом чего угодно, верно? Он может содержать числа, строки, объекты или что-то ещё. У нас есть набор каких-то элементов. Чтобы отсортировать его, нам нужна функция, определяющая порядок, которая знает, как сравнивать его элементы. По умолчанию элементы сортируются как строки.

Метод arr.sort(fn) реализует общий алгоритм сортировки. Нам не нужно заботиться о том, как он работает внутри (в большинстве случаев это оптимизированная быстрая сортировка или Timsort). Она проходится по массиву, сравнивает его элементы с помощью предоставленной функции и переупорядочивает их. Всё, что остаётся нам, это предоставить fn, которая делает это сравнение.