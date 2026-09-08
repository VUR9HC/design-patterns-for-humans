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

> Cũng lưu ý rằng các ví dụ code bên dưới dùng C++17, nhưng điều đó không nên cản trở bạn vì các khái niệm thì vẫn như nhau.

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
```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual float getWidth() const = 0;
    virtual float getHeight() const = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
protected:
    float width;
    float height;

public:
    WoodenDoor(float width, float height) : width(width), height(height) {}

    float getWidth() const override {
        return width;
    }

    float getHeight() const override {
        return height;
    }
};

class DoorFactory {
public:
    static std::shared_ptr<Door> makeDoor(float width, float height) {
        return std::make_shared<WoodenDoor>(width, height);
    }
};

int main() {
    auto door = DoorFactory::makeDoor(100, 200);
    std::cout << "Width: " << door->getWidth();
    std::cout << "Height: " << door->getHeight();

    auto door2 = DoorFactory::makeDoor(50, 100);
    (void)door2;
    return 0;
}
```
Tiếp theo, chúng ta có door factory tạo cửa và trả nó về
```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual float getWidth() const = 0;
    virtual float getHeight() const = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
protected:
    float width;
    float height;

public:
    WoodenDoor(float width, float height) : width(width), height(height) {}

    float getWidth() const override {
        return width;
    }

    float getHeight() const override {
        return height;
    }
};

class DoorFactory {
public:
    static std::shared_ptr<Door> makeDoor(float width, float height) {
        return std::make_shared<WoodenDoor>(width, height);
    }
};

int main() {
    auto door = DoorFactory::makeDoor(100, 200);
    std::cout << "Width: " << door->getWidth();
    std::cout << "Height: " << door->getHeight();

    auto door2 = DoorFactory::makeDoor(50, 100);
    (void)door2;
    return 0;
}
```
Và sau đó có thể dùng như sau
```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual float getWidth() const = 0;
    virtual float getHeight() const = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
protected:
    float width;
    float height;

public:
    WoodenDoor(float width, float height) : width(width), height(height) {}

    float getWidth() const override {
        return width;
    }

    float getHeight() const override {
        return height;
    }
};

class DoorFactory {
public:
    static std::shared_ptr<Door> makeDoor(float width, float height) {
        return std::make_shared<WoodenDoor>(width, height);
    }
};

int main() {
    auto door = DoorFactory::makeDoor(100, 200);
    std::cout << "Width: " << door->getWidth();
    std::cout << "Height: " << door->getHeight();

    auto door2 = DoorFactory::makeDoor(50, 100);
    (void)door2;
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>

class Interviewer {
public:
    virtual void askQuestions() = 0;
    virtual ~Interviewer() = default;
};

class Developer : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about design patterns!";
    }
};

class CommunityExecutive : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about community building";
    }
};

class HiringManager {
protected:
    virtual std::shared_ptr<Interviewer> makeInterviewer() = 0;

public:
    virtual ~HiringManager() = default;

    void takeInterview() {
        auto interviewer = makeInterviewer();
        interviewer->askQuestions();
    }
};

class DevelopmentManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<Developer>();
    }
};

class MarketingManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<CommunityExecutive>();
    }
};

int main() {
    DevelopmentManager devManager;
    devManager.takeInterview();
    std::cout << std::endl;

    MarketingManager marketingManager;
    marketingManager.takeInterview();
    return 0;
}
```

Bây giờ hãy tạo `HiringManager` của chúng ta

```cpp
#include <iostream>
#include <memory>

class Interviewer {
public:
    virtual void askQuestions() = 0;
    virtual ~Interviewer() = default;
};

class Developer : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about design patterns!";
    }
};

class CommunityExecutive : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about community building";
    }
};

class HiringManager {
protected:
    virtual std::shared_ptr<Interviewer> makeInterviewer() = 0;

public:
    virtual ~HiringManager() = default;

    void takeInterview() {
        auto interviewer = makeInterviewer();
        interviewer->askQuestions();
    }
};

class DevelopmentManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<Developer>();
    }
};

class MarketingManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<CommunityExecutive>();
    }
};

int main() {
    DevelopmentManager devManager;
    devManager.takeInterview();
    std::cout << std::endl;

    MarketingManager marketingManager;
    marketingManager.takeInterview();
    return 0;
}
```
Giờ thì bất kỳ lớp con nào cũng có thể kế thừa nó và cung cấp người phỏng vấn phù hợp
```cpp
#include <iostream>
#include <memory>

class Interviewer {
public:
    virtual void askQuestions() = 0;
    virtual ~Interviewer() = default;
};

class Developer : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about design patterns!";
    }
};

class CommunityExecutive : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about community building";
    }
};

class HiringManager {
protected:
    virtual std::shared_ptr<Interviewer> makeInterviewer() = 0;

public:
    virtual ~HiringManager() = default;

    void takeInterview() {
        auto interviewer = makeInterviewer();
        interviewer->askQuestions();
    }
};

class DevelopmentManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<Developer>();
    }
};

class MarketingManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<CommunityExecutive>();
    }
};

int main() {
    DevelopmentManager devManager;
    devManager.takeInterview();
    std::cout << std::endl;

    MarketingManager marketingManager;
    marketingManager.takeInterview();
    return 0;
}
```
và sau đó có thể dùng như sau

```cpp
#include <iostream>
#include <memory>

class Interviewer {
public:
    virtual void askQuestions() = 0;
    virtual ~Interviewer() = default;
};

class Developer : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about design patterns!";
    }
};

class CommunityExecutive : public Interviewer {
public:
    void askQuestions() override {
        std::cout << "Asking about community building";
    }
};

class HiringManager {
protected:
    virtual std::shared_ptr<Interviewer> makeInterviewer() = 0;

public:
    virtual ~HiringManager() = default;

    void takeInterview() {
        auto interviewer = makeInterviewer();
        interviewer->askQuestions();
    }
};

class DevelopmentManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<Developer>();
    }
};

class MarketingManager : public HiringManager {
protected:
    std::shared_ptr<Interviewer> makeInterviewer() override {
        return std::make_shared<CommunityExecutive>();
    }
};

int main() {
    DevelopmentManager devManager;
    devManager.takeInterview();
    std::cout << std::endl;

    MarketingManager marketingManager;
    marketingManager.takeInterview();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual void getDescription() = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am a wooden door";
    }
};

class IronDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am an iron door";
    }
};

class DoorFittingExpert {
public:
    virtual void getDescription() = 0;
    virtual ~DoorFittingExpert() = default;
};

class Welder : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit iron doors";
    }
};

class Carpenter : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit wooden doors";
    }
};

class DoorFactory {
public:
    virtual std::shared_ptr<Door> makeDoor() = 0;
    virtual std::shared_ptr<DoorFittingExpert> makeFittingExpert() = 0;
    virtual ~DoorFactory() = default;
};

class WoodenDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<WoodenDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Carpenter>();
    }
};

class IronDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<IronDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Welder>();
    }
};

int main() {
    auto woodenFactory = std::make_shared<WoodenDoorFactory>();
    auto door = woodenFactory->makeDoor();
    auto expert = woodenFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    std::cout << std::endl;

    auto ironFactory = std::make_shared<IronDoorFactory>();
    door = ironFactory->makeDoor();
    expert = ironFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    return 0;
}
```
Tiếp theo, chúng ta có một số chuyên gia lắp đặt cho từng loại cửa

```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual void getDescription() = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am a wooden door";
    }
};

class IronDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am an iron door";
    }
};

class DoorFittingExpert {
public:
    virtual void getDescription() = 0;
    virtual ~DoorFittingExpert() = default;
};

class Welder : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit iron doors";
    }
};

class Carpenter : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit wooden doors";
    }
};

class DoorFactory {
public:
    virtual std::shared_ptr<Door> makeDoor() = 0;
    virtual std::shared_ptr<DoorFittingExpert> makeFittingExpert() = 0;
    virtual ~DoorFactory() = default;
};

class WoodenDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<WoodenDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Carpenter>();
    }
};

class IronDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<IronDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Welder>();
    }
};

int main() {
    auto woodenFactory = std::make_shared<WoodenDoorFactory>();
    auto door = woodenFactory->makeDoor();
    auto expert = woodenFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    std::cout << std::endl;

    auto ironFactory = std::make_shared<IronDoorFactory>();
    door = ironFactory->makeDoor();
    expert = ironFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    return 0;
}
```

Bây giờ chúng ta có abstract factory cho phép tạo ra cả một họ object liên quan với nhau, ví dụ wooden door factory sẽ tạo cửa gỗ và chuyên gia lắp cửa gỗ, còn iron door factory sẽ tạo cửa sắt và chuyên gia lắp cửa sắt
```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual void getDescription() = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am a wooden door";
    }
};

class IronDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am an iron door";
    }
};

class DoorFittingExpert {
public:
    virtual void getDescription() = 0;
    virtual ~DoorFittingExpert() = default;
};

class Welder : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit iron doors";
    }
};

class Carpenter : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit wooden doors";
    }
};

class DoorFactory {
public:
    virtual std::shared_ptr<Door> makeDoor() = 0;
    virtual std::shared_ptr<DoorFittingExpert> makeFittingExpert() = 0;
    virtual ~DoorFactory() = default;
};

class WoodenDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<WoodenDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Carpenter>();
    }
};

class IronDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<IronDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Welder>();
    }
};

int main() {
    auto woodenFactory = std::make_shared<WoodenDoorFactory>();
    auto door = woodenFactory->makeDoor();
    auto expert = woodenFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    std::cout << std::endl;

    auto ironFactory = std::make_shared<IronDoorFactory>();
    door = ironFactory->makeDoor();
    expert = ironFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    return 0;
}
```
Và sau đó có thể dùng như sau
```cpp
#include <iostream>
#include <memory>

class Door {
public:
    virtual void getDescription() = 0;
    virtual ~Door() = default;
};

class WoodenDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am a wooden door";
    }
};

class IronDoor : public Door {
public:
    void getDescription() override {
        std::cout << "I am an iron door";
    }
};

class DoorFittingExpert {
public:
    virtual void getDescription() = 0;
    virtual ~DoorFittingExpert() = default;
};

class Welder : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit iron doors";
    }
};

class Carpenter : public DoorFittingExpert {
public:
    void getDescription() override {
        std::cout << "I can only fit wooden doors";
    }
};

class DoorFactory {
public:
    virtual std::shared_ptr<Door> makeDoor() = 0;
    virtual std::shared_ptr<DoorFittingExpert> makeFittingExpert() = 0;
    virtual ~DoorFactory() = default;
};

class WoodenDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<WoodenDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Carpenter>();
    }
};

class IronDoorFactory : public DoorFactory {
public:
    std::shared_ptr<Door> makeDoor() override {
        return std::make_shared<IronDoor>();
    }

    std::shared_ptr<DoorFittingExpert> makeFittingExpert() override {
        return std::make_shared<Welder>();
    }
};

int main() {
    auto woodenFactory = std::make_shared<WoodenDoorFactory>();
    auto door = woodenFactory->makeDoor();
    auto expert = woodenFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    std::cout << std::endl;

    auto ironFactory = std::make_shared<IronDoorFactory>();
    door = ironFactory->makeDoor();
    expert = ironFactory->makeFittingExpert();
    door->getDescription();
    std::cout << std::endl;
    expert->getDescription();
    return 0;
}
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

```cpp
#include <memory>

class Burger {
public:
    Burger(int size, bool cheese = true, bool pepperoni = true, bool tomato = false, bool lettuce = true) {
        (void)size;
        (void)cheese;
        (void)pepperoni;
        (void)tomato;
        (void)lettuce;
    }
};

int main() {
    auto burger = std::make_shared<Burger>(14);
    (void)burger;
    return 0;
}
```

Như bạn thấy, số lượng tham số của constructor có thể nhanh chóng trở nên mất kiểm soát và rất khó hiểu thứ tự các tham số. Thêm vào đó, danh sách tham số này còn có thể tiếp tục dài ra nếu bạn muốn thêm nhiều tùy chọn trong tương lai. Đó được gọi là telescoping constructor anti-pattern.

**Ví dụ lập trình**

Giải pháp hợp lý là dùng builder pattern. Trước hết, chúng ta có chiếc burger mà mình muốn tạo

```cpp
#include <memory>

class BurgerBuilder;

class Burger {
protected:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

public:
    explicit Burger(const BurgerBuilder& builder);
};

class BurgerBuilder {
public:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

    explicit BurgerBuilder(int size) : size(size) {}

    BurgerBuilder& addPepperoni() {
        pepperoni = true;
        return *this;
    }

    BurgerBuilder& addLettuce() {
        lettuce = true;
        return *this;
    }

    BurgerBuilder& addCheese() {
        cheese = true;
        return *this;
    }

    BurgerBuilder& addTomato() {
        tomato = true;
        return *this;
    }

    std::shared_ptr<Burger> build() {
        return std::make_shared<Burger>(*this);
    }
};

Burger::Burger(const BurgerBuilder& builder)
    : size(builder.size),
      cheese(builder.cheese),
      pepperoni(builder.pepperoni),
      lettuce(builder.lettuce),
      tomato(builder.tomato) {}

int main() {
    auto burger = BurgerBuilder(14)
                      .addPepperoni()
                      .addLettuce()
                      .addTomato()
                      .build();
    (void)burger;
    return 0;
}
```

Tiếp theo, chúng ta có builder

```cpp
#include <memory>

class BurgerBuilder;

class Burger {
protected:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

public:
    explicit Burger(const BurgerBuilder& builder);
};

class BurgerBuilder {
public:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

    explicit BurgerBuilder(int size) : size(size) {}

    BurgerBuilder& addPepperoni() {
        pepperoni = true;
        return *this;
    }

    BurgerBuilder& addLettuce() {
        lettuce = true;
        return *this;
    }

    BurgerBuilder& addCheese() {
        cheese = true;
        return *this;
    }

    BurgerBuilder& addTomato() {
        tomato = true;
        return *this;
    }

    std::shared_ptr<Burger> build() {
        return std::make_shared<Burger>(*this);
    }
};

Burger::Burger(const BurgerBuilder& builder)
    : size(builder.size),
      cheese(builder.cheese),
      pepperoni(builder.pepperoni),
      lettuce(builder.lettuce),
      tomato(builder.tomato) {}

int main() {
    auto burger = BurgerBuilder(14)
                      .addPepperoni()
                      .addLettuce()
                      .addTomato()
                      .build();
    (void)burger;
    return 0;
}
```
Và sau đó có thể dùng như sau:

```cpp
#include <memory>

class BurgerBuilder;

class Burger {
protected:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

public:
    explicit Burger(const BurgerBuilder& builder);
};

class BurgerBuilder {
public:
    int size;
    bool cheese = false;
    bool pepperoni = false;
    bool lettuce = false;
    bool tomato = false;

    explicit BurgerBuilder(int size) : size(size) {}

    BurgerBuilder& addPepperoni() {
        pepperoni = true;
        return *this;
    }

    BurgerBuilder& addLettuce() {
        lettuce = true;
        return *this;
    }

    BurgerBuilder& addCheese() {
        cheese = true;
        return *this;
    }

    BurgerBuilder& addTomato() {
        tomato = true;
        return *this;
    }

    std::shared_ptr<Burger> build() {
        return std::make_shared<Burger>(*this);
    }
};

Burger::Burger(const BurgerBuilder& builder)
    : size(builder.size),
      cheese(builder.cheese),
      pepperoni(builder.pepperoni),
      lettuce(builder.lettuce),
      tomato(builder.tomato) {}

int main() {
    auto burger = BurgerBuilder(14)
                      .addPepperoni()
                      .addLettuce()
                      .addTomato()
                      .build();
    (void)burger;
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class Sheep {
protected:
    std::string name;
    std::string category;

public:
    Sheep(std::string name, std::string category = "Mountain Sheep")
        : name(std::move(name)), category(std::move(category)) {}

    void setName(const std::string& newName) {
        name = newName;
    }

    std::string getName() const {
        return name;
    }

    void setCategory(const std::string& newCategory) {
        category = newCategory;
    }

    std::string getCategory() const {
        return category;
    }
};

int main() {
    auto original = std::make_shared<Sheep>("Jolly");
    std::cout << original->getName() << std::endl;
    std::cout << original->getCategory() << std::endl;

    auto cloned = std::make_shared<Sheep>(*original);
    cloned->setName("Dolly");
    std::cout << cloned->getName() << std::endl;
    std::cout << cloned->getCategory();
    return 0;
}
```
Sau đó nó có thể được clone như bên dưới
```cpp
#include <iostream>
#include <memory>
#include <string>

class Sheep {
protected:
    std::string name;
    std::string category;

public:
    Sheep(std::string name, std::string category = "Mountain Sheep")
        : name(std::move(name)), category(std::move(category)) {}

    void setName(const std::string& newName) {
        name = newName;
    }

    std::string getName() const {
        return name;
    }

    void setCategory(const std::string& newCategory) {
        category = newCategory;
    }

    std::string getCategory() const {
        return category;
    }
};

int main() {
    auto original = std::make_shared<Sheep>("Jolly");
    std::cout << original->getName() << std::endl;
    std::cout << original->getCategory() << std::endl;

    auto cloned = std::make_shared<Sheep>(*original);
    cloned->setName("Dolly");
    std::cout << cloned->getName() << std::endl;
    std::cout << cloned->getCategory();
    return 0;
}
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
```cpp
#include <iostream>

class President final {
private:
    President() = default;

public:
    President(const President&) = delete;
    President& operator=(const President&) = delete;

    static President& getInstance() {
        static President instance;
        return instance;
    }
};

int main() {
    President& president1 = President::getInstance();
    President& president2 = President::getInstance();
    std::cout << std::boolalpha << (&president1 == &president2);
    return 0;
}
```
Sau đó, để sử dụng
```cpp
#include <iostream>

class President final {
private:
    President() = default;

public:
    President(const President&) = delete;
    President& operator=(const President&) = delete;

    static President& getInstance() {
        static President instance;
        return instance;
    }
};

int main() {
    President& president1 = President::getInstance();
    President& president2 = President::getInstance();
    std::cout << std::boolalpha << (&president1 == &president2);
    return 0;
}
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

```cpp
#include <memory>

class Lion {
public:
    virtual void roar() = 0;
    virtual ~Lion() = default;
};

class AfricanLion : public Lion {
public:
    void roar() override {}
};

class AsianLion : public Lion {
public:
    void roar() override {}
};

class Hunter {
public:
    void hunt(const std::shared_ptr<Lion>& lion) {
        lion->roar();
    }
};

class WildDog {
public:
    void bark() {}
};

class WildDogAdapter : public Lion {
protected:
    std::shared_ptr<WildDog> dog;

public:
    explicit WildDogAdapter(std::shared_ptr<WildDog> dog) : dog(std::move(dog)) {}

    void roar() override {
        dog->bark();
    }
};

int main() {
    auto wildDog = std::make_shared<WildDog>();
    auto wildDogAdapter = std::make_shared<WildDogAdapter>(wildDog);

    Hunter hunter;
    hunter.hunt(wildDogAdapter);
    return 0;
}
```
Và thợ săn kỳ vọng bất kỳ phần cài đặt nào của interface `Lion` cũng có thể dùng để săn.
```cpp
#include <memory>

class Lion {
public:
    virtual void roar() = 0;
    virtual ~Lion() = default;
};

class AfricanLion : public Lion {
public:
    void roar() override {}
};

class AsianLion : public Lion {
public:
    void roar() override {}
};

class Hunter {
public:
    void hunt(const std::shared_ptr<Lion>& lion) {
        lion->roar();
    }
};

class WildDog {
public:
    void bark() {}
};

class WildDogAdapter : public Lion {
protected:
    std::shared_ptr<WildDog> dog;

public:
    explicit WildDogAdapter(std::shared_ptr<WildDog> dog) : dog(std::move(dog)) {}

    void roar() override {
        dog->bark();
    }
};

int main() {
    auto wildDog = std::make_shared<WildDog>();
    auto wildDogAdapter = std::make_shared<WildDogAdapter>(wildDog);

    Hunter hunter;
    hunter.hunt(wildDogAdapter);
    return 0;
}
```

Giờ hãy giả sử chúng ta cần thêm `WildDog` vào trò chơi để thợ săn cũng có thể săn nó. Nhưng không thể làm trực tiếp vì chó có interface khác. Để làm nó tương thích với thợ săn, chúng ta sẽ phải tạo một adapter phù hợp.

```cpp
#include <memory>

class Lion {
public:
    virtual void roar() = 0;
    virtual ~Lion() = default;
};

class AfricanLion : public Lion {
public:
    void roar() override {}
};

class AsianLion : public Lion {
public:
    void roar() override {}
};

class Hunter {
public:
    void hunt(const std::shared_ptr<Lion>& lion) {
        lion->roar();
    }
};

class WildDog {
public:
    void bark() {}
};

class WildDogAdapter : public Lion {
protected:
    std::shared_ptr<WildDog> dog;

public:
    explicit WildDogAdapter(std::shared_ptr<WildDog> dog) : dog(std::move(dog)) {}

    void roar() override {
        dog->bark();
    }
};

int main() {
    auto wildDog = std::make_shared<WildDog>();
    auto wildDogAdapter = std::make_shared<WildDogAdapter>(wildDog);

    Hunter hunter;
    hunter.hunt(wildDogAdapter);
    return 0;
}
```
Và bây giờ `WildDog` có thể được dùng trong trò chơi của chúng ta thông qua `WildDogAdapter`.

```cpp
#include <memory>

class Lion {
public:
    virtual void roar() = 0;
    virtual ~Lion() = default;
};

class AfricanLion : public Lion {
public:
    void roar() override {}
};

class AsianLion : public Lion {
public:
    void roar() override {}
};

class Hunter {
public:
    void hunt(const std::shared_ptr<Lion>& lion) {
        lion->roar();
    }
};

class WildDog {
public:
    void bark() {}
};

class WildDogAdapter : public Lion {
protected:
    std::shared_ptr<WildDog> dog;

public:
    explicit WildDogAdapter(std::shared_ptr<WildDog> dog) : dog(std::move(dog)) {}

    void roar() override {
        dog->bark();
    }
};

int main() {
    auto wildDog = std::make_shared<WildDog>();
    auto wildDogAdapter = std::make_shared<WildDogAdapter>(wildDog);

    Hunter hunter;
    hunter.hunt(wildDogAdapter);
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class Theme {
public:
    virtual std::string getColor() const = 0;
    virtual ~Theme() = default;
};

class DarkTheme : public Theme {
public:
    std::string getColor() const override {
        return "Dark Black";
    }
};

class LightTheme : public Theme {
public:
    std::string getColor() const override {
        return "Off white";
    }
};

class AquaTheme : public Theme {
public:
    std::string getColor() const override {
        return "Light blue";
    }
};

class WebPage {
public:
    explicit WebPage(std::shared_ptr<Theme> theme) : theme(std::move(theme)) {}
    virtual std::string getContent() const = 0;
    virtual ~WebPage() = default;

protected:
    std::shared_ptr<Theme> theme;
};

class About : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "About page in " + theme->getColor();
    }
};

class Careers : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "Careers page in " + theme->getColor();
    }
};

int main() {
    auto darkTheme = std::make_shared<DarkTheme>();

    About about(darkTheme);
    Careers careers(darkTheme);

    std::cout << about.getContent() << std::endl;
    std::cout << careers.getContent();
    return 0;
}
```
Và hệ phân cấp theme riêng biệt
```cpp
#include <iostream>
#include <memory>
#include <string>

class Theme {
public:
    virtual std::string getColor() const = 0;
    virtual ~Theme() = default;
};

class DarkTheme : public Theme {
public:
    std::string getColor() const override {
        return "Dark Black";
    }
};

class LightTheme : public Theme {
public:
    std::string getColor() const override {
        return "Off white";
    }
};

class AquaTheme : public Theme {
public:
    std::string getColor() const override {
        return "Light blue";
    }
};

class WebPage {
public:
    explicit WebPage(std::shared_ptr<Theme> theme) : theme(std::move(theme)) {}
    virtual std::string getContent() const = 0;
    virtual ~WebPage() = default;

protected:
    std::shared_ptr<Theme> theme;
};

class About : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "About page in " + theme->getColor();
    }
};

class Careers : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "Careers page in " + theme->getColor();
    }
};

int main() {
    auto darkTheme = std::make_shared<DarkTheme>();

    About about(darkTheme);
    Careers careers(darkTheme);

    std::cout << about.getContent() << std::endl;
    std::cout << careers.getContent();
    return 0;
}
```
Và kết hợp cả hai hệ phân cấp
```cpp
#include <iostream>
#include <memory>
#include <string>

class Theme {
public:
    virtual std::string getColor() const = 0;
    virtual ~Theme() = default;
};

class DarkTheme : public Theme {
public:
    std::string getColor() const override {
        return "Dark Black";
    }
};

class LightTheme : public Theme {
public:
    std::string getColor() const override {
        return "Off white";
    }
};

class AquaTheme : public Theme {
public:
    std::string getColor() const override {
        return "Light blue";
    }
};

class WebPage {
public:
    explicit WebPage(std::shared_ptr<Theme> theme) : theme(std::move(theme)) {}
    virtual std::string getContent() const = 0;
    virtual ~WebPage() = default;

protected:
    std::shared_ptr<Theme> theme;
};

class About : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "About page in " + theme->getColor();
    }
};

class Careers : public WebPage {
public:
    using WebPage::WebPage;

    std::string getContent() const override {
        return "Careers page in " + theme->getColor();
    }
};

int main() {
    auto darkTheme = std::make_shared<DarkTheme>();

    About about(darkTheme);
    Careers careers(darkTheme);

    std::cout << about.getContent() << std::endl;
    std::cout << careers.getContent();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class Employee {
public:
    Employee(std::string name, float salary) : name(std::move(name)), salary(salary) {}
    virtual ~Employee() = default;

    virtual std::string getName() const {
        return name;
    }

    virtual void setSalary(float newSalary) {
        salary = newSalary;
    }

    virtual float getSalary() const {
        return salary;
    }

    virtual std::vector<std::string> getRoles() const = 0;

protected:
    std::string name;
    float salary;
};

class Developer : public Employee {
public:
    Developer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Designer : public Employee {
public:
    Designer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Organization {
protected:
    std::vector<std::shared_ptr<Employee>> employees;

public:
    void addEmployee(std::shared_ptr<Employee> employee) {
        employees.push_back(std::move(employee));
    }

    float getNetSalaries() const {
        float netSalary = 0;
        for (const auto& employee : employees) {
            netSalary += employee->getSalary();
        }
        return netSalary;
    }
};

int main() {
    auto john = std::make_shared<Developer>("John Doe", 12000);
    auto jane = std::make_shared<Designer>("Jane Doe", 15000);

    Organization organization;
    organization.addEmployee(john);
    organization.addEmployee(jane);

    std::cout << "Net salaries: " << organization.getNetSalaries();
    return 0;
}
```

Sau đó, chúng ta có một tổ chức gồm nhiều loại nhân viên khác nhau

```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class Employee {
public:
    Employee(std::string name, float salary) : name(std::move(name)), salary(salary) {}
    virtual ~Employee() = default;

    virtual std::string getName() const {
        return name;
    }

    virtual void setSalary(float newSalary) {
        salary = newSalary;
    }

    virtual float getSalary() const {
        return salary;
    }

    virtual std::vector<std::string> getRoles() const = 0;

protected:
    std::string name;
    float salary;
};

class Developer : public Employee {
public:
    Developer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Designer : public Employee {
public:
    Designer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Organization {
protected:
    std::vector<std::shared_ptr<Employee>> employees;

public:
    void addEmployee(std::shared_ptr<Employee> employee) {
        employees.push_back(std::move(employee));
    }

    float getNetSalaries() const {
        float netSalary = 0;
        for (const auto& employee : employees) {
            netSalary += employee->getSalary();
        }
        return netSalary;
    }
};

int main() {
    auto john = std::make_shared<Developer>("John Doe", 12000);
    auto jane = std::make_shared<Designer>("Jane Doe", 15000);

    Organization organization;
    organization.addEmployee(john);
    organization.addEmployee(jane);

    std::cout << "Net salaries: " << organization.getNetSalaries();
    return 0;
}
```

Và sau đó có thể dùng như sau

```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class Employee {
public:
    Employee(std::string name, float salary) : name(std::move(name)), salary(salary) {}
    virtual ~Employee() = default;

    virtual std::string getName() const {
        return name;
    }

    virtual void setSalary(float newSalary) {
        salary = newSalary;
    }

    virtual float getSalary() const {
        return salary;
    }

    virtual std::vector<std::string> getRoles() const = 0;

protected:
    std::string name;
    float salary;
};

class Developer : public Employee {
public:
    Developer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Designer : public Employee {
public:
    Designer(std::string name, float salary) : Employee(std::move(name), salary) {}

    std::vector<std::string> getRoles() const override {
        return {};
    }
};

class Organization {
protected:
    std::vector<std::shared_ptr<Employee>> employees;

public:
    void addEmployee(std::shared_ptr<Employee> employee) {
        employees.push_back(std::move(employee));
    }

    float getNetSalaries() const {
        float netSalary = 0;
        for (const auto& employee : employees) {
            netSalary += employee->getSalary();
        }
        return netSalary;
    }
};

int main() {
    auto john = std::make_shared<Developer>("John Doe", 12000);
    auto jane = std::make_shared<Designer>("Jane Doe", 15000);

    Organization organization;
    organization.addEmployee(john);
    organization.addEmployee(jane);

    std::cout << "Net salaries: " << organization.getNetSalaries();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class Coffee {
public:
    virtual int getCost() const = 0;
    virtual std::string getDescription() const = 0;
    virtual ~Coffee() = default;
};

class SimpleCoffee : public Coffee {
public:
    int getCost() const override {
        return 10;
    }

    std::string getDescription() const override {
        return "Simple coffee";
    }
};

class MilkCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit MilkCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 2;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", milk";
    }
};

class WhipCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit WhipCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 5;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", whip";
    }
};

class VanillaCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit VanillaCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 3;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", vanilla";
    }
};

int main() {
    std::shared_ptr<Coffee> someCoffee = std::make_shared<SimpleCoffee>();
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<MilkCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<WhipCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<VanillaCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription();
    return 0;
}
```
Chúng ta muốn làm cho code có thể mở rộng để thêm các tùy chọn chỉnh sửa khi cần. Hãy tạo một vài phần bổ sung (decorators)
```cpp
#include <iostream>
#include <memory>
#include <string>

class Coffee {
public:
    virtual int getCost() const = 0;
    virtual std::string getDescription() const = 0;
    virtual ~Coffee() = default;
};

class SimpleCoffee : public Coffee {
public:
    int getCost() const override {
        return 10;
    }

    std::string getDescription() const override {
        return "Simple coffee";
    }
};

class MilkCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit MilkCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 2;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", milk";
    }
};

class WhipCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit WhipCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 5;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", whip";
    }
};

class VanillaCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit VanillaCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 3;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", vanilla";
    }
};

int main() {
    std::shared_ptr<Coffee> someCoffee = std::make_shared<SimpleCoffee>();
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<MilkCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<WhipCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<VanillaCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription();
    return 0;
}
```

Giờ hãy pha một ly cà phê

```cpp
#include <iostream>
#include <memory>
#include <string>

class Coffee {
public:
    virtual int getCost() const = 0;
    virtual std::string getDescription() const = 0;
    virtual ~Coffee() = default;
};

class SimpleCoffee : public Coffee {
public:
    int getCost() const override {
        return 10;
    }

    std::string getDescription() const override {
        return "Simple coffee";
    }
};

class MilkCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit MilkCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 2;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", milk";
    }
};

class WhipCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit WhipCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 5;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", whip";
    }
};

class VanillaCoffee : public Coffee {
protected:
    std::shared_ptr<Coffee> coffee;

public:
    explicit VanillaCoffee(std::shared_ptr<Coffee> coffee) : coffee(std::move(coffee)) {}

    int getCost() const override {
        return coffee->getCost() + 3;
    }

    std::string getDescription() const override {
        return coffee->getDescription() + ", vanilla";
    }
};

int main() {
    std::shared_ptr<Coffee> someCoffee = std::make_shared<SimpleCoffee>();
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<MilkCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<WhipCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription() << std::endl;

    someCoffee = std::make_shared<VanillaCoffee>(someCoffee);
    std::cout << someCoffee->getCost() << std::endl;
    std::cout << someCoffee->getDescription();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>

class Computer {
public:
    void getElectricShock() {
        std::cout << "Ouch!";
    }

    void makeSound() {
        std::cout << "Beep beep!";
    }

    void showLoadingScreen() {
        std::cout << "Loading..";
    }

    void bam() {
        std::cout << "Ready to be used!";
    }

    void closeEverything() {
        std::cout << "Bup bup bup buzzzz!";
    }

    void sooth() {
        std::cout << "Zzzzz";
    }

    void pullCurrent() {
        std::cout << "Haaah!";
    }
};

class ComputerFacade {
protected:
    std::shared_ptr<Computer> computer;

public:
    explicit ComputerFacade(std::shared_ptr<Computer> computer) : computer(std::move(computer)) {}

    void turnOn() {
        computer->getElectricShock();
        computer->makeSound();
        computer->showLoadingScreen();
        computer->bam();
    }

    void turnOff() {
        computer->closeEverything();
        computer->pullCurrent();
        computer->sooth();
    }
};

int main() {
    ComputerFacade computer(std::make_shared<Computer>());
    computer.turnOn();
    std::cout << std::endl;
    computer.turnOff();
    return 0;
}
```
Ở đây là facade
```cpp
#include <iostream>
#include <memory>

class Computer {
public:
    void getElectricShock() {
        std::cout << "Ouch!";
    }

    void makeSound() {
        std::cout << "Beep beep!";
    }

    void showLoadingScreen() {
        std::cout << "Loading..";
    }

    void bam() {
        std::cout << "Ready to be used!";
    }

    void closeEverything() {
        std::cout << "Bup bup bup buzzzz!";
    }

    void sooth() {
        std::cout << "Zzzzz";
    }

    void pullCurrent() {
        std::cout << "Haaah!";
    }
};

class ComputerFacade {
protected:
    std::shared_ptr<Computer> computer;

public:
    explicit ComputerFacade(std::shared_ptr<Computer> computer) : computer(std::move(computer)) {}

    void turnOn() {
        computer->getElectricShock();
        computer->makeSound();
        computer->showLoadingScreen();
        computer->bam();
    }

    void turnOff() {
        computer->closeEverything();
        computer->pullCurrent();
        computer->sooth();
    }
};

int main() {
    ComputerFacade computer(std::make_shared<Computer>());
    computer.turnOn();
    std::cout << std::endl;
    computer.turnOff();
    return 0;
}
```
Bây giờ hãy dùng facade
```cpp
#include <iostream>
#include <memory>

class Computer {
public:
    void getElectricShock() {
        std::cout << "Ouch!";
    }

    void makeSound() {
        std::cout << "Beep beep!";
    }

    void showLoadingScreen() {
        std::cout << "Loading..";
    }

    void bam() {
        std::cout << "Ready to be used!";
    }

    void closeEverything() {
        std::cout << "Bup bup bup buzzzz!";
    }

    void sooth() {
        std::cout << "Zzzzz";
    }

    void pullCurrent() {
        std::cout << "Haaah!";
    }
};

class ComputerFacade {
protected:
    std::shared_ptr<Computer> computer;

public:
    explicit ComputerFacade(std::shared_ptr<Computer> computer) : computer(std::move(computer)) {}

    void turnOn() {
        computer->getElectricShock();
        computer->makeSound();
        computer->showLoadingScreen();
        computer->bam();
    }

    void turnOff() {
        computer->closeEverything();
        computer->pullCurrent();
        computer->sooth();
    }
};

int main() {
    ComputerFacade computer(std::make_shared<Computer>());
    computer.turnOn();
    std::cout << std::endl;
    computer.turnOff();
    return 0;
}
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

```cpp
#include <iostream>
#include <map>
#include <memory>
#include <string>

class KarakTea {
};

class TeaMaker {
protected:
    std::map<std::string, std::shared_ptr<KarakTea>> availableTea;

public:
    std::shared_ptr<KarakTea> make(const std::string& preference) {
        auto it = availableTea.find(preference);
        if (it == availableTea.end()) {
            availableTea[preference] = std::make_shared<KarakTea>();
        }
        return availableTea[preference];
    }
};

class TeaShop {
protected:
    std::map<int, std::shared_ptr<KarakTea>> orders;
    std::shared_ptr<TeaMaker> teaMaker;

public:
    explicit TeaShop(std::shared_ptr<TeaMaker> teaMaker) : teaMaker(std::move(teaMaker)) {}

    void takeOrder(const std::string& teaType, int table) {
        orders[table] = teaMaker->make(teaType);
    }

    void serve() {
        for (const auto& [table, tea] : orders) {
            (void)tea;
            std::cout << "Serving tea to table# " << table << std::endl;
        }
    }
};

int main() {
    auto teaMaker = std::make_shared<TeaMaker>();
    TeaShop shop(teaMaker);

    shop.takeOrder("less sugar", 1);
    shop.takeOrder("more milk", 2);
    shop.takeOrder("without sugar", 5);

    shop.serve();
    return 0;
}
```

Sau đó, chúng ta có `TeaShop`, nơi nhận đơn và phục vụ chúng

```cpp
#include <iostream>
#include <map>
#include <memory>
#include <string>

class KarakTea {
};

class TeaMaker {
protected:
    std::map<std::string, std::shared_ptr<KarakTea>> availableTea;

public:
    std::shared_ptr<KarakTea> make(const std::string& preference) {
        auto it = availableTea.find(preference);
        if (it == availableTea.end()) {
            availableTea[preference] = std::make_shared<KarakTea>();
        }
        return availableTea[preference];
    }
};

class TeaShop {
protected:
    std::map<int, std::shared_ptr<KarakTea>> orders;
    std::shared_ptr<TeaMaker> teaMaker;

public:
    explicit TeaShop(std::shared_ptr<TeaMaker> teaMaker) : teaMaker(std::move(teaMaker)) {}

    void takeOrder(const std::string& teaType, int table) {
        orders[table] = teaMaker->make(teaType);
    }

    void serve() {
        for (const auto& [table, tea] : orders) {
            (void)tea;
            std::cout << "Serving tea to table# " << table << std::endl;
        }
    }
};

int main() {
    auto teaMaker = std::make_shared<TeaMaker>();
    TeaShop shop(teaMaker);

    shop.takeOrder("less sugar", 1);
    shop.takeOrder("more milk", 2);
    shop.takeOrder("without sugar", 5);

    shop.serve();
    return 0;
}
```
Và nó có thể được dùng như bên dưới

```cpp
#include <iostream>
#include <map>
#include <memory>
#include <string>

class KarakTea {
};

class TeaMaker {
protected:
    std::map<std::string, std::shared_ptr<KarakTea>> availableTea;

public:
    std::shared_ptr<KarakTea> make(const std::string& preference) {
        auto it = availableTea.find(preference);
        if (it == availableTea.end()) {
            availableTea[preference] = std::make_shared<KarakTea>();
        }
        return availableTea[preference];
    }
};

class TeaShop {
protected:
    std::map<int, std::shared_ptr<KarakTea>> orders;
    std::shared_ptr<TeaMaker> teaMaker;

public:
    explicit TeaShop(std::shared_ptr<TeaMaker> teaMaker) : teaMaker(std::move(teaMaker)) {}

    void takeOrder(const std::string& teaType, int table) {
        orders[table] = teaMaker->make(teaType);
    }

    void serve() {
        for (const auto& [table, tea] : orders) {
            (void)tea;
            std::cout << "Serving tea to table# " << table << std::endl;
        }
    }
};

int main() {
    auto teaMaker = std::make_shared<TeaMaker>();
    TeaShop shop(teaMaker);

    shop.takeOrder("less sugar", 1);
    shop.takeOrder("more milk", 2);
    shop.takeOrder("without sugar", 5);

    shop.serve();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class Door {
public:
    virtual void open(const std::string& password = "") = 0;
    virtual void close() = 0;
    virtual ~Door() = default;
};

class LabDoor : public Door {
public:
    void open(const std::string& password = "") override {
        (void)password;
        std::cout << "Opening lab door";
    }

    void close() override {
        std::cout << "Closing the lab door";
    }
};

class SecuredDoor : public Door {
protected:
    std::shared_ptr<Door> door;

public:
    explicit SecuredDoor(std::shared_ptr<Door> door) : door(std::move(door)) {}

    void open(const std::string& password = "") override {
        if (authenticate(password)) {
            door->open();
        } else {
            std::cout << "Big no! It ain't possible.";
        }
    }

    bool authenticate(const std::string& password) const {
        return password == "$ecr@t";
    }

    void close() override {
        door->close();
    }
};

int main() {
    auto door = std::make_shared<SecuredDoor>(std::make_shared<LabDoor>());
    door->open("invalid");
    std::cout << std::endl;
    door->open("$ecr@t");
    std::cout << std::endl;
    door->close();
    return 0;
}
```
Sau đó, chúng ta có một proxy để bảo vệ bất kỳ cánh cửa nào mình muốn
```cpp
#include <iostream>
#include <memory>
#include <string>

class Door {
public:
    virtual void open(const std::string& password = "") = 0;
    virtual void close() = 0;
    virtual ~Door() = default;
};

class LabDoor : public Door {
public:
    void open(const std::string& password = "") override {
        (void)password;
        std::cout << "Opening lab door";
    }

    void close() override {
        std::cout << "Closing the lab door";
    }
};

class SecuredDoor : public Door {
protected:
    std::shared_ptr<Door> door;

public:
    explicit SecuredDoor(std::shared_ptr<Door> door) : door(std::move(door)) {}

    void open(const std::string& password = "") override {
        if (authenticate(password)) {
            door->open();
        } else {
            std::cout << "Big no! It ain't possible.";
        }
    }

    bool authenticate(const std::string& password) const {
        return password == "$ecr@t";
    }

    void close() override {
        door->close();
    }
};

int main() {
    auto door = std::make_shared<SecuredDoor>(std::make_shared<LabDoor>());
    door->open("invalid");
    std::cout << std::endl;
    door->open("$ecr@t");
    std::cout << std::endl;
    door->close();
    return 0;
}
```
Và đây là cách có thể dùng nó
```cpp
#include <iostream>
#include <memory>
#include <string>

class Door {
public:
    virtual void open(const std::string& password = "") = 0;
    virtual void close() = 0;
    virtual ~Door() = default;
};

class LabDoor : public Door {
public:
    void open(const std::string& password = "") override {
        (void)password;
        std::cout << "Opening lab door";
    }

    void close() override {
        std::cout << "Closing the lab door";
    }
};

class SecuredDoor : public Door {
protected:
    std::shared_ptr<Door> door;

public:
    explicit SecuredDoor(std::shared_ptr<Door> door) : door(std::move(door)) {}

    void open(const std::string& password = "") override {
        if (authenticate(password)) {
            door->open();
        } else {
            std::cout << "Big no! It ain't possible.";
        }
    }

    bool authenticate(const std::string& password) const {
        return password == "$ecr@t";
    }

    void close() override {
        door->close();
    }
};

int main() {
    auto door = std::make_shared<SecuredDoor>(std::make_shared<LabDoor>());
    door->open("invalid");
    std::cout << std::endl;
    door->open("$ecr@t");
    std::cout << std::endl;
    door->close();
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <stdexcept>
#include <string>

class Account {
protected:
    std::shared_ptr<Account> successor;
    float balance = 0;

public:
    virtual ~Account() = default;

    void setNext(std::shared_ptr<Account> account) {
        successor = std::move(account);
    }

    void pay(float amountToPay) {
        if (canPay(amountToPay)) {
            std::cout << "Paid " << amountToPay << " using " << getName() << std::endl;
        } else if (successor) {
            std::cout << "Cannot pay using " << getName() << ". Proceeding .." << std::endl;
            successor->pay(amountToPay);
        } else {
            throw std::runtime_error("None of the accounts have enough balance");
        }
    }

    bool canPay(float amount) const {
        return balance >= amount;
    }

    virtual std::string getName() const = 0;
};

class Bank : public Account {
public:
    explicit Bank(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Bank";
    }
};

class Paypal : public Account {
public:
    explicit Paypal(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Paypal";
    }
};

class Bitcoin : public Account {
public:
    explicit Bitcoin(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Bitcoin";
    }
};

int main() {
    auto bank = std::make_shared<Bank>(100);
    auto paypal = std::make_shared<Paypal>(200);
    auto bitcoin = std::make_shared<Bitcoin>(300);

    bank->setNext(paypal);
    paypal->setNext(bitcoin);

    bank->pay(259);
    return 0;
}
```

Bây giờ hãy chuẩn bị chuỗi bằng các mắt xích đã định nghĩa ở trên (tức là Bank, Paypal, Bitcoin)

```cpp
#include <iostream>
#include <memory>
#include <stdexcept>
#include <string>

class Account {
protected:
    std::shared_ptr<Account> successor;
    float balance = 0;

public:
    virtual ~Account() = default;

    void setNext(std::shared_ptr<Account> account) {
        successor = std::move(account);
    }

    void pay(float amountToPay) {
        if (canPay(amountToPay)) {
            std::cout << "Paid " << amountToPay << " using " << getName() << std::endl;
        } else if (successor) {
            std::cout << "Cannot pay using " << getName() << ". Proceeding .." << std::endl;
            successor->pay(amountToPay);
        } else {
            throw std::runtime_error("None of the accounts have enough balance");
        }
    }

    bool canPay(float amount) const {
        return balance >= amount;
    }

    virtual std::string getName() const = 0;
};

class Bank : public Account {
public:
    explicit Bank(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Bank";
    }
};

class Paypal : public Account {
public:
    explicit Paypal(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Paypal";
    }
};

class Bitcoin : public Account {
public:
    explicit Bitcoin(float balance) {
        this->balance = balance;
    }

    std::string getName() const override {
        return "Bitcoin";
    }
};

int main() {
    auto bank = std::make_shared<Bank>(100);
    auto paypal = std::make_shared<Paypal>(200);
    auto bitcoin = std::make_shared<Bitcoin>(300);

    bank->setNext(paypal);
    paypal->setNext(bitcoin);

    bank->pay(259);
    return 0;
}
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
```cpp
#include <iostream>
#include <memory>

class Bulb {
public:
    void turnOn() {
        std::cout << "Bulb has been lit";
    }

    void turnOff() {
        std::cout << "Darkness!";
    }
};

class Command {
public:
    virtual void execute() = 0;
    virtual void undo() = 0;
    virtual void redo() = 0;
    virtual ~Command() = default;
};

class TurnOn : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOn(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOn();
    }

    void undo() override {
        bulb->turnOff();
    }

    void redo() override {
        execute();
    }
};

class TurnOff : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOff(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOff();
    }

    void undo() override {
        bulb->turnOn();
    }

    void redo() override {
        execute();
    }
};

class RemoteControl {
public:
    void submit(const std::shared_ptr<Command>& command) {
        command->execute();
    }
};

int main() {
    auto bulb = std::make_shared<Bulb>();
    auto turnOn = std::make_shared<TurnOn>(bulb);
    auto turnOff = std::make_shared<TurnOff>(bulb);

    RemoteControl remote;
    remote.submit(turnOn);
    std::cout << std::endl;
    remote.submit(turnOff);
    return 0;
}
```
sau đó chúng ta có một interface mà mỗi command sẽ cài đặt, rồi tiếp theo là một tập các command
```cpp
#include <iostream>
#include <memory>

class Bulb {
public:
    void turnOn() {
        std::cout << "Bulb has been lit";
    }

    void turnOff() {
        std::cout << "Darkness!";
    }
};

class Command {
public:
    virtual void execute() = 0;
    virtual void undo() = 0;
    virtual void redo() = 0;
    virtual ~Command() = default;
};

class TurnOn : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOn(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOn();
    }

    void undo() override {
        bulb->turnOff();
    }

    void redo() override {
        execute();
    }
};

class TurnOff : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOff(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOff();
    }

    void undo() override {
        bulb->turnOn();
    }

    void redo() override {
        execute();
    }
};

class RemoteControl {
public:
    void submit(const std::shared_ptr<Command>& command) {
        command->execute();
    }
};

int main() {
    auto bulb = std::make_shared<Bulb>();
    auto turnOn = std::make_shared<TurnOn>(bulb);
    auto turnOff = std::make_shared<TurnOff>(bulb);

    RemoteControl remote;
    remote.submit(turnOn);
    std::cout << std::endl;
    remote.submit(turnOff);
    return 0;
}
```
Tiếp theo, chúng ta có `Invoker`, thành phần mà client sẽ tương tác để xử lý các command
```cpp
#include <iostream>
#include <memory>

class Bulb {
public:
    void turnOn() {
        std::cout << "Bulb has been lit";
    }

    void turnOff() {
        std::cout << "Darkness!";
    }
};

class Command {
public:
    virtual void execute() = 0;
    virtual void undo() = 0;
    virtual void redo() = 0;
    virtual ~Command() = default;
};

class TurnOn : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOn(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOn();
    }

    void undo() override {
        bulb->turnOff();
    }

    void redo() override {
        execute();
    }
};

class TurnOff : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOff(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOff();
    }

    void undo() override {
        bulb->turnOn();
    }

    void redo() override {
        execute();
    }
};

class RemoteControl {
public:
    void submit(const std::shared_ptr<Command>& command) {
        command->execute();
    }
};

int main() {
    auto bulb = std::make_shared<Bulb>();
    auto turnOn = std::make_shared<TurnOn>(bulb);
    auto turnOff = std::make_shared<TurnOff>(bulb);

    RemoteControl remote;
    remote.submit(turnOn);
    std::cout << std::endl;
    remote.submit(turnOff);
    return 0;
}
```
Cuối cùng, hãy xem cách chúng ta có thể dùng nó trong client
```cpp
#include <iostream>
#include <memory>

class Bulb {
public:
    void turnOn() {
        std::cout << "Bulb has been lit";
    }

    void turnOff() {
        std::cout << "Darkness!";
    }
};

class Command {
public:
    virtual void execute() = 0;
    virtual void undo() = 0;
    virtual void redo() = 0;
    virtual ~Command() = default;
};

class TurnOn : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOn(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOn();
    }

    void undo() override {
        bulb->turnOff();
    }

    void redo() override {
        execute();
    }
};

class TurnOff : public Command {
protected:
    std::shared_ptr<Bulb> bulb;

public:
    explicit TurnOff(std::shared_ptr<Bulb> bulb) : bulb(std::move(bulb)) {}

    void execute() override {
        bulb->turnOff();
    }

    void undo() override {
        bulb->turnOn();
    }

    void redo() override {
        execute();
    }
};

class RemoteControl {
public:
    void submit(const std::shared_ptr<Command>& command) {
        command->execute();
    }
};

int main() {
    auto bulb = std::make_shared<Bulb>();
    auto turnOn = std::make_shared<TurnOn>(bulb);
    auto turnOff = std::make_shared<TurnOff>(bulb);

    RemoteControl remote;
    remote.submit(turnOn);
    std::cout << std::endl;
    remote.submit(turnOff);
    return 0;
}
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

```cpp
#include <algorithm>
#include <iostream>
#include <memory>
#include <vector>

class RadioStation {
protected:
    double frequency;

public:
    explicit RadioStation(double frequency) : frequency(frequency) {}

    double getFrequency() const {
        return frequency;
    }
};

class StationList {
protected:
    std::vector<std::shared_ptr<RadioStation>> stations;
    std::size_t counter = 0;

public:
    void addStation(std::shared_ptr<RadioStation> station) {
        stations.push_back(std::move(station));
    }

    void removeStation(const std::shared_ptr<RadioStation>& toRemove) {
        double toRemoveFrequency = toRemove->getFrequency();
        stations.erase(
            std::remove_if(stations.begin(), stations.end(),
                [toRemoveFrequency](const std::shared_ptr<RadioStation>& station) {
                    return station->getFrequency() == toRemoveFrequency;
                }),
            stations.end());
    }

    std::size_t count() const {
        return stations.size();
    }

    std::shared_ptr<RadioStation> current() const {
        return stations.at(counter);
    }

    std::size_t key() const {
        return counter;
    }

    void next() {
        ++counter;
    }

    void rewind() {
        counter = 0;
    }

    bool valid() const {
        return counter < stations.size();
    }

    auto begin() {
        return stations.begin();
    }

    auto end() {
        return stations.end();
    }
};

int main() {
    StationList stationList;

    stationList.addStation(std::make_shared<RadioStation>(89));
    stationList.addStation(std::make_shared<RadioStation>(101));
    stationList.addStation(std::make_shared<RadioStation>(102));
    stationList.addStation(std::make_shared<RadioStation>(103.2));

    for (const auto& station : stationList) {
        std::cout << station->getFrequency() << std::endl;
    }

    stationList.removeStation(std::make_shared<RadioStation>(89));
    return 0;
}
```
Tiếp theo, chúng ta có iterator của mình

```cpp
#include <algorithm>
#include <iostream>
#include <memory>
#include <vector>

class RadioStation {
protected:
    double frequency;

public:
    explicit RadioStation(double frequency) : frequency(frequency) {}

    double getFrequency() const {
        return frequency;
    }
};

class StationList {
protected:
    std::vector<std::shared_ptr<RadioStation>> stations;
    std::size_t counter = 0;

public:
    void addStation(std::shared_ptr<RadioStation> station) {
        stations.push_back(std::move(station));
    }

    void removeStation(const std::shared_ptr<RadioStation>& toRemove) {
        double toRemoveFrequency = toRemove->getFrequency();
        stations.erase(
            std::remove_if(stations.begin(), stations.end(),
                [toRemoveFrequency](const std::shared_ptr<RadioStation>& station) {
                    return station->getFrequency() == toRemoveFrequency;
                }),
            stations.end());
    }

    std::size_t count() const {
        return stations.size();
    }

    std::shared_ptr<RadioStation> current() const {
        return stations.at(counter);
    }

    std::size_t key() const {
        return counter;
    }

    void next() {
        ++counter;
    }

    void rewind() {
        counter = 0;
    }

    bool valid() const {
        return counter < stations.size();
    }

    auto begin() {
        return stations.begin();
    }

    auto end() {
        return stations.end();
    }
};

int main() {
    StationList stationList;

    stationList.addStation(std::make_shared<RadioStation>(89));
    stationList.addStation(std::make_shared<RadioStation>(101));
    stationList.addStation(std::make_shared<RadioStation>(102));
    stationList.addStation(std::make_shared<RadioStation>(103.2));

    for (const auto& station : stationList) {
        std::cout << station->getFrequency() << std::endl;
    }

    stationList.removeStation(std::make_shared<RadioStation>(89));
    return 0;
}
```
Và sau đó có thể dùng như sau
```cpp
#include <algorithm>
#include <iostream>
#include <memory>
#include <vector>

class RadioStation {
protected:
    double frequency;

public:
    explicit RadioStation(double frequency) : frequency(frequency) {}

    double getFrequency() const {
        return frequency;
    }
};

class StationList {
protected:
    std::vector<std::shared_ptr<RadioStation>> stations;
    std::size_t counter = 0;

public:
    void addStation(std::shared_ptr<RadioStation> station) {
        stations.push_back(std::move(station));
    }

    void removeStation(const std::shared_ptr<RadioStation>& toRemove) {
        double toRemoveFrequency = toRemove->getFrequency();
        stations.erase(
            std::remove_if(stations.begin(), stations.end(),
                [toRemoveFrequency](const std::shared_ptr<RadioStation>& station) {
                    return station->getFrequency() == toRemoveFrequency;
                }),
            stations.end());
    }

    std::size_t count() const {
        return stations.size();
    }

    std::shared_ptr<RadioStation> current() const {
        return stations.at(counter);
    }

    std::size_t key() const {
        return counter;
    }

    void next() {
        ++counter;
    }

    void rewind() {
        counter = 0;
    }

    bool valid() const {
        return counter < stations.size();
    }

    auto begin() {
        return stations.begin();
    }

    auto end() {
        return stations.end();
    }
};

int main() {
    StationList stationList;

    stationList.addStation(std::make_shared<RadioStation>(89));
    stationList.addStation(std::make_shared<RadioStation>(101));
    stationList.addStation(std::make_shared<RadioStation>(102));
    stationList.addStation(std::make_shared<RadioStation>(103.2));

    for (const auto& station : stationList) {
        std::cout << station->getFrequency() << std::endl;
    }

    stationList.removeStation(std::make_shared<RadioStation>(89));
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class User;

class ChatRoomMediator {
public:
    virtual void showMessage(const User& user, const std::string& message) = 0;
    virtual ~ChatRoomMediator() = default;
};

class User {
protected:
    std::string name;
    std::shared_ptr<ChatRoomMediator> chatMediator;

public:
    User(std::string name, std::shared_ptr<ChatRoomMediator> chatMediator)
        : name(std::move(name)), chatMediator(std::move(chatMediator)) {}

    std::string getName() const {
        return name;
    }

    void send(const std::string& message) const {
        chatMediator->showMessage(*this, message);
    }
};

class ChatRoom : public ChatRoomMediator {
public:
    void showMessage(const User& user, const std::string& message) override {
        std::string time = "Feb 14, 10:58 ";
        std::string sender = user.getName();
        std::cout << time << "[" << sender << "]:" << message;
    }
};

int main() {
    auto mediator = std::make_shared<ChatRoom>();

    User john("John Doe", mediator);
    User jane("Jane Doe", mediator);

    john.send("Hi there!");
    std::cout << std::endl;
    jane.send("Hey!");
    return 0;
}
```

Tiếp theo, chúng ta có các user, tức là colleagues
```cpp
#include <iostream>
#include <memory>
#include <string>

class User;

class ChatRoomMediator {
public:
    virtual void showMessage(const User& user, const std::string& message) = 0;
    virtual ~ChatRoomMediator() = default;
};

class User {
protected:
    std::string name;
    std::shared_ptr<ChatRoomMediator> chatMediator;

public:
    User(std::string name, std::shared_ptr<ChatRoomMediator> chatMediator)
        : name(std::move(name)), chatMediator(std::move(chatMediator)) {}

    std::string getName() const {
        return name;
    }

    void send(const std::string& message) const {
        chatMediator->showMessage(*this, message);
    }
};

class ChatRoom : public ChatRoomMediator {
public:
    void showMessage(const User& user, const std::string& message) override {
        std::string time = "Feb 14, 10:58 ";
        std::string sender = user.getName();
        std::cout << time << "[" << sender << "]:" << message;
    }
};

int main() {
    auto mediator = std::make_shared<ChatRoom>();

    User john("John Doe", mediator);
    User jane("Jane Doe", mediator);

    john.send("Hi there!");
    std::cout << std::endl;
    jane.send("Hey!");
    return 0;
}
```
Và cách sử dụng
```cpp
#include <iostream>
#include <memory>
#include <string>

class User;

class ChatRoomMediator {
public:
    virtual void showMessage(const User& user, const std::string& message) = 0;
    virtual ~ChatRoomMediator() = default;
};

class User {
protected:
    std::string name;
    std::shared_ptr<ChatRoomMediator> chatMediator;

public:
    User(std::string name, std::shared_ptr<ChatRoomMediator> chatMediator)
        : name(std::move(name)), chatMediator(std::move(chatMediator)) {}

    std::string getName() const {
        return name;
    }

    void send(const std::string& message) const {
        chatMediator->showMessage(*this, message);
    }
};

class ChatRoom : public ChatRoomMediator {
public:
    void showMessage(const User& user, const std::string& message) override {
        std::string time = "Feb 14, 10:58 ";
        std::string sender = user.getName();
        std::cout << time << "[" << sender << "]:" << message;
    }
};

int main() {
    auto mediator = std::make_shared<ChatRoom>();

    User john("John Doe", mediator);
    User jane("Jane Doe", mediator);

    john.send("Hi there!");
    std::cout << std::endl;
    jane.send("Hey!");
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <string>

class EditorMemento {
protected:
    std::string content;

public:
    explicit EditorMemento(std::string content) : content(std::move(content)) {}

    std::string getContent() const {
        return content;
    }
};

class Editor {
protected:
    std::string content;

public:
    void type(const std::string& words) {
        content = content + " " + words;
    }

    std::string getContent() const {
        return content;
    }

    std::shared_ptr<EditorMemento> save() const {
        return std::make_shared<EditorMemento>(content);
    }

    void restore(const std::shared_ptr<EditorMemento>& memento) {
        content = memento->getContent();
    }
};

int main() {
    Editor editor;
    editor.type("This is the first sentence.");
    editor.type("This is second.");

    auto saved = editor.save();
    editor.type("And this is third.");

    std::cout << editor.getContent() << std::endl;
    editor.restore(saved);
    std::cout << editor.getContent();
    return 0;
}
```

Tiếp theo, chúng ta có editor, tức originator, thành phần sẽ dùng memento object

```cpp
#include <iostream>
#include <memory>
#include <string>

class EditorMemento {
protected:
    std::string content;

public:
    explicit EditorMemento(std::string content) : content(std::move(content)) {}

    std::string getContent() const {
        return content;
    }
};

class Editor {
protected:
    std::string content;

public:
    void type(const std::string& words) {
        content = content + " " + words;
    }

    std::string getContent() const {
        return content;
    }

    std::shared_ptr<EditorMemento> save() const {
        return std::make_shared<EditorMemento>(content);
    }

    void restore(const std::shared_ptr<EditorMemento>& memento) {
        content = memento->getContent();
    }
};

int main() {
    Editor editor;
    editor.type("This is the first sentence.");
    editor.type("This is second.");

    auto saved = editor.save();
    editor.type("And this is third.");

    std::cout << editor.getContent() << std::endl;
    editor.restore(saved);
    std::cout << editor.getContent();
    return 0;
}
```

Và sau đó có thể dùng như sau

```cpp
#include <iostream>
#include <memory>
#include <string>

class EditorMemento {
protected:
    std::string content;

public:
    explicit EditorMemento(std::string content) : content(std::move(content)) {}

    std::string getContent() const {
        return content;
    }
};

class Editor {
protected:
    std::string content;

public:
    void type(const std::string& words) {
        content = content + " " + words;
    }

    std::string getContent() const {
        return content;
    }

    std::shared_ptr<EditorMemento> save() const {
        return std::make_shared<EditorMemento>(content);
    }

    void restore(const std::shared_ptr<EditorMemento>& memento) {
        content = memento->getContent();
    }
};

int main() {
    Editor editor;
    editor.type("This is the first sentence.");
    editor.type("This is second.");

    auto saved = editor.save();
    editor.type("And this is third.");

    std::cout << editor.getContent() << std::endl;
    editor.restore(saved);
    std::cout << editor.getContent();
    return 0;
}
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
```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class JobPost {
protected:
    std::string title;

public:
    explicit JobPost(std::string title) : title(std::move(title)) {}

    std::string getTitle() const {
        return title;
    }
};

class Observer {
public:
    virtual void onJobPosted(const JobPost& job) = 0;
    virtual ~Observer() = default;
};

class JobSeeker : public Observer {
protected:
    std::string name;

public:
    explicit JobSeeker(std::string name) : name(std::move(name)) {}

    void onJobPosted(const JobPost& job) override {
        std::cout << "Hi " << name << "! New job posted: " << job.getTitle();
    }
};

class Observable {
public:
    virtual void attach(std::shared_ptr<Observer> observer) = 0;
    virtual ~Observable() = default;
};

class EmploymentAgency : public Observable {
protected:
    std::vector<std::shared_ptr<Observer>> observers;

    void notify(const JobPost& jobPosting) {
        for (const auto& observer : observers) {
            observer->onJobPosted(jobPosting);
            std::cout << std::endl;
        }
    }

public:
    void attach(std::shared_ptr<Observer> observer) override {
        observers.push_back(std::move(observer));
    }

    void addJob(const JobPost& jobPosting) {
        notify(jobPosting);
    }
};

int main() {
    auto johnDoe = std::make_shared<JobSeeker>("John Doe");
    auto janeDoe = std::make_shared<JobSeeker>("Jane Doe");

    EmploymentAgency jobPostings;
    jobPostings.attach(johnDoe);
    jobPostings.attach(janeDoe);
    jobPostings.addJob(JobPost("Software Engineer"));
    return 0;
}
```
Tiếp theo, chúng ta có nơi đăng tin tuyển dụng mà người tìm việc sẽ đăng ký theo dõi
```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class JobPost {
protected:
    std::string title;

public:
    explicit JobPost(std::string title) : title(std::move(title)) {}

    std::string getTitle() const {
        return title;
    }
};

class Observer {
public:
    virtual void onJobPosted(const JobPost& job) = 0;
    virtual ~Observer() = default;
};

class JobSeeker : public Observer {
protected:
    std::string name;

public:
    explicit JobSeeker(std::string name) : name(std::move(name)) {}

    void onJobPosted(const JobPost& job) override {
        std::cout << "Hi " << name << "! New job posted: " << job.getTitle();
    }
};

class Observable {
public:
    virtual void attach(std::shared_ptr<Observer> observer) = 0;
    virtual ~Observable() = default;
};

class EmploymentAgency : public Observable {
protected:
    std::vector<std::shared_ptr<Observer>> observers;

    void notify(const JobPost& jobPosting) {
        for (const auto& observer : observers) {
            observer->onJobPosted(jobPosting);
            std::cout << std::endl;
        }
    }

public:
    void attach(std::shared_ptr<Observer> observer) override {
        observers.push_back(std::move(observer));
    }

    void addJob(const JobPost& jobPosting) {
        notify(jobPosting);
    }
};

int main() {
    auto johnDoe = std::make_shared<JobSeeker>("John Doe");
    auto janeDoe = std::make_shared<JobSeeker>("Jane Doe");

    EmploymentAgency jobPostings;
    jobPostings.attach(johnDoe);
    jobPostings.attach(janeDoe);
    jobPostings.addJob(JobPost("Software Engineer"));
    return 0;
}
```
Sau đó có thể dùng như sau
```cpp
#include <iostream>
#include <memory>
#include <string>
#include <vector>

class JobPost {
protected:
    std::string title;

public:
    explicit JobPost(std::string title) : title(std::move(title)) {}

    std::string getTitle() const {
        return title;
    }
};

class Observer {
public:
    virtual void onJobPosted(const JobPost& job) = 0;
    virtual ~Observer() = default;
};

class JobSeeker : public Observer {
protected:
    std::string name;

public:
    explicit JobSeeker(std::string name) : name(std::move(name)) {}

    void onJobPosted(const JobPost& job) override {
        std::cout << "Hi " << name << "! New job posted: " << job.getTitle();
    }
};

class Observable {
public:
    virtual void attach(std::shared_ptr<Observer> observer) = 0;
    virtual ~Observable() = default;
};

class EmploymentAgency : public Observable {
protected:
    std::vector<std::shared_ptr<Observer>> observers;

    void notify(const JobPost& jobPosting) {
        for (const auto& observer : observers) {
            observer->onJobPosted(jobPosting);
            std::cout << std::endl;
        }
    }

public:
    void attach(std::shared_ptr<Observer> observer) override {
        observers.push_back(std::move(observer));
    }

    void addJob(const JobPost& jobPosting) {
        notify(jobPosting);
    }
};

int main() {
    auto johnDoe = std::make_shared<JobSeeker>("John Doe");
    auto janeDoe = std::make_shared<JobSeeker>("Jane Doe");

    EmploymentAgency jobPostings;
    jobPostings.attach(johnDoe);
    jobPostings.attach(janeDoe);
    jobPostings.addJob(JobPost("Software Engineer"));
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;

    monkey.accept(speak);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    dolphin.accept(speak);
    return 0;
}
```
Tiếp theo, chúng ta có các phần cài đặt cho những con vật
```cpp
#include <iostream>
#include <memory>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;

    monkey.accept(speak);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    dolphin.accept(speak);
    return 0;
}
```
Hãy cài đặt visitor của chúng ta
```cpp
#include <iostream>
#include <memory>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;

    monkey.accept(speak);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    dolphin.accept(speak);
    return 0;
}
```

Và sau đó có thể dùng như sau
```cpp
#include <iostream>
#include <memory>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;

    monkey.accept(speak);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    dolphin.accept(speak);
    return 0;
}
```
Chúng ta hoàn toàn có thể làm điều này chỉ bằng một hệ phân cấp kế thừa cho các con vật, nhưng khi cần thêm hành động mới cho động vật thì lại phải sửa chính các class động vật. Còn bây giờ, chúng ta sẽ không phải thay đổi chúng. Ví dụ, giả sử cần thêm hành vi nhảy cho động vật, ta chỉ cần tạo một visitor mới như sau.

```cpp
#include <iostream>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

class Jump : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        (void)monkey;
        std::cout << "Jumped 20 feet high! on to the tree!";
    }

    void visitLion(Lion& lion) override {
        (void)lion;
        std::cout << "Jumped 7 feet! Back on the ground!";
    }

    void visitDolphin(Dolphin& dolphin) override {
        (void)dolphin;
        std::cout << "Walked on water a little and disappeared";
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;
    Jump jump;

    monkey.accept(speak);
    std::cout << std::endl;
    monkey.accept(jump);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    lion.accept(jump);
    std::cout << std::endl;
    dolphin.accept(speak);
    std::cout << std::endl;
    dolphin.accept(jump);
    return 0;
}
```
Và cách sử dụng
```cpp
#include <iostream>

class Monkey;
class Lion;
class Dolphin;

class AnimalOperation {
public:
    virtual void visitMonkey(Monkey& monkey) = 0;
    virtual void visitLion(Lion& lion) = 0;
    virtual void visitDolphin(Dolphin& dolphin) = 0;
    virtual ~AnimalOperation() = default;
};

class Animal {
public:
    virtual void accept(AnimalOperation& operation) = 0;
    virtual ~Animal() = default;
};

class Monkey : public Animal {
public:
    void shout() {
        std::cout << "Ooh oo aa aa!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitMonkey(*this);
    }
};

class Lion : public Animal {
public:
    void roar() {
        std::cout << "Roaaar!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitLion(*this);
    }
};

class Dolphin : public Animal {
public:
    void speak() {
        std::cout << "Tuut tuttu tuutt!";
    }

    void accept(AnimalOperation& operation) override {
        operation.visitDolphin(*this);
    }
};

class Speak : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        monkey.shout();
    }

    void visitLion(Lion& lion) override {
        lion.roar();
    }

    void visitDolphin(Dolphin& dolphin) override {
        dolphin.speak();
    }
};

class Jump : public AnimalOperation {
public:
    void visitMonkey(Monkey& monkey) override {
        (void)monkey;
        std::cout << "Jumped 20 feet high! on to the tree!";
    }

    void visitLion(Lion& lion) override {
        (void)lion;
        std::cout << "Jumped 7 feet! Back on the ground!";
    }

    void visitDolphin(Dolphin& dolphin) override {
        (void)dolphin;
        std::cout << "Walked on water a little and disappeared";
    }
};

int main() {
    Monkey monkey;
    Lion lion;
    Dolphin dolphin;
    Speak speak;
    Jump jump;

    monkey.accept(speak);
    std::cout << std::endl;
    monkey.accept(jump);
    std::cout << std::endl;
    lion.accept(speak);
    std::cout << std::endl;
    lion.accept(jump);
    std::cout << std::endl;
    dolphin.accept(speak);
    std::cout << std::endl;
    dolphin.accept(jump);
    return 0;
}
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

```cpp
#include <iostream>
#include <memory>
#include <vector>

class SortStrategy {
public:
    virtual std::vector<int> sort(const std::vector<int>& dataset) = 0;
    virtual ~SortStrategy() = default;
};

class BubbleSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using bubble sort";
        return dataset;
    }
};

class QuickSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using quick sort";
        return dataset;
    }
};

class Sorter {
protected:
    std::shared_ptr<SortStrategy> sorterSmall;
    std::shared_ptr<SortStrategy> sorterBig;

public:
    Sorter(std::shared_ptr<SortStrategy> sorterSmall, std::shared_ptr<SortStrategy> sorterBig)
        : sorterSmall(std::move(sorterSmall)), sorterBig(std::move(sorterBig)) {}

    std::vector<int> sort(const std::vector<int>& dataset) {
        if (dataset.size() > 5) {
            return sorterBig->sort(dataset);
        }
        return sorterSmall->sort(dataset);
    }
};

int main() {
    std::vector<int> smalldataset{1, 3, 4, 2};
    std::vector<int> bigdataset{1, 4, 3, 2, 8, 10, 5, 6, 9, 7};

    Sorter sorter(std::make_shared<BubbleSortStrategy>(), std::make_shared<QuickSortStrategy>());
    sorter.sort(smalldataset);
    std::cout << std::endl;
    sorter.sort(bigdataset);
    return 0;
}
```

Tiếp theo, chúng ta có client sẽ sử dụng bất kỳ strategy nào
```cpp
#include <iostream>
#include <memory>
#include <vector>

class SortStrategy {
public:
    virtual std::vector<int> sort(const std::vector<int>& dataset) = 0;
    virtual ~SortStrategy() = default;
};

class BubbleSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using bubble sort";
        return dataset;
    }
};

class QuickSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using quick sort";
        return dataset;
    }
};

class Sorter {
protected:
    std::shared_ptr<SortStrategy> sorterSmall;
    std::shared_ptr<SortStrategy> sorterBig;

public:
    Sorter(std::shared_ptr<SortStrategy> sorterSmall, std::shared_ptr<SortStrategy> sorterBig)
        : sorterSmall(std::move(sorterSmall)), sorterBig(std::move(sorterBig)) {}

    std::vector<int> sort(const std::vector<int>& dataset) {
        if (dataset.size() > 5) {
            return sorterBig->sort(dataset);
        }
        return sorterSmall->sort(dataset);
    }
};

int main() {
    std::vector<int> smalldataset{1, 3, 4, 2};
    std::vector<int> bigdataset{1, 4, 3, 2, 8, 10, 5, 6, 9, 7};

    Sorter sorter(std::make_shared<BubbleSortStrategy>(), std::make_shared<QuickSortStrategy>());
    sorter.sort(smalldataset);
    std::cout << std::endl;
    sorter.sort(bigdataset);
    return 0;
}
```
Và nó có thể được dùng như sau
```cpp
#include <iostream>
#include <memory>
#include <vector>

class SortStrategy {
public:
    virtual std::vector<int> sort(const std::vector<int>& dataset) = 0;
    virtual ~SortStrategy() = default;
};

class BubbleSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using bubble sort";
        return dataset;
    }
};

class QuickSortStrategy : public SortStrategy {
public:
    std::vector<int> sort(const std::vector<int>& dataset) override {
        std::cout << "Sorting using quick sort";
        return dataset;
    }
};

class Sorter {
protected:
    std::shared_ptr<SortStrategy> sorterSmall;
    std::shared_ptr<SortStrategy> sorterBig;

public:
    Sorter(std::shared_ptr<SortStrategy> sorterSmall, std::shared_ptr<SortStrategy> sorterBig)
        : sorterSmall(std::move(sorterSmall)), sorterBig(std::move(sorterBig)) {}

    std::vector<int> sort(const std::vector<int>& dataset) {
        if (dataset.size() > 5) {
            return sorterBig->sort(dataset);
        }
        return sorterSmall->sort(dataset);
    }
};

int main() {
    std::vector<int> smalldataset{1, 3, 4, 2};
    std::vector<int> bigdataset{1, 4, 3, 2, 8, 10, 5, 6, 9, 7};

    Sorter sorter(std::make_shared<BubbleSortStrategy>(), std::make_shared<QuickSortStrategy>());
    sorter.sort(smalldataset);
    std::cout << std::endl;
    sorter.sort(bigdataset);
    return 0;
}
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

```cpp
#include <memory>
#include <stdexcept>
#include <string>

class PhoneState {
public:
    virtual std::shared_ptr<PhoneState> pickUp() = 0;
    virtual std::shared_ptr<PhoneState> hangUp() = 0;
    virtual std::shared_ptr<PhoneState> dial() = 0;
    virtual ~PhoneState() = default;
};

class PhoneStateIdle;
class PhoneStatePickedUp;
class PhoneStateCalling;

class PhoneStateIdle : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStatePickedUp : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStateCalling : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

std::shared_ptr<PhoneState> PhoneStateIdle::pickUp() {
    return std::make_shared<PhoneStatePickedUp>();
}

std::shared_ptr<PhoneState> PhoneStateIdle::hangUp() {
    throw std::runtime_error("already idle");
}

std::shared_ptr<PhoneState> PhoneStateIdle::dial() {
    throw std::runtime_error("unable to dial in idle state");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::dial() {
    return std::make_shared<PhoneStateCalling>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStateCalling::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::dial() {
    throw std::runtime_error("already dialing");
}

class Phone {
private:
    std::shared_ptr<PhoneState> state;

public:
    Phone() : state(std::make_shared<PhoneStateIdle>()) {}

    void pickUp() {
        state = state->pickUp();
    }

    void hangUp() {
        state = state->hangUp();
    }

    void dial() {
        state = state->dial();
    }
};

int main() {
    Phone phone;
    phone.pickUp();
    phone.dial();
    return 0;
}
```

Tiếp theo, chúng ta có class Phone thay đổi state theo các lời gọi hành vi khác nhau

```cpp
#include <memory>
#include <stdexcept>
#include <string>

class PhoneState {
public:
    virtual std::shared_ptr<PhoneState> pickUp() = 0;
    virtual std::shared_ptr<PhoneState> hangUp() = 0;
    virtual std::shared_ptr<PhoneState> dial() = 0;
    virtual ~PhoneState() = default;
};

class PhoneStateIdle;
class PhoneStatePickedUp;
class PhoneStateCalling;

class PhoneStateIdle : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStatePickedUp : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStateCalling : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

std::shared_ptr<PhoneState> PhoneStateIdle::pickUp() {
    return std::make_shared<PhoneStatePickedUp>();
}

std::shared_ptr<PhoneState> PhoneStateIdle::hangUp() {
    throw std::runtime_error("already idle");
}

std::shared_ptr<PhoneState> PhoneStateIdle::dial() {
    throw std::runtime_error("unable to dial in idle state");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::dial() {
    return std::make_shared<PhoneStateCalling>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStateCalling::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::dial() {
    throw std::runtime_error("already dialing");
}

class Phone {
private:
    std::shared_ptr<PhoneState> state;

public:
    Phone() : state(std::make_shared<PhoneStateIdle>()) {}

    void pickUp() {
        state = state->pickUp();
    }

    void hangUp() {
        state = state->hangUp();
    }

    void dial() {
        state = state->dial();
    }
};

int main() {
    Phone phone;
    phone.pickUp();
    phone.dial();
    return 0;
}
```

Và sau đó có thể dùng như sau, khi đó nó sẽ gọi các method state tương ứng:

```cpp
#include <memory>
#include <stdexcept>
#include <string>

class PhoneState {
public:
    virtual std::shared_ptr<PhoneState> pickUp() = 0;
    virtual std::shared_ptr<PhoneState> hangUp() = 0;
    virtual std::shared_ptr<PhoneState> dial() = 0;
    virtual ~PhoneState() = default;
};

class PhoneStateIdle;
class PhoneStatePickedUp;
class PhoneStateCalling;

class PhoneStateIdle : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStatePickedUp : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

class PhoneStateCalling : public PhoneState {
public:
    std::shared_ptr<PhoneState> pickUp() override;
    std::shared_ptr<PhoneState> hangUp() override;
    std::shared_ptr<PhoneState> dial() override;
};

std::shared_ptr<PhoneState> PhoneStateIdle::pickUp() {
    return std::make_shared<PhoneStatePickedUp>();
}

std::shared_ptr<PhoneState> PhoneStateIdle::hangUp() {
    throw std::runtime_error("already idle");
}

std::shared_ptr<PhoneState> PhoneStateIdle::dial() {
    throw std::runtime_error("unable to dial in idle state");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStatePickedUp::dial() {
    return std::make_shared<PhoneStateCalling>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::pickUp() {
    throw std::runtime_error("already picked up");
}

std::shared_ptr<PhoneState> PhoneStateCalling::hangUp() {
    return std::make_shared<PhoneStateIdle>();
}

std::shared_ptr<PhoneState> PhoneStateCalling::dial() {
    throw std::runtime_error("already dialing");
}

class Phone {
private:
    std::shared_ptr<PhoneState> state;

public:
    Phone() : state(std::make_shared<PhoneStateIdle>()) {}

    void pickUp() {
        state = state->pickUp();
    }

    void hangUp() {
        state = state->hangUp();
    }

    void dial() {
        state = state->dial();
    }
};

int main() {
    Phone phone;
    phone.pickUp();
    phone.dial();
    return 0;
}
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
```cpp
#include <iostream>

class Builder {
public:
    virtual ~Builder() = default;

    virtual void build() final {
        test();
        lint();
        assemble();
        deploy();
    }

    virtual void test() = 0;
    virtual void lint() = 0;
    virtual void assemble() = 0;
    virtual void deploy() = 0;
};

class AndroidBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running android tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the android code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the android build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying android build to server" << std::endl;
    }
};

class IosBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running ios tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the ios code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the ios build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying ios build to server" << std::endl;
    }
};

int main() {
    AndroidBuilder androidBuilder;
    androidBuilder.build();

    IosBuilder iosBuilder;
    iosBuilder.build();
    return 0;
}
```

Sau đó, chúng ta có thể có các phần cài đặt cụ thể

```cpp
#include <iostream>

class Builder {
public:
    virtual ~Builder() = default;

    virtual void build() final {
        test();
        lint();
        assemble();
        deploy();
    }

    virtual void test() = 0;
    virtual void lint() = 0;
    virtual void assemble() = 0;
    virtual void deploy() = 0;
};

class AndroidBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running android tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the android code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the android build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying android build to server" << std::endl;
    }
};

class IosBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running ios tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the ios code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the ios build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying ios build to server" << std::endl;
    }
};

int main() {
    AndroidBuilder androidBuilder;
    androidBuilder.build();

    IosBuilder iosBuilder;
    iosBuilder.build();
    return 0;
}
```
Và sau đó có thể dùng như sau

```cpp
#include <iostream>

class Builder {
public:
    virtual ~Builder() = default;

    virtual void build() final {
        test();
        lint();
        assemble();
        deploy();
    }

    virtual void test() = 0;
    virtual void lint() = 0;
    virtual void assemble() = 0;
    virtual void deploy() = 0;
};

class AndroidBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running android tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the android code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the android build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying android build to server" << std::endl;
    }
};

class IosBuilder : public Builder {
public:
    void test() override {
        std::cout << "Running ios tests" << std::endl;
    }

    void lint() override {
        std::cout << "Linting the ios code" << std::endl;
    }

    void assemble() override {
        std::cout << "Assembling the ios build" << std::endl;
    }

    void deploy() override {
        std::cout << "Deploying ios build to server" << std::endl;
    }
};

int main() {
    AndroidBuilder androidBuilder;
    androidBuilder.build();

    IosBuilder iosBuilder;
    iosBuilder.build();
    return 0;
}
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
