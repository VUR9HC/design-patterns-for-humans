<br>
<p align="center">
  <img src="./.github/banner.svg" height="150px" />
</p>

***

<p align="center">
🎉 Giải thích siêu đơn giản về design patterns! 🎉
</p>
<p align="center">
Một chủ đề rất dễ làm bất kỳ ai rối trí. Ở đây tôi cố gắng giúp chúng in sâu vào<br> tâm trí bạn (và có lẽ cả của tôi nữa) bằng cách giải thích chúng theo cách <i>đơn giản</i> nhất có thể.
</p>

***

<sub>Hãy xem [dự án khác](http://roadmap.sh) của tôi và ghé [Twitter](https://twitter.com/kamrify) để nói "xin chào".</sub>

<br>

|[Creational Design Patterns](#creational-design-patterns)|[Structural Design Patterns](#structural-design-patterns)|[Behavioral Design Patterns](#behavioral-design-patterns)|
|:-|:-|:-|
|[Simple Factory](#-simple-factory)|[Adapter](#-adapter)|[Chain of Responsibility](#-chain-of-responsibility)|
|[Factory Method](#-factory-method)|[Bridge](#-bridge)|[Command](#-command)|
|[Abstract Factory](#-abstract-factory)|[Composite](#-composite)|[Iterator](#-iterator)|
|[Builder](#-builder)|[Decorator](#-decorator)|[Mediator](#-mediator)|
|[Prototype](#-prototype)|[Facade](#-facade)|[Memento](#-memento)|
|[Singleton](#-singleton)|[Flyweight](#-flyweight)|[Observer](#-observer)|
||[Proxy](#-proxy)|[Visitor](#-visitor)|
|||[Strategy](#-strategy)|
|||[State](#-state)|
|||[Template Method](#-template-method)|

<br>

Giới thiệu
=================

Design patterns là lời giải cho những vấn đề lặp đi lặp lại; **những hướng dẫn về cách xử lý một số vấn đề nhất định**. Chúng không phải là class, package hay library mà bạn có thể cắm vào ứng dụng rồi chờ phép màu xảy ra. Đúng hơn, chúng là những hướng dẫn về cách giải quyết một số vấn đề trong những tình huống nhất định.

> Design patterns là lời giải cho những vấn đề lặp đi lặp lại; những hướng dẫn về cách xử lý một số vấn đề nhất định

Wikipedia mô tả chúng như sau

> Trong kỹ nghệ phần mềm, một software design pattern là một giải pháp tổng quát có thể tái sử dụng cho một vấn đề thường gặp trong một ngữ cảnh cụ thể của thiết kế phần mềm. Nó không phải là một thiết kế hoàn chỉnh có thể chuyển trực tiếp thành source code hay machine code. Nó là một mô tả hoặc khuôn mẫu về cách giải quyết một vấn đề có thể được dùng trong nhiều tình huống khác nhau.

⚠️ Cẩn thận
-----------------
- Design patterns không phải là viên đạn bạc cho mọi vấn đề của bạn.
- Đừng cố ép áp dụng chúng; nếu làm vậy thì rất dễ có chuyện tệ xảy ra. 
- Hãy nhớ rằng design patterns là lời giải **cho** vấn đề, không phải lời giải **đi tìm** vấn đề; vì vậy đừng suy diễn quá mức.
- Nếu được dùng đúng chỗ, đúng cách, chúng có thể trở thành cứu tinh; còn không thì có thể biến code của bạn thành một mớ hỗn độn kinh khủng.

> Cũng lưu ý rằng các ví dụ code bên dưới dùng PHP-7, nhưng điều đó không nên cản trở bạn vì các khái niệm thì vẫn như nhau.

Các loại design patterns
-----------------

* [Creational](#creational-design-patterns)
* [Structural](#structural-design-patterns)
* [Behavioral](#behavioral-design-patterns)

Creational Design Patterns
==========================

Nói đơn giản
> Các pattern creational tập trung vào cách khởi tạo một object hoặc một nhóm object có liên quan với nhau.

Wikipedia nói
> Trong kỹ nghệ phần mềm, creational design patterns là các design patterns xử lý cơ chế tạo object, cố gắng tạo object theo cách phù hợp với tình huống. Cách tạo object cơ bản có thể dẫn đến các vấn đề thiết kế hoặc làm tăng độ phức tạp của thiết kế. Creational design patterns giải quyết vấn đề này bằng cách kiểm soát việc tạo object theo một cách nào đó.

 * [Simple Factory](#-simple-factory)
 * [Factory Method](#-factory-method)
 * [Abstract Factory](#-abstract-factory)
 * [Builder](#-builder)
 * [Prototype](#-prototype)
 * [Singleton](#-singleton)

🏠 Simple Factory
--------------
Ví dụ thực tế
> Hãy tưởng tượng bạn đang xây nhà và cần cửa. Bạn có thể tự mặc đồ thợ mộc, mang gỗ, keo, đinh và mọi dụng cụ cần thiết để làm cửa rồi bắt đầu đóng ngay tại nhà; hoặc bạn chỉ cần gọi cho factory và nhận cánh cửa hoàn thiện được giao tới, để không phải học cách làm cửa hay xử lý mớ bừa bộn đi kèm với việc đó.

Nói đơn giản
> simple factory chỉ đơn giản tạo ra một instance cho client mà không để lộ logic khởi tạo cho client

Wikipedia nói
> Trong lập trình hướng đối tượng (OOP), factory là một object dùng để tạo ra các object khác — nói chính xác hơn, factory là một function hoặc method trả về các object có prototype hoặc class khác nhau từ một lời gọi method, vốn được ngầm hiểu là `new`.

**Ví dụ lập trình**

Trước hết, chúng ta có một interface cho cửa và phần cài đặt của nó
```php
interface Door
{
    public function getWidth(): float;
    public function getHeight(): float;
}

class WoodenDoor implements Door
{
    protected $width;
    protected $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getWidth(): float
    {
        return $this->width;
    }

    public function getHeight(): float
    {
        return $this->height;
    }
}
```
Tiếp theo, chúng ta có door factory tạo cửa và trả nó về
```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```
Và sau đó có thể dùng như sau
```php
// Make me a door of 100x200
$door = DoorFactory::makeDoor(100, 200);

echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();

// Make me a door of 50x100
$door2 = DoorFactory::makeDoor(50, 100);
```

**Khi nào sử dụng?**

Khi việc tạo một object không chỉ là vài phép gán đơn giản mà còn bao gồm một số logic, thì việc đặt nó vào một factory chuyên biệt sẽ hợp lý hơn là lặp lại cùng một đoạn code ở khắp nơi.

🏭 Factory Method
--------------

Ví dụ thực tế
> Hãy xem trường hợp của một quản lý tuyển dụng. Một người không thể phỏng vấn cho mọi vị trí. Dựa trên vị trí đang tuyển, cô ấy phải quyết định và giao các bước phỏng vấn cho những người khác nhau.

Nói đơn giản
> Nó cung cấp một cách để ủy quyền logic khởi tạo cho các lớp con.

Wikipedia nói
> Trong lập trình dựa trên class, factory method pattern là một creational pattern sử dụng factory methods để giải quyết bài toán tạo object mà không cần chỉ rõ chính xác class của object sẽ được tạo. Điều này được thực hiện bằng cách tạo object thông qua việc gọi một factory method — hoặc được khai báo trong một interface và được cài đặt bởi các lớp con, hoặc được cài đặt trong một base class và có thể được các lớp dẫn xuất ghi đè — thay vì gọi constructor trực tiếp.

 **Ví dụ lập trình**

Lấy ví dụ về quản lý tuyển dụng ở trên. Trước hết, chúng ta có một interface cho người phỏng vấn và một vài phần cài đặt của nó

```php
interface Interviewer
{
    public function askQuestions();
}

class Developer implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about design patterns!';
    }
}

class CommunityExecutive implements Interviewer
{
    public function askQuestions()
    {
        echo 'Asking about community building';
    }
}
```

Bây giờ hãy tạo `HiringManager` của chúng ta

```php
abstract class HiringManager
{

    // Factory method
    abstract protected function makeInterviewer(): Interviewer;

    public function takeInterview()
    {
        $interviewer = $this->makeInterviewer();
        $interviewer->askQuestions();
    }
}

```
Giờ thì bất kỳ lớp con nào cũng có thể kế thừa nó và cung cấp người phỏng vấn phù hợp
```php
class DevelopmentManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new Developer();
    }
}

class MarketingManager extends HiringManager
{
    protected function makeInterviewer(): Interviewer
    {
        return new CommunityExecutive();
    }
}
```
và sau đó có thể dùng như sau

```php
$devManager = new DevelopmentManager();
$devManager->takeInterview(); // Output: Asking about design patterns

$marketingManager = new MarketingManager();
$marketingManager->takeInterview(); // Output: Asking about community building.
```

**Khi nào sử dụng?**

Hữu ích khi có một số xử lý chung trong một class nhưng lớp con cần dùng lại được quyết định động tại runtime. Nói cách khác, khi client không biết chính xác nó sẽ cần lớp con nào.

🔨 Abstract Factory
----------------

Ví dụ thực tế
> Mở rộng ví dụ về cửa từ Simple Factory. Tùy theo nhu cầu, bạn có thể lấy cửa gỗ từ cửa hàng cửa gỗ, cửa sắt từ cửa hàng đồ sắt hoặc cửa PVC từ cửa hàng tương ứng. Thêm nữa, bạn sẽ cần người có chuyên môn phù hợp để lắp từng loại cửa, ví dụ thợ mộc cho cửa gỗ, thợ hàn cho cửa sắt, v.v. Như bạn thấy, giờ đã có sự phụ thuộc giữa các loại cửa: cửa gỗ cần thợ mộc, cửa sắt cần thợ hàn, v.v.

Nói đơn giản
> Một factory của các factory; tức là một factory gom các factory riêng lẻ nhưng có liên quan/phụ thuộc với nhau lại mà không cần chỉ rõ các concrete class của chúng.

Wikipedia nói
> abstract factory pattern cung cấp một cách để đóng gói một nhóm các factory riêng lẻ có chung một chủ đề mà không cần chỉ rõ các concrete class của chúng

**Ví dụ lập trình**

Chuyển ví dụ về cửa ở trên sang code. Trước hết, chúng ta có interface `Door` và một vài phần cài đặt của nó

```php
interface Door
{
    public function getDescription();
}

class WoodenDoor implements Door
{
    public function getDescription()
    {
        echo 'I am a wooden door';
    }
}

class IronDoor implements Door
{
    public function getDescription()
    {
        echo 'I am an iron door';
    }
}
```
Tiếp theo, chúng ta có một số chuyên gia lắp đặt cho từng loại cửa

```php
interface DoorFittingExpert
{
    public function getDescription();
}

class Welder implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit iron doors';
    }
}

class Carpenter implements DoorFittingExpert
{
    public function getDescription()
    {
        echo 'I can only fit wooden doors';
    }
}
```

Bây giờ chúng ta có abstract factory cho phép tạo ra cả một họ object liên quan với nhau, ví dụ wooden door factory sẽ tạo cửa gỗ và chuyên gia lắp cửa gỗ, còn iron door factory sẽ tạo cửa sắt và chuyên gia lắp cửa sắt
```php
interface DoorFactory
{
    public function makeDoor(): Door;
    public function makeFittingExpert(): DoorFittingExpert;
}

// Wooden factory to return carpenter and wooden door
class WoodenDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new WoodenDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Carpenter();
    }
}

// Iron door factory to get iron door and the relevant fitting expert
class IronDoorFactory implements DoorFactory
{
    public function makeDoor(): Door
    {
        return new IronDoor();
    }

    public function makeFittingExpert(): DoorFittingExpert
    {
        return new Welder();
    }
}
```
Và sau đó có thể dùng như sau
```php
$woodenFactory = new WoodenDoorFactory();

$door = $woodenFactory->makeDoor();
$expert = $woodenFactory->makeFittingExpert();

$door->getDescription();  // Output: I am a wooden door
$expert->getDescription(); // Output: I can only fit wooden doors

// Same for Iron Factory
$ironFactory = new IronDoorFactory();

$door = $ironFactory->makeDoor();
$expert = $ironFactory->makeFittingExpert();

$door->getDescription();  // Output: I am an iron door
$expert->getDescription(); // Output: I can only fit iron doors
```

Như bạn có thể thấy, wooden door factory đã đóng gói cả `carpenter` và `wooden door`, còn iron door factory đã đóng gói cả `iron door` và `welder`. Nhờ đó, nó giúp đảm bảo rằng với mỗi cánh cửa được tạo ra, chúng ta sẽ không lấy nhầm người lắp đặt.   

**Khi nào sử dụng?**

Dùng khi có các phụ thuộc liên quan lẫn nhau cùng với logic khởi tạo không hề đơn giản.

👷 Builder
--------------------------------------------
Ví dụ thực tế
> Hãy tưởng tượng bạn đang ở Hardee's và gọi một combo cụ thể, ví dụ như "Big Hardee", rồi họ giao ngay cho bạn mà không hỏi *bất kỳ câu nào*; đó là ví dụ của simple factory. Nhưng có những trường hợp logic tạo ra sản phẩm bao gồm nhiều bước hơn. Ví dụ bạn muốn một phần Subway tùy biến, bạn có nhiều lựa chọn cho chiếc burger của mình như: muốn loại bánh mì nào? muốn loại sốt nào? muốn loại phô mai nào? v.v. Trong những trường hợp như vậy, builder pattern sẽ phát huy tác dụng.

Nói đơn giản
> Cho phép bạn tạo ra nhiều biến thể khác nhau của một object trong khi tránh làm constructor trở nên rối rắm. Hữu ích khi một object có thể có nhiều biến thể hoặc khi việc tạo object gồm rất nhiều bước.

Wikipedia nói
> builder pattern là một software design pattern cho việc tạo object với mục tiêu tìm ra lời giải cho telescoping constructor anti-pattern.

Nhân đây, hãy nói thêm một chút về telescoping constructor anti-pattern là gì. Chắc hẳn ở đâu đó chúng ta đều từng thấy một constructor như bên dưới:

```php
public function __construct($size, $cheese = true, $pepperoni = true, $tomato = false, $lettuce = true)
{
}
```

Như bạn thấy, số lượng tham số của constructor có thể nhanh chóng trở nên mất kiểm soát và rất khó hiểu thứ tự các tham số. Thêm vào đó, danh sách tham số này còn có thể tiếp tục dài ra nếu bạn muốn thêm nhiều tùy chọn trong tương lai. Đó được gọi là telescoping constructor anti-pattern.

**Ví dụ lập trình**

Giải pháp hợp lý là dùng builder pattern. Trước hết, chúng ta có chiếc burger mà mình muốn tạo

```php
class Burger
{
    protected $size;

    protected $cheese = false;
    protected $pepperoni = false;
    protected $lettuce = false;
    protected $tomato = false;

    public function __construct(BurgerBuilder $builder)
    {
        $this->size = $builder->size;
        $this->cheese = $builder->cheese;
        $this->pepperoni = $builder->pepperoni;
        $this->lettuce = $builder->lettuce;
        $this->tomato = $builder->tomato;
    }
}
```

Tiếp theo, chúng ta có builder

```php
class BurgerBuilder
{
    public $size;

    public $cheese = false;
    public $pepperoni = false;
    public $lettuce = false;
    public $tomato = false;

    public function __construct(int $size)
    {
        $this->size = $size;
    }

    public function addPepperoni()
    {
        $this->pepperoni = true;
        return $this;
    }

    public function addLettuce()
    {
        $this->lettuce = true;
        return $this;
    }

    public function addCheese()
    {
        $this->cheese = true;
        return $this;
    }

    public function addTomato()
    {
        $this->tomato = true;
        return $this;
    }

    public function build(): Burger
    {
        return new Burger($this);
    }
}
```
Và sau đó có thể dùng như sau:

```php
$burger = (new BurgerBuilder(14))
                    ->addPepperoni()
                    ->addLettuce()
                    ->addTomato()
                    ->build();
```

**Khi nào sử dụng?**

Dùng khi một object có thể có nhiều biến thể và bạn muốn tránh tình trạng constructor bị phình to. Điểm khác biệt chính so với factory pattern là: factory pattern dùng khi việc tạo là một bước duy nhất, còn builder pattern dùng khi việc tạo gồm nhiều bước.

🐑 Prototype
------------
Ví dụ thực tế
> Bạn còn nhớ Dolly chứ? Con cừu đã được nhân bản! Không cần đi sâu vào chi tiết, điểm mấu chốt ở đây là mọi thứ đều xoay quanh việc sao chép.

Nói đơn giản
> Tạo object dựa trên một object có sẵn thông qua việc clone.

Wikipedia nói
> prototype pattern là một creational design pattern trong phát triển phần mềm. Nó được dùng khi kiểu object cần tạo được xác định bởi một instance nguyên mẫu, instance này sẽ được clone để sinh ra các object mới.

Nói ngắn gọn, nó cho phép bạn tạo một bản sao của object hiện có rồi chỉnh sửa theo nhu cầu, thay vì phải vất vả tạo object từ đầu và cấu hình lại.

**Ví dụ lập trình**

Trong PHP, việc này có thể được thực hiện rất dễ dàng bằng `clone`

```php
class Sheep
{
    protected $name;
    protected $category;

    public function __construct(string $name, string $category = 'Mountain Sheep')
    {
        $this->name = $name;
        $this->category = $category;
    }

    public function setName(string $name)
    {
        $this->name = $name;
    }

    public function getName()
    {
        return $this->name;
    }

    public function setCategory(string $category)
    {
        $this->category = $category;
    }

    public function getCategory()
    {
        return $this->category;
    }
}
```
Sau đó nó có thể được clone như bên dưới
```php
$original = new Sheep('Jolly');
echo $original->getName(); // Jolly
echo $original->getCategory(); // Mountain Sheep

// Clone and modify what is required
$cloned = clone $original;
$cloned->setName('Dolly');
echo $cloned->getName(); // Dolly
echo $cloned->getCategory(); // Mountain sheep
```

Bạn cũng có thể dùng magic method `__clone` để thay đổi hành vi clone.

**Khi nào sử dụng?**

Dùng khi bạn cần một object tương tự object đã có hoặc khi việc tạo mới tốn kém hơn so với clone.

💍 Singleton
------------
Ví dụ thực tế
> Ở một thời điểm chỉ có thể có một tổng thống của một quốc gia. Mỗi khi cần, cũng chính vị tổng thống đó phải được đưa vào hoạt động. Tổng thống ở đây chính là singleton.

Nói đơn giản
> Đảm bảo rằng chỉ có đúng một object của một class cụ thể từng được tạo ra.

Wikipedia nói
> Trong kỹ nghệ phần mềm, singleton pattern là một software design pattern giới hạn việc khởi tạo một class chỉ còn một object. Điều này hữu ích khi hệ thống cần chính xác một object để điều phối các hành động.

singleton pattern thực ra thường bị xem là một anti-pattern và nên tránh lạm dụng. Nó không hẳn là xấu và vẫn có một số trường hợp dùng hợp lý, nhưng cần dùng thận trọng vì nó đưa global state vào ứng dụng; thay đổi ở một nơi có thể ảnh hưởng đến nơi khác và khiến việc debug trở nên khá khó khăn. Điểm bất lợi khác là nó làm code bị kết dính chặt hơn và việc mock singleton cũng có thể khó.

**Ví dụ lập trình**

Để tạo singleton, hãy đặt constructor thành private, vô hiệu hóa việc clone, không cho phép kế thừa và tạo một biến static để giữ instance đó
```php
final class President
{
    private static $instance;

    private function __construct()
    {
        // Hide the constructor
    }

    public static function getInstance(): President
    {
        if (!self::$instance) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    private function __clone()
    {
        // Disable cloning
    }

    private function __wakeup()
    {
        // Disable unserialize
    }
}
```
Sau đó, để sử dụng
```php
$president1 = President::getInstance();
$president2 = President::getInstance();

var_dump($president1 === $president2); // true
```

Structural Design Patterns
==========================
Nói đơn giản
> Structural patterns chủ yếu quan tâm đến việc kết hợp các object, hay nói cách khác là cách các thực thể có thể dùng lẫn nhau. Một cách diễn đạt khác là chúng giúp trả lời câu hỏi: "Làm thế nào để xây dựng một software component?"

Wikipedia nói
> Trong kỹ nghệ phần mềm, structural design patterns là các design patterns giúp việc thiết kế trở nên dễ dàng hơn bằng cách xác định một cách đơn giản để hiện thực hóa các mối quan hệ giữa các thực thể.

 * [Adapter](#-adapter)
 * [Bridge](#-bridge)
 * [Composite](#-composite)
 * [Decorator](#-decorator)
 * [Facade](#-facade)
 * [Flyweight](#-flyweight)
 * [Proxy](#-proxy)

🔌 Adapter
-------
Ví dụ thực tế
> Hãy tưởng tượng bạn có một số ảnh trong thẻ nhớ và cần chuyển chúng sang máy tính. Để làm điều đó, bạn cần một loại adapter tương thích với các cổng trên máy tính để có thể gắn thẻ nhớ vào. Trong trường hợp này, đầu đọc thẻ chính là adapter.
> Một ví dụ khác là bộ đổi nguồn quen thuộc; một phích cắm ba chấu không thể cắm vào ổ hai chấu, nó cần dùng power adapter để tương thích với ổ hai chấu.
> Một ví dụ nữa là người phiên dịch, chuyển lời nói của người này sang cho người kia.

Nói đơn giản
> adapter pattern cho phép bạn bọc một object vốn không tương thích bên trong một adapter để làm nó tương thích với một class khác.

Wikipedia nói
> Trong kỹ nghệ phần mềm, adapter pattern là một software design pattern cho phép interface của một class có sẵn được dùng như một interface khác. Nó thường được dùng để làm cho các class hiện có hoạt động được với nhau mà không cần sửa source code của chúng.

**Ví dụ lập trình**

Hãy xét một trò chơi có một thợ săn và anh ta săn sư tử.

Trước tiên, chúng ta có interface `Lion` mà mọi loại sư tử đều phải cài đặt

```php
interface Lion
{
    public function roar();
}

class AfricanLion implements Lion
{
    public function roar()
    {
    }
}

class AsianLion implements Lion
{
    public function roar()
    {
    }
}
```
Và thợ săn kỳ vọng bất kỳ phần cài đặt nào của interface `Lion` cũng có thể dùng để săn.
```php
class Hunter
{
    public function hunt(Lion $lion)
    {
        $lion->roar();
    }
}
```

Giờ hãy giả sử chúng ta cần thêm `WildDog` vào trò chơi để thợ săn cũng có thể săn nó. Nhưng không thể làm trực tiếp vì chó có interface khác. Để làm nó tương thích với thợ săn, chúng ta sẽ phải tạo một adapter phù hợp.

```php
// This needs to be added to the game
class WildDog
{
    public function bark()
    {
    }
}

// Adapter around wild dog to make it compatible with our game
class WildDogAdapter implements Lion
{
    protected $dog;

    public function __construct(WildDog $dog)
    {
        $this->dog = $dog;
    }

    public function roar()
    {
        $this->dog->bark();
    }
}
```
Và bây giờ `WildDog` có thể được dùng trong trò chơi của chúng ta thông qua `WildDogAdapter`.

```php
$wildDog = new WildDog();
$wildDogAdapter = new WildDogAdapter($wildDog);

$hunter = new Hunter();
$hunter->hunt($wildDogAdapter);
```

🚡 Bridge
------
Ví dụ thực tế
> Hãy tưởng tượng bạn có một website với nhiều trang khác nhau và bạn cần cho phép người dùng đổi theme. Bạn sẽ làm gì? Tạo nhiều bản sao của từng trang cho từng theme, hay chỉ tạo các theme riêng biệt và nạp chúng dựa trên sở thích của người dùng? Bridge pattern cho phép bạn làm theo cách thứ hai, tức là:

![Với và không có bridge pattern](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)

Nói đơn giản
> bridge pattern đề cao composition hơn inheritance. Các chi tiết cài đặt được tách khỏi một hệ phân cấp và đẩy sang một object khác có hệ phân cấp riêng.

Wikipedia nói
> bridge pattern là một design pattern được dùng trong kỹ nghệ phần mềm với mục đích "tách abstraction ra khỏi implementation để cả hai có thể thay đổi độc lập"

**Ví dụ lập trình**

Chuyển ví dụ `WebPage` ở trên sang code. Ở đây chúng ta có hệ phân cấp `WebPage`

```php
interface WebPage
{
    public function __construct(Theme $theme);
    public function getContent();
}

class About implements WebPage
{
    protected $theme;

    public function __construct(Theme $theme)
    {
        $this->theme = $theme;
    }

    public function getContent()
    {
        return "About page in " . $this->theme->getColor();
    }
}

class Careers implements WebPage
{
    protected $theme;

    public function __construct(Theme $theme)
    {
        $this->theme = $theme;
    }

    public function getContent()
    {
        return "Careers page in " . $this->theme->getColor();
    }
}
```
Và hệ phân cấp theme riêng biệt
```php

interface Theme
{
    public function getColor();
}

class DarkTheme implements Theme
{
    public function getColor()
    {
        return 'Dark Black';
    }
}
class LightTheme implements Theme
{
    public function getColor()
    {
        return 'Off white';
    }
}
class AquaTheme implements Theme
{
    public function getColor()
    {
        return 'Light blue';
    }
}
```
Và kết hợp cả hai hệ phân cấp
```php
$darkTheme = new DarkTheme();

$about = new About($darkTheme);
$careers = new Careers($darkTheme);

echo $about->getContent(); // "About page in Dark Black";
echo $careers->getContent(); // "Careers page in Dark Black";
```

🌿 Composite
-----------------

Ví dụ thực tế
> Mọi tổ chức đều được tạo thành từ các nhân viên. Mỗi nhân viên có những đặc điểm giống nhau, tức là có lương, có một số trách nhiệm, có thể hoặc không báo cáo cho ai đó, có thể hoặc không có cấp dưới, v.v.

Nói đơn giản
> composite pattern cho phép client xử lý các object riêng lẻ theo một cách thống nhất.

Wikipedia nói
> Trong kỹ nghệ phần mềm, composite pattern là một design pattern phân chia cấu trúc. composite pattern mô tả rằng một nhóm object sẽ được đối xử giống như một instance đơn lẻ của object. Mục đích của composite là "ghép" các object thành cấu trúc cây để biểu diễn quan hệ bộ phận-tổng thể. Việc cài đặt composite pattern cho phép client xử lý thống nhất cả object riêng lẻ lẫn tổ hợp object.

**Ví dụ lập trình**

Lấy ví dụ về nhân viên ở trên. Ở đây chúng ta có nhiều kiểu nhân viên khác nhau

```php
interface Employee
{
    public function __construct(string $name, float $salary);
    public function getName(): string;
    public function setSalary(float $salary);
    public function getSalary(): float;
    public function getRoles(): array;
}

class Developer implements Employee
{
    protected $salary;
    protected $name;
    protected $roles;
    
    public function __construct(string $name, float $salary)
    {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setSalary(float $salary)
    {
        $this->salary = $salary;
    }

    public function getSalary(): float
    {
        return $this->salary;
    }

    public function getRoles(): array
    {
        return $this->roles;
    }
}

class Designer implements Employee
{
    protected $salary;
    protected $name;
    protected $roles;

    public function __construct(string $name, float $salary)
    {
        $this->name = $name;
        $this->salary = $salary;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function setSalary(float $salary)
    {
        $this->salary = $salary;
    }

    public function getSalary(): float
    {
        return $this->salary;
    }

    public function getRoles(): array
    {
        return $this->roles;
    }
}
```

Sau đó, chúng ta có một tổ chức gồm nhiều loại nhân viên khác nhau

```php
class Organization
{
    protected $employees;

    public function addEmployee(Employee $employee)
    {
        $this->employees[] = $employee;
    }

    public function getNetSalaries(): float
    {
        $netSalary = 0;

        foreach ($this->employees as $employee) {
            $netSalary += $employee->getSalary();
        }

        return $netSalary;
    }
}
```

Và sau đó có thể dùng như sau

```php
// Prepare the employees
$john = new Developer('John Doe', 12000);
$jane = new Designer('Jane Doe', 15000);

// Add them to organization
$organization = new Organization();
$organization->addEmployee($john);
$organization->addEmployee($jane);

echo "Net salaries: " . $organization->getNetSalaries(); // Net Salaries: 27000
```

☕ Decorator
-------------

Ví dụ thực tế

> Hãy tưởng tượng bạn điều hành một gara cung cấp nhiều dịch vụ. Vậy bạn tính hóa đơn như thế nào? Bạn bắt đầu với một dịch vụ rồi động thêm giá của từng dịch vụ được cung cấp cho tới khi ra tổng chi phí cuối cùng. Ở đây mỗi loại dịch vụ chính là một decorator.

Nói đơn giản
> decorator pattern cho phép bạn thay đổi động hành vi của một object trong lúc chạy bằng cách bọc nó bên trong một object thuộc decorator class.

Wikipedia nói
> Trong lập trình hướng đối tượng, decorator pattern là một design pattern cho phép bổ sung hành vi cho một object riêng lẻ, theo cách tĩnh hoặc động, mà không ảnh hưởng đến hành vi của các object khác cùng class. decorator pattern thường hữu ích để tuân theo Single Responsibility Principle, vì nó cho phép chia chức năng giữa các class với các mối quan tâm riêng biệt.

**Ví dụ lập trình**

Hãy lấy cà phê làm ví dụ. Trước hết, chúng ta có một loại cà phê đơn giản cài đặt coffee interface

```php
interface Coffee
{
    public function getCost();
    public function getDescription();
}

class SimpleCoffee implements Coffee
{
    public function getCost()
    {
        return 10;
    }

    public function getDescription()
    {
        return 'Simple coffee';
    }
}
```
Chúng ta muốn làm cho code có thể mở rộng để thêm các tùy chọn chỉnh sửa khi cần. Hãy tạo một vài phần bổ sung (decorators)
```php
class MilkCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 2;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', milk';
    }
}

class WhipCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 5;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', whip';
    }
}

class VanillaCoffee implements Coffee
{
    protected $coffee;

    public function __construct(Coffee $coffee)
    {
        $this->coffee = $coffee;
    }

    public function getCost()
    {
        return $this->coffee->getCost() + 3;
    }

    public function getDescription()
    {
        return $this->coffee->getDescription() . ', vanilla';
    }
}
```

Giờ hãy pha một ly cà phê

```php
$someCoffee = new SimpleCoffee();
echo $someCoffee->getCost(); // 10
echo $someCoffee->getDescription(); // Simple Coffee

$someCoffee = new MilkCoffee($someCoffee);
echo $someCoffee->getCost(); // 12
echo $someCoffee->getDescription(); // Simple Coffee, milk

$someCoffee = new WhipCoffee($someCoffee);
echo $someCoffee->getCost(); // 17
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip

$someCoffee = new VanillaCoffee($someCoffee);
echo $someCoffee->getCost(); // 20
echo $someCoffee->getDescription(); // Simple Coffee, milk, whip, vanilla
```

📦 Facade
----------------

Ví dụ thực tế
> Bạn bật máy tính như thế nào? "Nhấn nút nguồn" — bạn sẽ nói vậy! Đó là điều bạn nghĩ vì bạn đang dùng một interface đơn giản mà máy tính cung cấp ở bên ngoài, trong khi bên trong nó phải làm rất nhiều việc để chuyện đó xảy ra. Interface đơn giản dẫn vào một subsystem phức tạp đó chính là facade.

Nói đơn giản
> facade pattern cung cấp một interface đơn giản hóa cho một subsystem phức tạp.

Wikipedia nói
> facade là một object cung cấp một interface đơn giản hóa cho một khối code lớn hơn, chẳng hạn như một class library.

**Ví dụ lập trình**

Lấy ví dụ về máy tính ở trên. Ở đây chúng ta có class máy tính

```php
class Computer
{
    public function getElectricShock()
    {
        echo "Ouch!";
    }

    public function makeSound()
    {
        echo "Beep beep!";
    }

    public function showLoadingScreen()
    {
        echo "Loading..";
    }

    public function bam()
    {
        echo "Ready to be used!";
    }

    public function closeEverything()
    {
        echo "Bup bup bup buzzzz!";
    }

    public function sooth()
    {
        echo "Zzzzz";
    }

    public function pullCurrent()
    {
        echo "Haaah!";
    }
}
```
Ở đây là facade
```php
class ComputerFacade
{
    protected $computer;

    public function __construct(Computer $computer)
    {
        $this->computer = $computer;
    }

    public function turnOn()
    {
        $this->computer->getElectricShock();
        $this->computer->makeSound();
        $this->computer->showLoadingScreen();
        $this->computer->bam();
    }

    public function turnOff()
    {
        $this->computer->closeEverything();
        $this->computer->pullCurrent();
        $this->computer->sooth();
    }
}
```
Bây giờ hãy dùng facade
```php
$computer = new ComputerFacade(new Computer());
$computer->turnOn(); // Ouch! Beep beep! Loading.. Ready to be used!
$computer->turnOff(); // Bup bup buzzz! Haah! Zzzzz
```

🍃 Flyweight
---------

Ví dụ thực tế
> Bạn đã từng uống trà tươi ở một quầy hàng chưa? Họ thường pha nhiều hơn số ly bạn gọi và giữ phần còn lại cho khách khác để tiết kiệm tài nguyên như gas, v.v. flyweight pattern chính là như vậy, tức là chia sẻ.

Nói đơn giản
> Nó được dùng để giảm mức sử dụng bộ nhớ hoặc chi phí tính toán bằng cách chia sẻ nhiều nhất có thể giữa các object tương tự nhau.

Wikipedia nói
> Trong lập trình máy tính, flyweight là một software design pattern. flyweight là một object giảm thiểu việc dùng bộ nhớ bằng cách chia sẻ càng nhiều dữ liệu càng tốt với các object tương tự khác; đây là một cách để dùng số lượng lớn object khi một biểu diễn lặp lại đơn giản sẽ tiêu tốn lượng bộ nhớ không thể chấp nhận được.

**Ví dụ lập trình**

Chuyển ví dụ về trà ở trên sang code. Trước hết, chúng ta có các loại trà và tea maker

```php
// Anything that will be cached is flyweight.
// Types of tea here will be flyweights.
class KarakTea
{
}

// Acts as a factory and saves the tea
class TeaMaker
{
    protected $availableTea = [];

    public function make($preference)
    {
        if (empty($this->availableTea[$preference])) {
            $this->availableTea[$preference] = new KarakTea();
        }

        return $this->availableTea[$preference];
    }
}
```

Sau đó, chúng ta có `TeaShop`, nơi nhận đơn và phục vụ chúng

```php
class TeaShop
{
    protected $orders;
    protected $teaMaker;

    public function __construct(TeaMaker $teaMaker)
    {
        $this->teaMaker = $teaMaker;
    }

    public function takeOrder(string $teaType, int $table)
    {
        $this->orders[$table] = $this->teaMaker->make($teaType);
    }

    public function serve()
    {
        foreach ($this->orders as $table => $tea) {
            echo "Serving tea to table# " . $table;
        }
    }
}
```
Và nó có thể được dùng như bên dưới

```php
$teaMaker = new TeaMaker();
$shop = new TeaShop($teaMaker);

$shop->takeOrder('less sugar', 1);
$shop->takeOrder('more milk', 2);
$shop->takeOrder('without sugar', 5);

$shop->serve();
// Serving tea to table# 1
// Serving tea to table# 2
// Serving tea to table# 5
```

🎱 Proxy
-------------------
Ví dụ thực tế
> Bạn đã bao giờ dùng thẻ ra vào để mở cửa chưa? Có nhiều cách để mở cánh cửa đó, ví dụ nó có thể được mở bằng thẻ ra vào hoặc bằng cách nhấn một nút bỏ qua lớp bảo mật. Chức năng chính của cánh cửa là mở, nhưng có một proxy được thêm lên trên để bổ sung thêm chức năng. Để tôi giải thích rõ hơn bằng ví dụ code dưới đây.

Nói đơn giản
> Với proxy pattern, một class đại diện cho chức năng của một class khác.

Wikipedia nói
> proxy, ở dạng tổng quát nhất, là một class hoạt động như interface cho một thứ khác. proxy là một object bao bọc hoặc đại diện được client gọi để truy cập object thực thi thật ở phía sau. Việc dùng proxy có thể chỉ đơn giản là chuyển tiếp sang object thật, hoặc cung cấp thêm logic bổ sung. Trong proxy có thể thêm chức năng như cache khi các thao tác trên object thật tốn nhiều tài nguyên, hoặc kiểm tra điều kiện trước khi gọi các thao tác trên object thật.

**Ví dụ lập trình**

Lấy ví dụ về cửa bảo mật ở trên. Trước hết, chúng ta có door interface và một phần cài đặt của cửa

```php
interface Door
{
    public function open();
    public function close();
}

class LabDoor implements Door
{
    public function open()
    {
        echo "Opening lab door";
    }

    public function close()
    {
        echo "Closing the lab door";
    }
}
```
Sau đó, chúng ta có một proxy để bảo vệ bất kỳ cánh cửa nào mình muốn
```php
class SecuredDoor implements Door
{
    protected $door;

    public function __construct(Door $door)
    {
        $this->door = $door;
    }

    public function open($password)
    {
        if ($this->authenticate($password)) {
            $this->door->open();
        } else {
            echo "Big no! It ain't possible.";
        }
    }

    public function authenticate($password)
    {
        return $password === '$ecr@t';
    }

    public function close()
    {
        $this->door->close();
    }
}
```
Và đây là cách có thể dùng nó
```php
$door = new SecuredDoor(new LabDoor());
$door->open('invalid'); // Big no! It ain't possible.

$door->open('$ecr@t'); // Opening lab door
$door->close(); // Closing lab door
```
Một ví dụ khác là một kiểu cài đặt data-mapper nào đó. Ví dụ, gần đây tôi đã tạo một ODM (Object Data Mapper) cho MongoDB bằng pattern này, trong đó tôi viết một proxy bao quanh các class mongo và sử dụng magic method `__call()`. Mọi lời gọi method đều được chuyển tiếp tới class mongo gốc và kết quả lấy được được trả về nguyên trạng; nhưng trong trường hợp `find` hoặc `findOne`, dữ liệu sẽ được ánh xạ sang các object class cần thiết và object đó được trả về thay cho `Cursor`.

Behavioral Design Patterns
==========================

Nói đơn giản
> Nhóm này quan tâm đến việc phân chia trách nhiệm giữa các object. Điểm khiến chúng khác với structural patterns là chúng không chỉ mô tả cấu trúc mà còn phác thảo các mẫu truyền thông điệp/giao tiếp giữa chúng. Nói cách khác, chúng giúp trả lời câu hỏi: "Làm thế nào để chạy một hành vi trong software component?"

Wikipedia nói
> Trong kỹ nghệ phần mềm, behavioral design patterns là các design patterns nhận diện những mẫu giao tiếp phổ biến giữa các object và hiện thực hóa các mẫu đó. Nhờ vậy, chúng tăng tính linh hoạt khi thực hiện việc giao tiếp này.

* [Chain of Responsibility](#-chain-of-responsibility)
* [Command](#-command)
* [Iterator](#-iterator)
* [Mediator](#-mediator)
* [Memento](#-memento)
* [Observer](#-observer)
* [Visitor](#-visitor)
* [Strategy](#-strategy)
* [State](#-state)
* [Template Method](#-template-method)

🔗 Chain of Responsibility
-----------------------

Ví dụ thực tế
> Ví dụ, bạn có ba phương thức thanh toán (`A`, `B` và `C`) được thiết lập trong tài khoản; mỗi phương thức có một số tiền khác nhau. `A` có 100 USD, `B` có 300 USD và `C` có 1000 USD, và thứ tự ưu tiên thanh toán được chọn là `A`, rồi `B`, rồi `C`. Bạn muốn mua một món đồ trị giá 210 USD. Với Chain of Responsibility, trước tiên tài khoản `A` sẽ được kiểm tra xem có thể thanh toán hay không; nếu có thì việc mua sẽ được thực hiện và chuỗi dừng lại. Nếu không, yêu cầu sẽ được chuyển tiếp sang tài khoản `B` để kiểm tra số dư; nếu được thì chuỗi dừng, còn không thì yêu cầu tiếp tục được chuyển tiếp cho tới khi tìm thấy handler phù hợp. Ở đây `A`, `B` và `C` là các mắt xích của chuỗi, và toàn bộ hiện tượng đó chính là Chain of Responsibility.

Nói đơn giản
> Nó giúp xây dựng một chuỗi object. Yêu cầu đi vào từ một đầu và tiếp tục truyền từ object này sang object khác cho tới khi tìm được handler phù hợp.

Wikipedia nói
> Trong thiết kế hướng đối tượng, chain-of-responsibility pattern là một design pattern gồm một nguồn command object và một chuỗi các object xử lý. Mỗi object xử lý chứa logic xác định kiểu command object mà nó có thể xử lý; phần còn lại sẽ được chuyển sang object xử lý tiếp theo trong chuỗi.

**Ví dụ lập trình**

Chuyển ví dụ tài khoản ở trên sang code. Trước hết, chúng ta có một account cơ sở chứa logic để nối các account lại với nhau cùng một số account cụ thể

```php
abstract class Account
{
    protected $successor;
    protected $balance;

    public function setNext(Account $account)
    {
        $this->successor = $account;
    }

    public function pay(float $amountToPay)
    {
        if ($this->canPay($amountToPay)) {
            echo sprintf('Paid %s using %s' . PHP_EOL, $amountToPay, get_called_class());
        } elseif ($this->successor) {
            echo sprintf('Cannot pay using %s. Proceeding ..' . PHP_EOL, get_called_class());
            $this->successor->pay($amountToPay);
        } else {
            throw new Exception('None of the accounts have enough balance');
        }
    }

    public function canPay($amount): bool
    {
        return $this->balance >= $amount;
    }
}

class Bank extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}

class Paypal extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}

class Bitcoin extends Account
{
    protected $balance;

    public function __construct(float $balance)
    {
        $this->balance = $balance;
    }
}
```

Bây giờ hãy chuẩn bị chuỗi bằng các mắt xích đã định nghĩa ở trên (tức là Bank, Paypal, Bitcoin)

```php
// Let's prepare a chain like below
//      $bank->$paypal->$bitcoin
//
// First priority bank
//      If bank can't pay then paypal
//      If paypal can't pay then bit coin

$bank = new Bank(100);          // Bank with balance 100
$paypal = new Paypal(200);      // Paypal with balance 200
$bitcoin = new Bitcoin(300);    // Bitcoin with balance 300

$bank->setNext($paypal);
$paypal->setNext($bitcoin);

// Let's try to pay using the first priority i.e. bank
$bank->pay(259);

// Output will be
// ==============
// Cannot pay using bank. Proceeding ..
// Cannot pay using paypal. Proceeding ..:
// Paid 259 using Bitcoin!
```

👮 Command
-------

Ví dụ thực tế
> Một ví dụ quen thuộc là bạn gọi món trong nhà hàng. Bạn (tức `Client`) nhờ người phục vụ (tức `Invoker`) mang thức ăn (tức `Command`), và người phục vụ chỉ việc chuyển tiếp yêu cầu đó cho đầu bếp (tức `Receiver`) — người biết phải nấu gì và nấu như thế nào.
> Một ví dụ khác là bạn (`Client`) bật (`Command`) chiếc TV (`Receiver`) bằng điều khiển từ xa (`Invoker`).

Nói đơn giản
> Cho phép bạn đóng gói các hành động bên trong object. Ý tưởng cốt lõi đằng sau pattern này là cung cấp cách để tách client khỏi receiver.

Wikipedia nói
> Trong lập trình hướng đối tượng, command pattern là một behavioral design pattern trong đó một object được dùng để đóng gói toàn bộ thông tin cần thiết để thực hiện một hành động hoặc kích hoạt một sự kiện vào thời điểm sau này. Thông tin đó bao gồm tên method, object sở hữu method và các giá trị của tham số method.

**Ví dụ lập trình**

Trước hết, chúng ta có receiver, nơi chứa phần cài đặt của mọi hành động có thể được thực hiện
```php
// Receiver
class Bulb
{
    public function turnOn()
    {
        echo "Bulb has been lit";
    }

    public function turnOff()
    {
        echo "Darkness!";
    }
}
```
sau đó chúng ta có một interface mà mỗi command sẽ cài đặt, rồi tiếp theo là một tập các command
```php
interface Command
{
    public function execute();
    public function undo();
    public function redo();
}

// Command
class TurnOn implements Command
{
    protected $bulb;

    public function __construct(Bulb $bulb)
    {
        $this->bulb = $bulb;
    }

    public function execute()
    {
        $this->bulb->turnOn();
    }

    public function undo()
    {
        $this->bulb->turnOff();
    }

    public function redo()
    {
        $this->execute();
    }
}

class TurnOff implements Command
{
    protected $bulb;

    public function __construct(Bulb $bulb)
    {
        $this->bulb = $bulb;
    }

    public function execute()
    {
        $this->bulb->turnOff();
    }

    public function undo()
    {
        $this->bulb->turnOn();
    }

    public function redo()
    {
        $this->execute();
    }
}
```
Tiếp theo, chúng ta có `Invoker`, thành phần mà client sẽ tương tác để xử lý các command
```php
// Invoker
class RemoteControl
{
    public function submit(Command $command)
    {
        $command->execute();
    }
}
```
Cuối cùng, hãy xem cách chúng ta có thể dùng nó trong client
```php
$bulb = new Bulb();

$turnOn = new TurnOn($bulb);
$turnOff = new TurnOff($bulb);

$remote = new RemoteControl();
$remote->submit($turnOn); // Bulb has been lit!
$remote->submit($turnOff); // Darkness!
```

command pattern cũng có thể được dùng để cài đặt một hệ thống dựa trên transaction. Bạn sẽ lưu lại lịch sử các command ngay khi thực thi chúng. Nếu command cuối cùng chạy thành công thì mọi thứ ổn; còn nếu không, chỉ cần duyệt ngược lịch sử và tiếp tục gọi `undo` trên tất cả các command đã thực thi.

➿ Iterator
--------

Ví dụ thực tế
> Một chiếc radio kiểu cũ là ví dụ hay cho iterator, nơi người dùng có thể bắt đầu ở một kênh nào đó rồi dùng nút next hoặc previous để đi qua các kênh tương ứng. Hoặc hãy nghĩ tới máy nghe MP3 hay TV, nơi bạn có thể nhấn nút next và previous để đi qua các kênh liên tiếp; nói cách khác, tất cả chúng đều cung cấp một interface để duyệt qua các kênh, bài hát hoặc đài phát thanh tương ứng.  

Nói đơn giản
> Nó cung cấp một cách để truy cập các phần tử của một object mà không để lộ cách biểu diễn bên dưới.

Wikipedia nói
> Trong lập trình hướng đối tượng, iterator pattern là một design pattern trong đó iterator được dùng để duyệt một container và truy cập các phần tử của container đó. iterator pattern tách thuật toán ra khỏi container; tuy vậy, trong một số trường hợp, thuật toán gắn chặt với container nên không thể tách rời.

**Ví dụ lập trình**

Trong PHP, việc cài đặt pattern này khá dễ dàng bằng SPL (Standard PHP Library). Chuyển ví dụ về các đài phát thanh ở trên sang code, trước hết chúng ta có `RadioStation`

```php
class RadioStation
{
    protected $frequency;

    public function __construct(float $frequency)
    {
        $this->frequency = $frequency;
    }

    public function getFrequency(): float
    {
        return $this->frequency;
    }
}
```
Tiếp theo, chúng ta có iterator của mình

```php
use Countable;
use Iterator;

class StationList implements Countable, Iterator
{
    /** @var RadioStation[] $stations */
    protected $stations = [];

    /** @var int $counter */
    protected $counter;

    public function addStation(RadioStation $station)
    {
        $this->stations[] = $station;
    }

    public function removeStation(RadioStation $toRemove)
    {
        $toRemoveFrequency = $toRemove->getFrequency();
        $this->stations = array_filter($this->stations, function (RadioStation $station) use ($toRemoveFrequency) {
            return $station->getFrequency() !== $toRemoveFrequency;
        });
    }

    public function count(): int
    {
        return count($this->stations);
    }

    public function current(): RadioStation
    {
        return $this->stations[$this->counter];
    }

    public function key()
    {
        return $this->counter;
    }

    public function next()
    {
        $this->counter++;
    }

    public function rewind()
    {
        $this->counter = 0;
    }

    public function valid(): bool
    {
        return isset($this->stations[$this->counter]);
    }
}
```
Và sau đó có thể dùng như sau
```php
$stationList = new StationList();

$stationList->addStation(new RadioStation(89));
$stationList->addStation(new RadioStation(101));
$stationList->addStation(new RadioStation(102));
$stationList->addStation(new RadioStation(103.2));

foreach($stationList as $station) {
    echo $station->getFrequency() . PHP_EOL;
}

$stationList->removeStation(new RadioStation(89)); // Will remove station 89
```

👽 Mediator
========

Ví dụ thực tế
> Một ví dụ quen thuộc là khi bạn nói chuyện với ai đó qua điện thoại di động, sẽ có nhà mạng đứng ở giữa bạn và họ, và cuộc trò chuyện đi qua nhà mạng thay vì được gửi trực tiếp. Trong trường hợp này, nhà mạng chính là mediator.

Nói đơn giản
> mediator pattern thêm một object bên thứ ba (gọi là mediator) để kiểm soát sự tương tác giữa hai object (gọi là colleagues). Nó giúp giảm coupling giữa các class đang giao tiếp với nhau, vì giờ đây chúng không cần biết chi tiết cài đặt của nhau.

Wikipedia nói
> Trong kỹ nghệ phần mềm, mediator pattern định nghĩa một object đóng gói cách một tập hợp object tương tác với nhau. Pattern này được xem là một behavioral pattern vì cách nó có thể thay đổi hành vi chạy của chương trình.

**Ví dụ lập trình**

Đây là ví dụ đơn giản nhất về một phòng chat (tức mediator) với các người dùng (tức colleagues) gửi tin nhắn cho nhau.

Trước hết, chúng ta có mediator, tức là phòng chat

```php
interface ChatRoomMediator 
{
    public function showMessage(User $user, string $message);
}

// Mediator
class ChatRoom implements ChatRoomMediator
{
    public function showMessage(User $user, string $message)
    {
        $time = date('M d, y H:i');
        $sender = $user->getName();

        echo $time . '[' . $sender . ']:' . $message;
    }
}
```

Tiếp theo, chúng ta có các user, tức là colleagues
```php
class User {
    protected $name;
    protected $chatMediator;

    public function __construct(string $name, ChatRoomMediator $chatMediator) {
        $this->name = $name;
        $this->chatMediator = $chatMediator;
    }

    public function getName() {
        return $this->name;
    }

    public function send($message) {
        $this->chatMediator->showMessage($this, $message);
    }
}
```
Và cách sử dụng
```php
$mediator = new ChatRoom();

$john = new User('John Doe', $mediator);
$jane = new User('Jane Doe', $mediator);

$john->send('Hi there!');
$jane->send('Hey!');

// Output will be
// Feb 14, 10:58 [John]: Hi there!
// Feb 14, 10:58 [Jane]: Hey!
```

💾 Memento
-------
Ví dụ thực tế
> Hãy lấy ví dụ máy tính bỏ túi (tức originator), nơi mỗi khi bạn thực hiện một phép tính thì phép tính gần nhất được lưu vào bộ nhớ (tức memento) để bạn có thể quay lại nó và khôi phục bằng một số nút thao tác (tức caretaker).

Nói đơn giản
> memento pattern là về việc chụp lại và lưu trữ trạng thái hiện tại của một object theo cách mà sau này có thể khôi phục lại một cách trơn tru.

Wikipedia nói
> memento pattern là một software design pattern cung cấp khả năng khôi phục một object về trạng thái trước đó của nó (undo thông qua rollback).

Thường hữu ích khi bạn cần cung cấp một dạng chức năng undo nào đó.

**Ví dụ lập trình**

Hãy lấy ví dụ một trình soạn thảo văn bản liên tục lưu trạng thái theo thời gian và bạn có thể khôi phục nếu muốn.

Trước hết, chúng ta có memento object có khả năng giữ trạng thái của trình soạn thảo

```php
class EditorMemento
{
    protected $content;

    public function __construct(string $content)
    {
        $this->content = $content;
    }

    public function getContent()
    {
        return $this->content;
    }
}
```

Tiếp theo, chúng ta có editor, tức originator, thành phần sẽ dùng memento object

```php
class Editor
{
    protected $content = '';

    public function type(string $words)
    {
        $this->content = $this->content . ' ' . $words;
    }

    public function getContent()
    {
        return $this->content;
    }

    public function save()
    {
        return new EditorMemento($this->content);
    }

    public function restore(EditorMemento $memento)
    {
        $this->content = $memento->getContent();
    }
}
```

Và sau đó có thể dùng như sau

```php
$editor = new Editor();

// Type some stuff
$editor->type('This is the first sentence.');
$editor->type('This is second.');

// Save the state to restore to : This is the first sentence. This is second.
$saved = $editor->save();

// Type some more
$editor->type('And this is third.');

// Output: Content before Saving
echo $editor->getContent(); // This is the first sentence. This is second. And this is third.

// Restoring to last saved state
$editor->restore($saved);

$editor->getContent(); // This is the first sentence. This is second.
```

😎 Observer
--------
Ví dụ thực tế
> Một ví dụ hay là những người tìm việc đăng ký theo dõi một trang tuyển dụng và được thông báo bất cứ khi nào có cơ hội việc làm phù hợp.   

Nói đơn giản
> Định nghĩa một sự phụ thuộc giữa các object để khi một object thay đổi trạng thái, tất cả đối tượng phụ thuộc vào nó đều được thông báo.

Wikipedia nói
> observer pattern là một software design pattern trong đó một object, gọi là subject, duy trì danh sách các đối tượng phụ thuộc vào nó, gọi là observers, và tự động thông báo cho họ về mọi thay đổi trạng thái, thường bằng cách gọi một trong các method của họ.

**Ví dụ lập trình**

Chuyển ví dụ ở trên sang code. Trước hết, chúng ta có những người tìm việc cần được thông báo khi có tin tuyển dụng
```php
class JobPost
{
    protected $title;

    public function __construct(string $title)
    {
        $this->title = $title;
    }

    public function getTitle()
    {
        return $this->title;
    }
}

class JobSeeker implements Observer
{
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function onJobPosted(JobPost $job)
    {
        // Do something with the job posting
        echo 'Hi ' . $this->name . '! New job posted: '. $job->getTitle();
    }
}
```
Tiếp theo, chúng ta có nơi đăng tin tuyển dụng mà người tìm việc sẽ đăng ký theo dõi
```php
class EmploymentAgency implements Observable
{
    protected $observers = [];

    protected function notify(JobPost $jobPosting)
    {
        foreach ($this->observers as $observer) {
            $observer->onJobPosted($jobPosting);
        }
    }

    public function attach(Observer $observer)
    {
        $this->observers[] = $observer;
    }

    public function addJob(JobPost $jobPosting)
    {
        $this->notify($jobPosting);
    }
}
```
Sau đó có thể dùng như sau
```php
// Create subscribers
$johnDoe = new JobSeeker('John Doe');
$janeDoe = new JobSeeker('Jane Doe');

// Create publisher and attach subscribers
$jobPostings = new EmploymentAgency();
$jobPostings->attach($johnDoe);
$jobPostings->attach($janeDoe);

// Add a new job and see if subscribers get notified
$jobPostings->addJob(new JobPost('Software Engineer'));

// Output
// Hi John Doe! New job posted: Software Engineer
// Hi Jane Doe! New job posted: Software Engineer
```

🏃 Visitor
-------
Ví dụ thực tế
> Hãy tưởng tượng một người tới thăm Dubai. Họ chỉ cần một cách (tức visa) để vào Dubai. Sau khi đến nơi, họ có thể tự mình đi thăm bất kỳ đâu ở Dubai mà không cần xin phép hay làm thêm thủ tục gì để ghé từng địa điểm; chỉ cần cho họ biết địa điểm là họ có thể đến. visitor pattern cũng cho phép bạn làm điều tương tự: nó giúp bạn thêm các nơi cần ghé thăm để người đó có thể đi được bao nhiêu tùy thích mà không cần thêm công sức chuẩn bị.

Nói đơn giản
> visitor pattern cho phép bạn thêm các thao tác mới cho object mà không cần sửa đổi chính chúng.

Wikipedia nói
> Trong lập trình hướng đối tượng và kỹ nghệ phần mềm, visitor design pattern là một cách tách thuật toán khỏi cấu trúc object mà nó vận hành trên đó. Kết quả thực tế của sự tách biệt này là khả năng thêm các thao tác mới vào các cấu trúc object hiện có mà không cần sửa đổi chính các cấu trúc đó. Đây là một cách để tuân theo nguyên tắc open/closed.

**Ví dụ lập trình**

Hãy lấy ví dụ một mô phỏng sở thú, nơi chúng ta có nhiều loại động vật khác nhau và cần khiến chúng phát ra âm thanh. Hãy chuyển điều này sang code bằng visitor pattern

```php
// Visitee
interface Animal
{
    public function accept(AnimalOperation $operation);
}

// Visitor
interface AnimalOperation
{
    public function visitMonkey(Monkey $monkey);
    public function visitLion(Lion $lion);
    public function visitDolphin(Dolphin $dolphin);
}
```
Tiếp theo, chúng ta có các phần cài đặt cho những con vật
```php
class Monkey implements Animal
{
    public function shout()
    {
        echo 'Ooh oo aa aa!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitMonkey($this);
    }
}

class Lion implements Animal
{
    public function roar()
    {
        echo 'Roaaar!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitLion($this);
    }
}

class Dolphin implements Animal
{
    public function speak()
    {
        echo 'Tuut tuttu tuutt!';
    }

    public function accept(AnimalOperation $operation)
    {
        $operation->visitDolphin($this);
    }
}
```
Hãy cài đặt visitor của chúng ta
```php
class Speak implements AnimalOperation
{
    public function visitMonkey(Monkey $monkey)
    {
        $monkey->shout();
    }

    public function visitLion(Lion $lion)
    {
        $lion->roar();
    }

    public function visitDolphin(Dolphin $dolphin)
    {
        $dolphin->speak();
    }
}
```

Và sau đó có thể dùng như sau
```php
$monkey = new Monkey();
$lion = new Lion();
$dolphin = new Dolphin();

$speak = new Speak();

$monkey->accept($speak);    // Ooh oo aa aa!    
$lion->accept($speak);      // Roaaar!
$dolphin->accept($speak);   // Tuut tutt tuutt!
```
Chúng ta hoàn toàn có thể làm điều này chỉ bằng một hệ phân cấp kế thừa cho các con vật, nhưng khi cần thêm hành động mới cho động vật thì lại phải sửa chính các class động vật. Còn bây giờ, chúng ta sẽ không phải thay đổi chúng. Ví dụ, giả sử cần thêm hành vi nhảy cho động vật, ta chỉ cần tạo một visitor mới như sau.

```php
class Jump implements AnimalOperation
{
    public function visitMonkey(Monkey $monkey)
    {
        echo 'Jumped 20 feet high! on to the tree!';
    }

    public function visitLion(Lion $lion)
    {
        echo 'Jumped 7 feet! Back on the ground!';
    }

    public function visitDolphin(Dolphin $dolphin)
    {
        echo 'Walked on water a little and disappeared';
    }
}
```
Và cách sử dụng
```php
$jump = new Jump();

$monkey->accept($speak);   // Ooh oo aa aa!
$monkey->accept($jump);    // Jumped 20 feet high! on to the tree!

$lion->accept($speak);     // Roaaar!
$lion->accept($jump);      // Jumped 7 feet! Back on the ground!

$dolphin->accept($speak);  // Tuut tutt tuutt!
$dolphin->accept($jump);   // Walked on water a little and disappeared
```

💡 Strategy
--------

Ví dụ thực tế
> Hãy xét ví dụ về sắp xếp: ban đầu chúng ta cài bubble sort nhưng dữ liệu ngày càng lớn và bubble sort trở nên rất chậm. Để xử lý việc đó, chúng ta cài Quick sort. Nhưng rồi, dù quick sort chạy tốt hơn với tập dữ liệu lớn, nó lại rất chậm với tập dữ liệu nhỏ. Vì vậy, chúng ta cài một strategy: với tập dữ liệu nhỏ thì dùng bubble sort, còn với tập dữ liệu lớn thì dùng quick sort.

Nói đơn giản
> strategy pattern cho phép bạn chuyển đổi thuật toán hoặc strategy tùy theo tình huống.

Wikipedia nói
> Trong lập trình máy tính, strategy pattern (còn được gọi là policy pattern) là một behavioural software design pattern cho phép lựa chọn hành vi của thuật toán tại runtime.

**Ví dụ lập trình**

Chuyển ví dụ ở trên sang code. Trước hết, chúng ta có strategy interface và các phần cài đặt strategy khác nhau

```php
interface SortStrategy
{
    public function sort(array $dataset): array;
}

class BubbleSortStrategy implements SortStrategy
{
    public function sort(array $dataset): array
    {
        echo "Sorting using bubble sort";

        // Do sorting
        return $dataset;
    }
}

class QuickSortStrategy implements SortStrategy
{
    public function sort(array $dataset): array
    {
        echo "Sorting using quick sort";

        // Do sorting
        return $dataset;
    }
}
```

Tiếp theo, chúng ta có client sẽ sử dụng bất kỳ strategy nào
```php
class Sorter
{
    protected $sorterSmall;
    protected $sorterBig;

    public function __construct(SortStrategy $sorterSmall, SortStrategy $sorterBig)
    {
        $this->sorterSmall = $sorterSmall;
        $this->sorterBig = $sorterBig;
    }

    public function sort(array $dataset): array
    {
        if (count($dataset) > 5) {
            return $this->sorterBig->sort($dataset);
        } else {
            return $this->sorterSmall->sort($dataset);
        }
    }
}
```
Và nó có thể được dùng như sau
```php
$smalldataset = [1, 3, 4, 2];
$bigdataset = [1, 4, 3, 2, 8, 10, 5, 6, 9, 7];

$sorter = new Sorter(new BubbleSortStrategy(), new QuickSortStrategy());

$sorter->sort($dataset); // Output : Sorting using bubble sort

$sorter->sort($bigdataset); // Output : Sorting using quick sort
```

💢 State
-----
Ví dụ thực tế
> Hãy tưởng tượng bạn đang dùng một ứng dụng vẽ và chọn cọ vẽ để vẽ. Lúc này cây cọ thay đổi hành vi tùy theo màu đã chọn, ví dụ nếu chọn màu đỏ thì nó sẽ vẽ màu đỏ, nếu là xanh thì sẽ vẽ màu xanh, v.v.  

Nói đơn giản
> Nó cho phép bạn thay đổi hành vi của một class khi state thay đổi.

Wikipedia nói
> state pattern là một behavioral software design pattern cài đặt state machine theo cách hướng đối tượng. Với state pattern, state machine được hiện thực bằng cách cài đặt từng state riêng lẻ thành lớp dẫn xuất của state pattern interface, và cài đặt các chuyển đổi state bằng cách gọi các method được định nghĩa bởi superclass của pattern.
> state pattern có thể được hiểu như một strategy pattern có khả năng chuyển đổi strategy hiện tại thông qua việc gọi các method được định nghĩa trong interface của pattern.

**Ví dụ lập trình**

Hãy lấy ví dụ một chiếc điện thoại. Trước hết, chúng ta có state interface và một số phần cài đặt state

```php
interface PhoneState {
    public function pickUp(): PhoneState;
    public function hangUp(): PhoneState;
    public function dial(): PhoneState;
}

// states implementation
class PhoneStateIdle implements PhoneState {
    public function pickUp(): PhoneState {
        return new PhoneStatePickedUp();
    }
    public function hangUp(): PhoneState {
        throw new Exception("already idle");
    }
    public function dial(): PhoneState {
        throw new Exception("unable to dial in idle state");
    }
}

class PhoneStatePickedUp implements PhoneState {
    public function pickUp(): PhoneState {
        throw new Exception("already picked up");
    }
    public function hangUp(): PhoneState {
        return new PhoneStateIdle();
    }
    public function dial(): PhoneState {
        return new PhoneStateCalling();
    }
}

class PhoneStateCalling implements PhoneState {
    public function pickUp(): PhoneState {
        throw new Exception("already picked up");
    }
    public function hangUp(): PhoneState {
        return new PhoneStateIdle();
    }
    public function dial(): PhoneState {
        throw new Exception("already dialing");
    }
}
```

Tiếp theo, chúng ta có class Phone thay đổi state theo các lời gọi hành vi khác nhau

```php
class Phone {
    private $state;

    public function __construct() {
        $this->state = new PhoneStateIdle();
    }
    public function pickUp() {
        $this->state = $this->state->pickUp();
    }
    public function hangUp() {
        $this->state = $this->state->hangUp();
    }
    public function dial() {
        $this->state = $this->state->dial();
    }
}
```

Và sau đó có thể dùng như sau, khi đó nó sẽ gọi các method state tương ứng:

```php
$phone = new Phone();

$phone->pickUp();
$phone->dial();
```

📒 Template Method
---------------

Ví dụ thực tế
> Giả sử chúng ta đang xây một căn nhà. Các bước xây dựng có thể trông như sau
> - Chuẩn bị móng nhà
> - Xây tường
> - Lợp mái
> - Thêm các tầng khác

> Thứ tự của các bước này không bao giờ được thay đổi, tức là bạn không thể lợp mái trước khi xây tường, v.v.; nhưng mỗi bước đều có thể được biến đổi, ví dụ tường có thể làm bằng gỗ, polyester hoặc đá.

Nói đơn giản
> template method định nghĩa bộ khung của cách một thuật toán nhất định được thực hiện, nhưng hoãn phần cài đặt của các bước đó cho các lớp con.

Wikipedia nói
> Trong kỹ nghệ phần mềm, template method pattern là một behavioral design pattern định nghĩa bộ khung chương trình của một thuật toán trong một thao tác, đồng thời hoãn một số bước cho các lớp con. Nó cho phép định nghĩa lại một số bước nhất định của thuật toán mà không làm thay đổi cấu trúc của thuật toán.

**Ví dụ lập trình**

Hãy tưởng tượng chúng ta có một build tool giúp test, lint, build, tạo các báo cáo build (ví dụ báo cáo code coverage, báo cáo linting, v.v.) và deploy ứng dụng của mình lên test server.

Trước hết, chúng ta có base class chỉ rõ bộ khung của thuật toán build
```php
abstract class Builder
{

    // Template method
    final public function build()
    {
        $this->test();
        $this->lint();
        $this->assemble();
        $this->deploy();
    }

    abstract public function test();
    abstract public function lint();
    abstract public function assemble();
    abstract public function deploy();
}
```

Sau đó, chúng ta có thể có các phần cài đặt cụ thể

```php
class AndroidBuilder extends Builder
{
    public function test()
    {
        echo 'Running android tests';
    }

    public function lint()
    {
        echo 'Linting the android code';
    }

    public function assemble()
    {
        echo 'Assembling the android build';
    }

    public function deploy()
    {
        echo 'Deploying android build to server';
    }
}

class IosBuilder extends Builder
{
    public function test()
    {
        echo 'Running ios tests';
    }

    public function lint()
    {
        echo 'Linting the ios code';
    }

    public function assemble()
    {
        echo 'Assembling the ios build';
    }

    public function deploy()
    {
        echo 'Deploying ios build to server';
    }
}
```
Và sau đó có thể dùng như sau

```php
$androidBuilder = new AndroidBuilder();
$androidBuilder->build();

// Output:
// Running android tests
// Linting the android code
// Assembling the android build
// Deploying android build to server

$iosBuilder = new IosBuilder();
$iosBuilder->build();

// Output:
// Running ios tests
// Linting the ios code
// Assembling the ios build
// Deploying ios build to server
```

## 🚦 Tổng kết

Vậy là chúng ta tạm khép lại ở đây. Tôi sẽ tiếp tục cải thiện tài liệu này, nên bạn có thể watch/star repository này để quay lại sau. Ngoài ra, tôi cũng có kế hoạch viết một phiên bản tương tự về architectural patterns, hãy chờ nhé.

## 👬 Đóng góp

- Báo cáo vấn đề
- Mở pull request với các cải tiến
- Lan tỏa cho mọi người cùng biết
- Gửi cho tôi bất kỳ phản hồi nào [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/kamrify.svg?style=social&label=Follow%20%40kamrify)](https://twitter.com/kamrify)

## Giấy phép

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
