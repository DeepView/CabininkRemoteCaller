# **项目说明（Project Desperation）**

> - **注意：如果这份文档出现了其他自然语言，则这些语言的翻译结果由机器翻译提供！**
> - **Note: if other natural languages appear in this document, the translation results of these languages are provided by machine translation!**
> - **注意：この文書に他の自然言語が現れたら、これらの言語の翻訳結果は機械翻訳によって提供されます。**
> - **Примечание: если этот документ составлен на других природных языках, то результат перевода на эти языки обеспечивается машинным переводом!**

---
## 标签（Tags）

> - 基于 .Net Stardand 的项目（Project based on .Net stardand；ベース .Net Stardand の項目；Проект на базе .Net Stardand）
> - Router 架构（Router architecture；Routerアーキテクチャ；Router архитектура）

---
## 类说明（Class's Desperation）

类名称（Class Name，クラスの名前，название класса）|概述（Summary，概要，Общее описание）
-----------------------------------------------|---------------------------------
RemoteCaller|用于实现远程调用的Router简易实现类（Router simple implementation class for remote call；リモート呼び出しを実現するためのRouter簡易実現類；исполняемый класс Router для удалённого вызова）。
IRemoteCallProtocol&lt;T&gt;|用于规范RemoteCall的被调用方的基础访问API的接口（The interface used to standardize the callee's underlying access API for remotecall；RemoteCallを規範化するための被呼加入者の基礎アクセスAPIのインターフェース；интерфейс API, используемый для регулирования доступа к основам Remote Call）。
CodeExecutedTimestampResult|用于描述代码执行所需时间的时间戳返回结果的类，基于IDisposable接口实现，如果您在控制台应用程序或者应用程序调试过程中需要使用此类，可以考虑使用IDisposable接口模式进行访问（The class used to describe the time stamp return result of code execution. It is implemented based on the IDisposable interface. If you need to use this class during console application or application debugging, you can consider using the IDisposable interface mode for access；コードの実行に要するタイムスタンプの結果を記述するクラスは、IDisposableインターフェースに基づいて実現されます。コンソールアプリケーションやアプリケーションのデバッグ中にこのようなものが必要であれば、IDisposableインターフェースモードを使ってアクセスすることが考えられます。；для описания периода, необходимого для выполнения кода, введите время для возвращения результатов класса, основанного на интерфейсе IDisposable, если вы хотите использовать это в консольных приложениях или в процессе отладки приложений, можно рассмотреть возможность использования режима интерфейса IDisposable）。
SchemeNotMatchedException|当URL的方案名称不匹配时需要抛出的异常（Exception to be thrown when the scheme name of the URL does not match；URLのソリューション名が一致しない場合は、スローする必要があります。；ошибка, которую необходимо выбрасывать, если имя программы не совпадает）。
NotSupportedTypeException|当所属类型不支持时需要抛出的异常（Exception to be thrown when the owning type is not supported；当所属のタイプがサポートされていない場合は、投げられる異常があります。；ошибка, которую необходимо выбросить, если тип не поддерживается）。

---
## 简易教学（Simple Teaching）

这个类常用于远程访问某个地址，或者调用本地程序集的接口，在使用这个类之前，说先要进行单例化：
```csharp
RemoteCaller router = RemoteCaller.CreateInstance();
```
当然你可以在访问CreateInstance方法指定更加详细的参数（Of course, you can specify more detailed parameters in the CreateInstance method；もちろんCreateInstanceにアクセスして、より詳細なパラメータを指定できます。；Конечно, вы можете указать более подробные параметры доступа к CreateInstance）。

如果你需要打开一个Web页面，那么可以通过以下方式进行访问，然后将会得到一个存放Web页面的HTML代码或者请求的Json代码的字符串（If you need to open a web page, you can access it in the following ways, and then you will get a string of HTML code for the web page or JSON code for the request；Webページを開く必要があるなら、次のようにアクセスして、WebページのHTMLコードまたは要求されたJsonコードを格納した文字列を得ることができます。；если вам необходимо открыть веб - страницу, то доступ можно получить следующим образом: будет получен код HTML для веб - страницы или запрошенный код Json）：
```csharp
string original = @"https://visualstudio.microsoft.com/zh-hans/";
Uri webUrl = new Uri(original);
Console("Result:\n\n{0}", router.Via(webUrl, out HttpStatusCode code));
```
当然如果你不需要获取Via方法捕获到的HTTP状态码，则可以替换为这个方法的重载版本（Of course, if you don't need to get the HTTP status code captured by Via method, you can replace it with the overloaded version of this method；もちろん、Via方式で取り込まれたHTTP状態コードを取得する必要がないなら、この方法のリロードバージョンに置き換えることができる。；Конечно, если вы не хотите получить код состояния на HTTTP с помощью метода Via, то вы можете заменить его повторенной версией этого метода）：
```csharp
Uri webUrl = new Uri(@"https://visualstudio.microsoft.com/zh-hans/");
object obj = router.Via(webUrl);
```
如果你需要访问一个FTP、本地文件或者本地目录，那么，只需要将上面代码中string变量original的值替换掉即可，比如说（If you need to access an FTP, local file or local directory, just replace the original value of the string variable in the above code, for example；FTP、ローカルファイルまたはローカルディレクトリにアクセスする必要があるなら、上のコードの中のstring変数origginnalの値を置き換えるだけでいいです。；если вам необходимо получить доступ к файлу FTP, локальному файлу или локальному каталогу, то нужно просто заменить значение переменной string из указанного выше кода на original, например）：
```csharp
string original = @"C:\Windows\System32\Notepad.exe";
```
Via方法支持通过URL的方式访问程序集（当前程序集或者指定的程序集）中的公开的静态方法，一般要实现其有效访问，需要为其对应的实例附加一个Protocol（Via method supports accessing public static methods in assembly (current assembly or specified assembly) through URL. In general, to achieve effective access, you need to attach a protocol to its corresponding instance；Via方法は、URLによってプログラムセット（現在のプログラムセットまたは指定されたプログラムセット）にアクセスするための開示された静的な方法をサポートしており、一般的に、その有効なアクセスを実現するには、その対応するインスタンスにプロトールを追加する必要がある。；метод Via поддерживает открытые статические методы доступа через URL (текущий набор программ или указанный набор программ), для чего, как правило, требуется дополнительный протокол к соответствующему экземпляру）。

值得说明的是，每一个类的Protocol类，其类名称后面必须是Protocol结尾，且必须实现IRemoteCallProtocol接口。比如说存在如下一个User类（It is worth noting that for each class's Protocol class, the class name must be followed by the end of Protocol, and the IRemoteCallProtocol interface must be implemented. For example, there is a User class；説明に値するのは、各クラスのProtocl類は、そのクラス名の後にProtocolが終端しなければならず、IRemoteCallProtocolインターフェースを実現しなければならない。例えば次のようなUser類があります。Следует отметить, что каждая категория, относящаяся к категории Protocol, должна иметь название, которое должно быть указано в конце протокола, и должна иметь интерфейс IRemoteCallProtocol.  например, существует следующая категория пользователей）：
```csharp
public class User
{
    private int _id;
    private string _name;
    public User(int id, string name)
    {
       _id = id;
       _name = name;
    }
    public override string ToString() => $"User[Id={_id};Name={_name}]";
 }
```
那么我们就要为这个User类实现一个UserProtocol类，并实现IRemoteCallProtocol接口，示例代码如下（Then we need to implement a UserProtocol class for this User class and the IRemoteCallProtocol interface. The example code is as follows；このUserクラスのためにUserProtocolクラスを実現し、IRemoteCallProtocolインターフェースを実現します。コード例は以下の通りです。；Итак, мы должны ввести класс UserProtocol для этого класса и выполнить IRemoteCallProtocol интерфейс, пример кода ниже）：
```csharp
public class UserProtocol : IRemoteCallProtocol<User>
{
    public User Ctor(IDictionary<string, object> parameters)
    {
       bool isGotId = parameters.TryGetValue("id", out object id);
       bool isGotName = parameters.TryGetValue("name", out object name);
       User usr = new User(Convert.ToInt32(id), Convert.ToString(name));
       return usr;
    }
    public static User Init(IDictionary<string, object> parameters)
    {
       UserProtocol userProtocol = new UserProtocol();
       return userProtocol.Ctor(parameters);
    }
 }
```
> - 注意，需要通过URL访问的接口必须为静态接口（Note that the interface to be accessed through the URL must be a static interface；なお、URLを介してアクセスする必要があるインターフェースは、静的インターフェースでなければならない。；обратите внимание, что интерфейс, требующий доступа через URL, должен быть статическим интерфейсом）！

当我们需要通过一个URL初始化一个User实例的时候，那么就可以通过下面的代码实现（When we need to initialize a User instance through a URL, we can do this through the following code；私たちは一つのURLを通じてUserのインスタンスを初期化する必要がある場合、以下のコードを通じて実現することができる。；если необходимо инициализировать User экземпляр через URL, то это можно сделать с помощью следующего кода）：
```csharp
RemoteCaller router = RemoteCaller.CreateInstance(Assembly.GetExecutingAssembly());
string original = @"app://Namespace.User/Init?id=0&amp;name=cabinink";
Uri nativebUrl = new Uri(original);
object obj = router.Via(nativeUrl, out HttpStatusCode code);
Console.WriteLine("{0}", obj.ToString());
```
在上述代码呈现的链接里面，Namespace表示User类所在的命名空间，假设User类在MyApp.Core命名空间下，那么你的链接应该替换成如下所示（In the link shown in the above code, the Namespace represents the namespace where the user class is located. If the User class is under the MyApp.Core namespace, then your link should be replaced as follows；上記のコードが提示されているリンクの中で、NamespaceはUser類が存在する名前空間を表しています。もしUser類がMyApp.Coreの名前空間にあると仮定すれば、あなたのリンクは以下のように置き換えられます。；в ссылке, приведенной выше, Namespace указывает, что класс User находится в пространстве имён, и если класс User находится в пространстве имён MypApp.Core, то ссылку следует заменить следующей:）：
```csharp
string original = @"app://MyApp.Core.User/Init?id=0&name=cabinink"
```
最后需要注意的是，一定要区分这类URL的字符串大小写（Finally, it should be noted that the case of such URLs should be distinguished；最後に注意したいのは、このようなURLの文字列の大きさと書き方を区別しなければなりません。；Наконец, следует отметить, что необходимо различать размер строк для таких URL）。