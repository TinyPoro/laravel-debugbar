## ITCSS: KĨ THUẬT MỞ RỘNG BẢO TRÌ CSS 
Lubos Kmetko ngày 10 tháng 2, 2016 
### Làm thế nào để khiến css có thể mở rộng và bảo trì ?Nó là 1 vấn đề cần quan tâm của mỗi lập trình viên front-end. Và ITCSS sẽ là câu trả lời cho họ.

Năm ngoái khi tôi bắt đầu lên kế hoạch thiết kế lại [HEROized](https://www.heroized.com/) và thiết kế cho trang mới Xfive.co, tôi đa tìm kiếm một kĩ thuật CSS cho phép dễ dàng phát triển trang web của mình cũng như là bảo trì về sau.

[CSS Modules](http://www.sitepoint.com/understanding-css-modules-methodology/) lúc bấy giờ vẫn đang trong những giai đoạn đầu phát triển và còn khá mới mẻ và tôi luôn luôn cho rằng sự tương đồng trong cấu trúc [Atomic Design](http://patternlab.io/) thì sẽ nhân tạo hơn. Sau đó tôi bắt gặp ITCSS của [Roberts’s](https://csswizardry.com/) trong những vấn đề của [net magazine](https://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731) tháng 6 năm 2015 và tôi gần như ngay lập tức bị mê hoặc bởi sự đơn giản, thực tế trong cách nó tiếp cận CSS.

 ### vậy ITCSS là gì?
 ITCSS đại diện cho Inverted Triangle CSS và nó giúp bạn tổ chức các file CSS trong dự án của bạn sao cho bạn có thể **giải quyết** những vấn đề liên quan đến CSS(mà không phải lúc nào cũng dễ giái quyết) như **global namespace, cascade và selectors specificity**.
ITCSS có thể được sử dụng với các bộ tiền xử lý hoặc cũng có thể không và nó tương thích với các phương pháp luận CSS như BEM, SMACSS hoặc OOCSS.
Một trong nhưngx nguyên tắc quan trọng của ITCSS là nó chia codebase CSS của bạn thành một vài phần nhỏ (gọi là các lớp), có dạng của tam giác ngược như hình vẽ:
![inverted triangle](https://other.media/wp-content/uploads/2017/01/itcss_2.png)
Thông tin chi tiết về các lớp như sau:
 - Settings (các cài đặt) - dùng với các tiền xử lý và bao gồm phông chứ, định nghĩa màu sắc, vân vân.
 - Tool (công cụ) - sử dụng các mixins và các hàm ở mức global. Điều quan trọng là không được ghi bất kỳ CSS nào ở 2 lớp đầu tiên.
 - Generic (chung) - cài đặt lại và/hoặc tiêu chuẩn hóa các mẫu (styles), định nghĩa kích thước các box, vân vân. Đây là lớp đầu tạo ra CSS.
 - Elements (phần tử) - tạo mẫu cho các phần tử HTML cở bản ( như H1, a, vân vân). Mặc định nó sẽ theo những mẫu của trình duyệt và bạn có thể định nghĩa lại chúng ở đây.
 - Objects (đối tượng) - bộ chọn (selectors) dựa trên lớp, định nghĩa các mẫu thiết kế chưa được trang trí, ví dụ như đối tượng media từ OOCSS.
 - Components (thành phần) - đặc tả các thành phần UI. Phần lớn công việc của chúng ta là ở đây và các thành phần UI thường bao gồm các Đối tượng và các Thành phần.
 - Utilities (tiện ích) - các tiện tích và các lớp hỗ trợ với khả năng ghi đè bất cứ thứ gì phía trước trong "tam giác", ví dụ lớp hỗ trợ hide.
"Tam giác" cũng cho chúng ta thấy các mẫu, được đại diện bởi các bộ chọn, được sắp xếp trong kết quả CSS như thế nào : từ nhưng mẫu chung nhất cho đến những mẫu riêng biệt, từ những bộ chọn ít cụ thể đến những bộ chọn cụ thể hơn (nhưng vẫn không quá cụ thế, và ID thì không được phép) và từ những cái có thể ảnh hượng rộng rãi đến những cái ít ảnh hưởng hơn.
![inverted triangle](https://other.media/wp-content/uploads/2017/01/itcss_1.png)
Như vậy, cấu tạo CSS sẽ giúp bạn tránh các Specificity Wars và được đại diện bởi [một biểu đồ đặc thù lành mành](https://jonassebastianohlsson.com/specificity-graph/)
 ### Tài liệu
Cập nhật ngày 27 tháng 10 năm 2016 : net magazine vừa mới tái xuất bản bài báo gốc từ phiên bản tạp chí (xem nguồn bên dưới)
Bình thường thì lúc này tôi sẽ bảo các bạn tới các [trang web về ITCSS](https://itcss.io/) để tìm hiểu sâu hơn. Nhưng tiếc thay hiện giờ không có tài liệu mã nguồn mở nào cả.
ITCSS hiện nãy vẫn còn một phần thuộc sở hữu độc quyền nên nếu bạn muốn hoàn toàn sử dụng nó, bạn nên đọc bài giới thiệu gốc từ net magazine. Tôi không ở đây để phán xét quyết định của tác giả (tôi cảm ơn ông ý vì đã chia sẻ kiến thức), nhưng tôi nghĩ điều này sẽ ngăn cản ITCSS được kế thừa rộng rãi (có thể đây chính là chủ ý của ông ấy).
 > Tính độc quyền một phần của ITCSS sẽ ngăn nó được ekes thể rộng rãi

Các bạn không nên vì điều này mà không bắt đầu sử dụng nó trong các dự án của mình nếu bạn thực sự thích nó. Xem các [vấn đề đặc biệt](https://www.myfavouritemagazines.co.uk/design/net-magazine-back-issues/) của net magazine để học các vấn đề cơ bản của ITCSS, và sau đó bạn có thể học từ các nguồn online và qua các ví dụ áp dụng nó trong các dự án thực tế.
### Nguồn
Tôi đã sử dụng ITCSS cho 4 dự án gần đây (bao gồm cả Xfive.co) và nhưng nguồn dưới đây đã giúp tôi hiểu về nó nhiều hơn.
 - [Quản lý dự án CSS lớn với ITCSS](http://www.creativebloq.com/web-design/manage-large-css-projects-itcss-101517528) - giới thiệu ITCSS của Harry Roberts (bài báo gốc được xuất bản từ phiên bản tạp chí, thiếu 1 vài cột ở biểu đồ đặc thù và bộ tiền xử lý)
 - [Quản lý trang dự án web qui mô lớn với kĩ thuật CSS mới ITCSS](https://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731) - giới thiệu ITCSS và phỏng vấn Harry Roberts.
 - [Harry Roberts - Quản lý dứ án CSS với ITCSS](https://www.youtube.com/watch?v=1OKZOV-iLj4) - cuộc nói chuyện của Harry tại DaFED và các [slide kèm theo](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)
 - [Quản lý dự án CSS lớn với ITCSS](https://www.youtube.com/watch?v=hz76JIU_xB0) - một screencast(kiểu video tutorial) cho các bài báo.
 - [ITCSS Screencast code](https://github.com/itcss/itcss-netmag) -  mã nguồn từ screencast phía trên trên github.
 - [Các dự án mẫu ITCSS khác](https://github.com/csswizardry/frcss)
 - Các bài báo tại địa chỉ csswizardry.com và đặc biệt là các bài dưới đây:
    - [BEMIT: Quy ước đặt tên BEM mở rộng](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)
    - [Code UI sáng sủa hơn với Namespaces](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
    - [CSS bất biến](https://csswizardry.com/2015/03/immutable-css/)
    - [Biểu đồ đặc thù](https://csswizardry.com/2014/10/the-specificity-graph/)
 - [inuitcss](https://github.com/inuitcss/inuitcss) - framework OOCSS dựa trên ITCSS, cải tiến 1 số khái niệm và 1 số chức năng.
 - [Qui ước đặt tên BEMIT](http://www.jamesturneronline.net/blog/bemit-naming-convention.html)
Bạn cũng có thể xem qua [Chisel](https://github.com/xfiveco/generator-chisel/), bộ sinh Yeoman cho các dự án front-end và WordPress của chúng tôi, nó có hỗ trợ ITCSS.
 ### Kinh nghiệm
Sau đây là 1 vài suy nghĩ của tôi dựa trên những kĩnh nghiệm tích lũy được qua các dự án ITCSS
 ##### Nghĩ ít hơn về việc đặt tên hay tạo mẫu vị trí
Bản chất tự nhiên của ITCSS, đặc biệt khi kết hợp với [qui ước đặt tên BEMIT](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/) cho phép bạn tập trung vài việc giải quyết các thách thức front-end thay vì nghĩ về tên gọi hay mẫu của các vị trí. Đây, file main.css của Xfive.co có dạng thế này:
```
@import "settings.colors";
@import "settings.global";

@import "tools.mixins";

@import "normalize-scss/normalize.scss";
@import "generic.reset";
@import "generic.box-sizing";
@import "generic.shared";

@import "elements.headings";
@import "elements.hr";
@import "elements.forms";
@import "elements.links";
@import "elements.lists";
@import "elements.page";
@import "elements.quotes";
@import "elements.tables";

@import "objects.animations";
@import "objects.drawer";
@import "objects.list-bare";
@import "objects.media";
@import "objects.layout";
@import "objects.overlays";

@import "components.404";
@import "components.about";
@import "components.archive";
@import "components.avatars";
@import "components.blog-post";
@import "components.buttons";
@import "components.callout";
@import "components.clients";
@import "components.comments";
@import "components.contact";
@import "components.cta";
@import "components.faq";
@import "components.features";
@import "components.footer";
@import "components.forms";
@import "components.header";
@import "components.headings";
@import "components.hero";
@import "components.jobs";
@import "components.legal-nav";
@import "components.main-cta";
@import "components.main-nav";
@import "components.newsletter";
@import "components.page-title";
@import "components.pagination";
@import "components.post-teaser";
@import "components.process";
@import "components.quote-banner";
@import "components.offices";
@import "components.sec-nav";
@import "components.services";
@import "components.share-buttons";
@import "components.social-media";
@import "components.team";
@import "components.testimonials";
@import "components.topbar";
@import "components.reasons";
@import "components.wordpress";
@import "components.work-list";
@import "components.work-detail";

@import "vendor.prism";

@import "trumps.clearfix";
@import "trumps.utilities";

@import "healthcheck";
```
Lưu ý: Chúng ta sử dụng [các thư mục riêng biệt cho mỗi lớp](https://github.com/xfiveco/generator-chisel/tree/master/generators/app/templates/styles/itcss) và tự động tải các định dạng thêm mới bằng [Chisel](https://github.com/xfiveco/generator-chisel/)
 ##### Áp dụng tính dùng lại của đối tượng để phát triển nhanh hơn
 Các đối tượng của ITCSS là ứng cử viên hàng đầu cho việc xây dựng thư viện các thành phần dùng lại được nhằm phát triển front-end nhanh hơn. Các thành phần UI bao gồm các đối tượng chung và các thành phần đặc thù của dự án. Ví dụ, innuitcss, 1 framework dựa trên ITCSS, chứa [kha khá đối tượng](https://github.com/inuitcss/inuitcss/tree/develop/objects) nhưng lại chỉ có [1 thành mẫu duy nhất](https://github.com/inuitcss/inuitcss/tree/develop/components)
 ##### Hoạt ảnh
 Tôi khuyên bạn nên định nghĩa các hoạt ảnh chung như là các đối tượng, ví dụ như @keyframes o-fade-in trong file _objects.animations.scss
 Các thành phần đặc thù cho hoạt ảnh nên được định nghĩa trong các file thành phần tương ứng, ví dụ @keyframes c-hero-scale trong file _components.hero.scss.
 ##### Sự linh hoạt
 ITCSS rất linh hoạt trong luồng công việc cũng như các công cụ của bạn. Một trong nhưng lập trình viên của chúng tôi đã bày tỏ sự quan tâm về việc ITCSS nó đã đầy đủ như thế nào. Nhưng sự thật là điều đó hoàn toàn phụ thuộc vào bạn - ITCSS không yêu cầu bạn phải có tất cả các lớp (chỉ cái nào cần thôi)
Do vậy trong 1 cài đặt tối thiểu, bạn có thể chỉ cần 1 vài thành phần với những phần tử mẫu mặc định theo trình duyệt. Tất nhiên là điều này không thiết thực chút nào - một vài cài đặt, đặt lại và/ hay chuẩn hóa CSS được sử dụng bởi hầu hết mọi người vì những lợi ích của chúng.
 ##### Critical CSS (đoạn css tối thiểu cho những nội dung quan trọng với người dùng trong màn hình đầu tiên)
 ITCSS hỗ trợ rất tốt với critical CSS nhờ nhưng số liệu khóa của "tam giác ngược". Các thành phần dựa trên mô hình(model) cho phép bạn tách riêng từng thành phần UI thành các thành phần logic, do đó bạn thậm chí có thể chọn từng phần critical CSS của bạn thủ công (chi tiết hơn ở trong bài viết tiếp theo)
 ##### Kích thước file và lặp mẫu
 Nếu có bất kỳ mỗi mối bận tâm nào về kiến trúc như ITCSS hay đơn giản là bất kỳ thành phần nào như là kiến trúc CSS, nó có thể là kết quả của kích thước file. Các thành phần sẽ đóng gói các mẫu và cho phép chúng ta tránh các xung đột CSS và ghi đè, tuy nhiên điều này cũng đồng nghĩa với việc sự lặp lại mẫu có thể thường xuyên xảy ra.
ITCSS dường như không thể cạnh tranh được với [CSS chức năng](https://blog.colepeters.com/building-and-shipping-functional-css/). Mặt khác,, nếu bạn nhận thấy lặp quá nhiều mẫu trong các thành phần, bạn có thể cân nhắc đến việc chuyển các mẫu đó đến các đối tượng riêng biệt.
### Kết luận
Bạn sẽ không mắc sai lầm với ITCSS được. Nó là kết quả của kinh nghiệm và rất nhiều năm làm việc của Harry Roberts, một trong những tác giả CSS nổi tiếng nhất trên thế giới. Nếu bạn muốn đào sâu vào mã nguồn 1 chút, bạn sẽ thấy rằng đây là một kiến trúc đơn giản nhưng mô cùng mạnh mẽ, cho phép bạn tạo ra những dự án nhỏ lẫn to với CSS rất dễ mở rộng và bảo trì.
Tuy nhiên, đừng quên để mắt đến những cái khác như [CSS modules](https://github.com/css-modules/css-modules) trong lúc rảnh rỗi.
 
