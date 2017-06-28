Описание классов php расширения BrowserExt
==========================================

class PhpBrowser
----------------

### свойство downloadDirectory

`public $downloadDirectory;`

Задает директорию куда будут автоматически скачиваться файлы, если
браузер получит запрос на скачивание. Такое происходит, например, при
клике на ссылку на файл. По-умолчанию равно:

    __DIR__.'/download'



### свойство proxyCheckThreads

`public $proxyCheckThreads = 5;`

Задает количество потоков для тестирования прокси-серверов.
По-умолчнию равно 5.



### метод __construct()

`public __construct();`

Конструктор.



### метод load

`public bool load(string $url[, bool $samewnd=false[, long $timeout=0]]);`

Загружает страницу по url. $samewnd определяет, будет ли
страница загружаться в той же вкладке, или в новой. При
удачной загрузке возвращает true, иначе false. $timeout
задает время ожидания загрузки страницы, по-умолчанию время
не ограничено.



### метод title

`public string title();`

Возвращает заголовок текущей страницы.



### метод click

`public bool click(string $xpath[, bool $samewnd=false]);`

Кликает на элементе, заданном xpath. Если в результате будет
загружаться новая страница, то она будет загружаться в новой
вкладке. Для загрузки в той же вкладке установите $samewnd = true.
При удачной загрузке возвращает true, иначе false.



### метод elements

`public array elements(string $xpath);`

Делает выборку элементов документа по xpath. Возвращает массив объектов
класса PhpWebElement. Если ни одного элемента не найдено
возвращает пустой массив.



### метод download

`public int download(string $url, string $dest);`

Скачивает файл по url. $dest - путь для сохранения, включая
имя файла. Возвращает 0 если произошла ошибка и 1 если скачивание
прошло успешно.



### метод back

`public back();`

Переходит к предыдущей вкладке. Текущая вкладка закрывается.



### метод wait

`public wait(int $seconds);`

Ждет некоторое время, заданное в параметре $seconds.



### метод scroll

`public bool scroll(int $screens);`

Вертикально прокручивает страницу на количество экранов, заданных
параметром $screens. Размер экрана определяется размером
окна браузера. В случае успешной прокрутки возвращает true.
Если достигнут конец страницы, возвращается false.

Эту функцию можно использовать для страниц, которые динамически
подгружают содержимое при достижении конца страницы. Алгоритм может
быть следующий:

    $res = true;
    for ($i=0; $i<500 && $res; $i++)
    {
        $res = $browser->scroll(1);
        if (!$res)
        {
            $browser->wait(3);
            $res = $browser->scroll(1);
        }
    }


### метод fill

`public bool fill(string $xpath, string $value);`

Заполняет элемент input типа text или textarea значением $value.
Элемент выбирается по xpath. Если xpath возвращает несколько
элементов, берется только первый.

Если элемент найден возвращается true, иначе false.



### метод fill2

`public bool fill2(string $xpath, string $value);`

Заполняет элемент input типа text или textarea значением $value
посредством посылки ему события нажатия клавиатуры. В этом случае
корректно срабатывают все javascript обработчики и прочее.
Элемент выбирается по xpath. Если xpath возвращает несколько
элементов, берется только первый.

Если элемент найден возвращается true, иначе false.



### метод check

`public bool check(string $xpath);`

Устанавливает checkbox, заданный xpath выражением.
Если элемент найден возвращается true, иначе false.



### метод uncheck

`public bool uncheck(string $xpath);`

Сбрасывает checkbox, заданный xpath выражением.
Если элемент найден возвращается true, иначе false.



### метод radio

`public bool radio(string $xpath);`

Устанавливает элемент radio, заданный xpath выражением.

Если элемент найден возвращается true, иначе false.



### метод select

`public bool select(string $xpath);`

Устанавливает элемент select. Параметр $xpath задает элемент
c тегом option, который будет выбран. 

Если элемент найден возвращается true, иначе false.



### метод selectByText

`public bool selectByText(string $xpath, string $text);`

Устанавливает элемент select, заданный xpath выражением.
$text задает текст, который следует выбрать.

Если элемент найден возвращается true, иначе false.



### метод selectByValue

`public bool selectByValue(string $xpath, string $value);`

Устанавливает элемент select, заданный xpath выражением.
$value определяет значение аттрибута value элемента option,
который следует выбрать.

Если элемент найден возвращается true, иначе false.



### метод fillfile

`public bool fillfile(string $xpath, string $value);`

Заполняет элемент input типа файл значением $value.
Элемент выбирается по xpath. Если xpath возвращает несколько
элементов, берется только первый.

Если элемент найден возвращается true, иначе false.



### метод setProxyList

`public int setProxyList(array $proxies[, bool ischeck=true]);`

Устанавливает список прокси-серверов, которые будут использоваться
при загрузке страниц и файлов. Параметр $ischeck определяет, будут ли
тестироваться прокси. Список прокси-серверов задается массивом строк,
каждая строка задает отдельный сервер, например

    $proxies = array('192.168.0.2:3128', 'user:psw@example.com:8080');

Количество потоков для тестирования прокси-серверов задается свойством
proxyCheckThreads.



### метод proxyList

`public array proxyList();`

Возвращает массив прокси-серверов, используемых браузером.
Если проводилось тестирование прокси, то возвращаются только
рабочие.



### метод html

`public string html();`

Возвращает html текущей страницы.



### метод show

`public show();`

Показывает окно браузера.



### метод hide

`public hide();`

Скрывает окно браузера.



### метод url

`public string url();`

Возвращает url текущей страницы браузера.



### метод requestedUrl

`public string requestedUrl();`

Возвращает запрошенный url текущей страницы браузера.



### метод setHtml

`public setHtml(string $html);`

Устанавливает html текущей страницы.



### метод setImageLoading

`public setHtml(bool isloadimage);`

Задает флаг - загружать ли картинки.



### метод gettext

`public gettext(string xpath);`

Выбирает элементы по xpath и возвращает
их текстовое содержимое.

Возвращает массив строк.



### метод getlink

`public getlink(string xpath);`

Выбирает элементы по xpath и возвращает
их свойство href.

Возвращает массив строк.



### метод getimglink

`public getimglink(string xpath);`

Выбирает элементы по xpath и возвращает
их свойство src.

Возвращает массив строк.



### метод getattr

`public getattr(string xpath, string attrname);`

Выбирает элементы по xpath и возвращает
их атрибут, заданный параметром attrname.

Возвращает массив строк.



### метод console

`public console();`

Возвращает строку - содержание консольного вывода javascript.



### метод clearConsole

`public clearConsole();`

Очищает содержание консольного вывода javascript.



### метод getCookies

`public getCookies();`

Возвращает ассоциативный массив с названиями и значениями
куков для текущей страницы.



### метод clearCookies

`public clearCookies();`

Очищает все куки для всех страниц.



### метод setCookiesForUrl

`public setCookiesForUrl(string url, array cookies);`

Устанавливает куки для заданного url. Ассоциативный массив
cookies содержит ключи (названия куков) и значения (значения куков)
только в текстовом виде (тип string), иначе будет ошибка.



### метод getCurrentProxy

`public getCurrentProxy();`

Возвращает строку - текущий используемый прокси.



### метод setUserAgent

`public setUserAgent(string useragent);`

Устанавливает UserAgent. Если нужно опять использовать
дефолтный - передайте пустую строку.





class PhpWebElement
-------------------

### метод attr

`public string attr(string $name);`

Возвращает значение аттрибута по его имени.
Если аттрибут не найден возвращается пустая строка.



### метод attrAll

`public array attrAll();`

Возвращает ассоциативный массив имя=>значение всех аттрибутов
элемента.



### метод tagName

`public string tagName();`    

Возвращает тэг элемента.



### метод prop

`public string prop(string $name);`

Возвращает значение свойства элемента по имени.
Свойства элементов определяются моделью DOM документа.



### метод textAll

`public string textAll();`

Возвращает значение всех вложенных текстовых дочерних
узлов элемента. Например, элемент $el1 имеет следующий html:

    <div>abc<p>123</p>345</div>

Тогда textAll() этого элемента вернет

    abc 123 345



### метод text

`public string text();`

Возвращает текстовое значение только тех текстовых узлов,
которые являются непосредственными потомками данного элемента.
Например, элемент $el1 имеет следующий html:

    <div>abc<p>123</p>345</div>

Тогда text() этого элемента вернет

    abc 345



### метод html

`public string html();`

Возвращает inner html элемента.



### метод getXPath

`public string getXPath();`

Возвращает xpath элемента.



### метод parent

`public PhpWebElement parent();`

Возвращает родительский элемент. Если родительского
элемента нет, то метод isNull возвращаемого элемента
будет равен true.


 
### метод nextSibling

`public PhpWebElement nextSibling();`

Возвращает следующий элемент по отношению к данному
в списке дочерних элементов родителя. Если элемент
последний, то метод isNull возвращаемого PhpWebElement
будет равен true.

    while (!$el->isNull())
        $el = $el->nextSibling();



### метод prevSibling

`public PhpWebElement prevSibling();`

Возвращает предыдущий элемент по отношению к данному
в списке дочерних элементов родителя. Если элемент
первый, то метод isNull возвращаемого PhpWebElement
будет равен true.

    while (!$el->isNull())
        $el = $el->prevSibling();



### метод firstChild

`public PhpWebElement firstChild();`

Возвращает первый дочерний элемент в списке дочерних
элементов. Если дочерних элементов нет, то метод isNull
возвращаемого элемента будет равен true.



### метод lastChild

`public PhpWebElement lastChild();`

Возвращает последний дочерний элемент в списке дочерних
элементов. Если дочерних элементов нет, то метод isNull
возвращаемого элемента будет равен true.



### метод isNull

`public bool isNull();`

Возвращает false если это нормальный элемент, или
true если это NULL элемент, т.е. элемент отсутствует.
Смотрите описание методов parent, nextSibling, prevSibling,
firstChild, lastChild. 



### метод elements

`public array elements(string $xpath);`

Выполняет xpath относительно данного элемента и возвращает
массив объектов класса PhpWebElement. Если элементы не найдены
возвращается пустой массив. Например, чтобы выбрать все ссылки
внутри элемента $el1 можно написать:

    $el1->elements('.//a');

Точка задает текущий контекст.



### метод click

`public bool click();`

Делает клик на элементе. Возвращает true при успешном
выполнении, например, если новая страница загрузилась,
иначе выдает false.


