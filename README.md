## Javascript: Execution Context là gì?Call Stack là gì?

Execution Context trong Javascript là gì? 

Tôi cá là bạn không biết câu trả lời.

Các thành phần cơ bản nhất của ngôn ngữ lập trình là gì?

Các biến và hàm phải không? Mọi người đều có thể học những thứ này.

Nhưng những gì nằm ngoài những điều cơ bản?

Những nền tảng của Javascript mà bạn nên làm chủ trước khi tự gọi mình là nhà phát triển Javascript ở le vồ mức trung (hoặc thậm chí mức cao) là gì?

Có rất nhiều thứ như: Scope, Closure, Callbacks, Prototype, và nhiều hơn nữa..

Nhưng trước khi đi sâu vào các khái niệm này, ít nhất bạn nên hiểu cách hoạt động của công cụ Javascript.

Trong bài này, chúng tôi sẽ giới thiệu hai phần cơ bản của mọi công cụ Javascript:Execution Context và the Call Stack.

(Đừng sợ. Nó dễ hơn bạn nghĩ)

Sẵn sàng chưa?

Tài liệu này là một phần của lớp Javascript nâng cao của tôi có sẵn khi đào tạo trực tuyến 1-1  hoặc đào tạo tại chỗ ở châu Âu.

### Javascript: Execution Context là gì? bạn sẽ học được những gi
Trong bài đăng này, bạn sẽ tìm hiểu về:
Cách công cụ Javascript hoạt động
Call Stack là gì
sự khác biệt giữa Execution Context toàn cục và Execution Context cục bộ

### Javascript: Execution Context là gì? Javascript chạy mã của bạn như thế nào?
Javascript chạy code của bạn như thế nào?
Nếu bạn là một senior developer, bạn có thể đã biết câu trả lời.
Nếu bạn là người mới bắt đầu, chúng ta sẽ cùng nhau tìm hiểu.
Sự thật là,Tổng quan về Javascript không dễ dàng.
Nhưng tôi đảm bảo bạn có thể học chúng.
Và khi bạn học, bạn sẽ cảm thấy được khai sáng và thông minh hơn.
Bằng cách xem xét chức năng bên trong Javascript, bạn sẽ trở thành một nhà phát triển Javascript tốt hơn, ngay cả khi bạn không thể nắm vững từng chi tiết.
Bây giờ, hãy xem đoạn mã sau:
```
var num = 2;

function pow(num) {
    return num * num;
}
```

xong?

Nó trông không khó nhỉ!

Bây giờ hãy cho tôi biết: theo thứ tự nào bạn nghĩ trình duyệt sẽ đánh giá code đó?

Nói cách khác, nếu bạn là trình duyệt, bạn sẽ đọc đoạn code đó như thế nào?

Nghe có vẻ dễ dàng.

Hầu hết mọi người nghĩ rằng "yeah, trình duyệt thực hiện hàm pow và trả về kết quả, sau đó nó gán 2 đến num."

Bạn có muốn biết câu trả lời của tôi không?

Từ trên xuống dưới

Trình duyệt sẽ bắt đầu ở hàm pow, tính num * num

JS engine sẽ chạy dòng mã theo dòng (loại)

Tôi đã mong đợi điều đó.

Tôi đã nói chính xác những điều này năm trước.

Trong các phần tiếp theo, bạn sẽ khám phá ra cơ chế  đằng sau những dòng mã đơn giản đó.

### Javascript: Execution Context là gì? Javascript Engines

Bạn có muốn trở thành một nhà phát triển Javascript mức trung không?

Tôi cá là bạn sẽ không làm thế.

Nếu bạn muốn tạo ấn tượng tốt trong một cuộc phỏng vấn Javascript, ít nhất bạn nên biết cách Javascript chạy mã của bạn.

(Và một loạt các thứ khác mà tôi sẽ không bao gồm ở đây).

Đừng vội vàng về những khái niệm này.

Bạn không thể học mọi thứ trong một ngày. Nó sẽ tốn thời gian.

Tin tốt đây? Tôi sẽ làm cho mọi thứ trở nên dễ hiểu đối với mọi người (ít nhất tôi sẽ thử).

Để hiểu cách Javascript chạy mã của bạn, chúng ta phải đáp ứng điều đáng sợ đầu tiên: Execution Contexti.

 Execution Context trong Javascript là gì?

Mỗi khi bạn chạy Javascript trong một trình duyệt (hoặc trong Node), engine sẽ trải qua một loạt các bước.

Một trong những bước này liên quan đến việc tạo ra  Execution Context toàn cục.

Nhưng chờ đã, engine là gì?

Đó là, Javascript engine là "động cơ" chạy mã Javascript.

Ngày nay có hai Javascript engine nổi bật: Google V8 và SpiderMonkey.

V8 là công cụ JavaScript mã nguồn mở của Google, được sử dụng trong Google Chrome và Node.js.

SpiderMonkey là công cụ JavaScript của Mozilla, được sử dụng trong Firefox.

Cho đến nay chúng ta có công cụ Javascript và một Execution Context

Bây giờ là lúc để hiểu cách họ làm việc cùng nhau.

### Javascript: Execution Context là gì? Nó hoạt động như thế nào?
engine tạo ra mộtExecution Context toàn cục mỗi khi bạn chạy một số mã Javascript.

Execution Context là một từ ưa thích để mô tả môi trường mà mã Javascript của bạn chạy.

Thật khó để hình dung những điều trừu tượng này, tôi cảm thấy như bạn vậy.

Bây giờ hãy nghĩ về Execution Context toàn cục như một cái hộp:

Execution Context toàn cục

Hãy xem lại mã của chúng ta:
```
var num = 2;

function pow(num) {
    return num * num;
}
```

engine đọc mã đó như thế nào?

Đây là một phiên bản đơn giản:

Engine: Dòng một. Có một biến! Thật tuyệt. Hãy lưu trữ nó trong Bộ nhớ toàn cục.

Engine: Dòng ba. Tôi thấy một hàm khai báo.Tuyệt dzời. Hãy lưu trữ nó trong Bộ nhớ toàn cục!

Engine: Có vẻ như tôi đã làm xong rồi.

Nếu tôi hỏi lại bạn: trình duyệt "xem" mã sau đây như thế nào, bạn sẽ nói gì?

Ừ, nó là từ trên xuống nhưng…

Như bạn có thể thấy động cơ không chạy chức năng pow!

Đó là một khai báo hàm, không phải là một lời gọi hàm.

Đoạn mã trên sẽ dịch thành một số giá trị được lưu trong Global Memory: một khai báo hàm và một biến.

Bộ nhớ toàn cục?

Valentino, tôi đã nhầm lẫn với  Execution Context và bây giờ bạn đang ném bộ nhớ toàn cục vào tôi?

Vâng là tôi.

Hãy xem Bộ nhớ toàn cục là gì.

### Javascript:  Execution Context là gì? Bộ nhớ toàn cục

Javascript engine cũng có Bộ nhớ chung.

Bộ nhớ toàn cục chứa các biến toàn cục và các khai báo hàm để sử dụng sau này.

Nếu bạn đọc “Scope and Closures” của Kyle Simpson, bạn có thể thấy rằng Bộ nhớ toàn cục trùng lặp với khái niệm Phạm vi toàn cục.

Trong thực tế, họ là những điều tương tự.

Tôi đang bay cao 10.000 feet ở đây, vì một lý do chính đáng.

Đó là những khái niệm khó.

Nhưng bây giờ bạn không nên lo lắng.

Tôi muốn bạn hiểu hai phần quan trọng trong câu đố của chúng tôi.

Khi công cụ Javascript chạy mã của bạn, nó tạo ra:

Execution Context toàn cục

Bộ nhớ toàn cục (còn được gọi là Phạm vi toàn cục hoặc Môi trường biến toàn cục)

Mọi thứ có rõ ràng không?

Nếu tôi là bạn vào thời điểm này, tôi sẽ:

viết xuống một số mã Javascript

phân tích cú pháp mã từng bước khi bạn là động cơ

tạo một biểu diễn đồ họa của cả bối cảnh Global Execution và Global Memory trong quá trình thực hiện

Bạn có thể viết bài tập trên giấy hoặc bằng công cụ tạo mẫu.

Đối với ví dụ nhỏ của tôi, hình ảnh sẽ như sau:

Một đại diện đồ họa của Execution Context Javascript / bộ nhớ toàn cục

Trong phần tiếp theo, chúng ta sẽ xem xét một điều đáng sợ khác: Call Stack.

### Javascript: Execution Context là gì? Call Stack là gì?
Bạn có một bức tranh rõ ràng về cách Execution Context, bộ nhớ toàn cục và công cụ Javascript phù hợp với nhau không?

Nếu không dành thời gian của bạn để xem lại phần trước.

Chúng tôi sẽ giới thiệu một phần khác trong câu đố của chúng tôi: Call Stack.

Hãy xem điều gì xảy ra trong quá trình thực thi mã.

Trước tiên, hãy tóm tắt lại những gì xảy ra khi Javascript engine chạy mã của bạn.

Nó tạo ra:

Execution Context toàn cục

một bộ nhớ toàn cục

Bên cạnh đó trong ví dụ của chúng tôi không có gì xảy ra nữa
```
var num = 2;

function pow(num) {
    return num * num;
}
```

Mã này là một phân bổ thuần túy các giá trị.

Hãy tiến thêm một bước nữa.

Điều gì xảy ra nếu tôi gọi hàm này?

```
var num = 2;

function pow(num) {
    return num * num;
}

var res = pow(num);

```

Câu hỏi rất thú vị.

Các hành động gọi một chức năng trong Javascript làm cho engine yêu cầu giúp đỡ.

Và sự trợ giúp đó đến từ một người bạn của engine Javascript: Call Stack.

Nó có thể không rõ ràng nhưng công cụ Javascript cần phải theo dõi những gì đang xảy ra.

Nó dựa trên Call Stack cho điều đó.

Call Stack trong Javascript là gì?

Call Stack giống như nhật ký thực hiện chương trình hiện tại.

Trong thực tế nó là một cấu trúc dữ liệu: a stack.

Call Stack chính xác hoạt động như thế nào?

Không có gì đáng ngạc nhiên khi nó có hai phương pháp: push và pop.

Đẩy là hành động đưa thứ gì đó vào ngăn xếp.

Tức là, khi bạn chạy một hàm trong Javascript, công cụ sẽ đẩy hàm đó vào trong Call Stack

Mọi Call Stack đều được đẩy vào Ngăn xếp cuộc gọi.

Điều đầu tiên được đẩy là main () (hoặc global ()), luồng chính của việc thực hiện chương trình Javascript của bạn.

Bây giờ, hình ảnh trước sẽ trông như sau:

Call Stack Javascript

Popping ở đầu bên kia là hành động loại bỏ thứ gì đó từ stack.

Khi một hàm kết thúc thực thi nó sẽ xuất hiện từ Call Stacki.

Và Call Stack của chúng tôi sẽ giống như sau:

Call Stack Javascript Pop

Và bây giờ bạn đã sẵn sàng để làm chủ mọi khái niệm Javascript trên mạng.

Nhưng ở đâu chưa xong! Chuyển đến phần tiếp theo!

### Javascript nâng cao: Execution Context? Execution Context cục bộ

Mọi thứ dường như rõ ràng cho đến hiện tại.

Chúng ta đang thiếu một cái gì đó?

Chúng ta biết rằng các công cụ Javascript tạo ra mộ tExecution Context toàn cục và một bộ nhớ toàn cục.

Sau đó, khi bạn gọi một hàm trong mã của bạn:

Javascript engine yêu cầu trợ giúp

sự trợ giúp đó đến từ một người bạn của công cụ Javascript: Call stack

Call stack theo dõi các chức năng đang được gọi trong mã của bạn

Tuy nhiên, một điều khác đã xảy ra khi bạn chạy một hàm trong Javascript.

Đầu tiên, hàm xuất hiện trong Execution Context Toàn cục.

Sau đó, một ngữ cảnh nhỏ khác xuất hiện cùng với chức năng.

Hộp nhỏ mới này được gọi là  Execution Context cục bộ.

Một Execution Context cục bộ được tạo bên trong hàm đó!

Cái gì??

Nếu bạn nhận thấy, trong hình trước đó một biến mới xuất hiện trong bộ nhớ toàn cục: var res.

Các biến res có giá trị không xác định lúc đầu.

Sau đó ngay khi pow xuất hiện trong Global Execution Context, hàm thực hiện và res lấy giá trị trả về của nó.

Trong suốt giai đoạn thực thi, một Local Execution Context được tạo ra, cùng với một Local Memory để giữ các biến cục bộ.

Thật là một khái niệm mạnh mẽ.

 Execution Context cục bộ

Hãy Ghi nhớ nó trong tâm trí bạn.

Hiểu cảExecution Context Toàn cục và cục bộ là chìa khóa để làm chủ scope và closures

### Javascript: Execution Context là gì? Call stack là gì? Gói gọn chúng lại nào

Bạn có thể tin những gì đằng sau 4 dòng mã không?

Công cụ Javascript tạo ra một Execution Context, một bộ nhớ toàn cục và một call stack.

Nhưng một khi bạn gọi một hàm, engine sẽ tạo ra một Local Execution Context có một Local Memory.

Đến cuối bài viết này, bạn sẽ có thể hiểu những gì sẽ xảy ra khi bạn chạy một số mã Javascript.

Thường bị bỏ qua, nội dung Javascript luôn được xem là những điều misterious bởi các nhà phát triển mới.

Tuy nhiên, chúng là chìa khóa để làm chủ các khái niệm Javascript nâng cao.

Nếu bạn học  Execution Context, bộ nhớ toàn cục và call stacki, thì scope, closures,Callback và các nội dung khác sẽ easy như một trò đùa.

Đặc biệt, sự hiểu biết Call Stack là tối quan trọng.

Tất cả các Javascript sẽ bắt đầu có ý nghĩa một khi bạn hình dung nó: cuối cùng bạn sẽ hiểu tại sao Javascript là không đồng bộ và tại sao chúng ta cần Callbacks.
Bạn có biết những gì đằng sau 4 dòng mã Javascript không?

Bây giờ bạn biết rồi đấy.

Cảm ơn vì đã theo dõi!
