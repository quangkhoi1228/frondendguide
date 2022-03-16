# Fragment

Trong một hệ thống giao diện web ( giao diện aladin) , các khối html  giống  nhau có thể  lặp đi lặp lại nhiều lần, để tránh việc lặp đi lặp lại nhiều lần, fragment sẽ chứa một khối html sử dụng chung cho các  trang web sử dụng khối html trong fragment, khi này các trang cần khối html trong fragment, chỉ cần thêm fragment vào các trang mà không cần code lại.&#x20;

Fragment trong html là một khối html được sử dụng  cho nhiều trang web khác nhau mà có cùng  1 cách hiển thị. Nói cách để tránh việc lặp lại nhiều lần của một đoạn html  người  ta sử dụng fragment.

Trong hệ thống của aladin, toàn bộ các  fragment sẽ được lưu trong folder tên  "fragment"

(link: /aladin/web/aladin/fragment );

![](../.gitbook/assets/screenshot-from-2021-04-26-21-11-03.png)

### Cách sử dụng

#### \* Lưu ý:&#x20;

* Khi tạo các fragment mới, các bạn phải bỏ vào thư mục tên fragment có sẵn trên aladin, mục đích nhằm dễ quản lí code và thống nhất cấu trúc  trong aladin .
* &#x20;**** Không thể thao tác bằng JS để thêm fragment vào trang web bất kì,  chỉ có thể import trực tiếp vào file html, Vì : Trình tự hành vi khi client lấy dữ liệu tới một trang : client gọi một DNS => Server  tiếp nhập  => server  thêm các khối html trong các fragment vào trang client gọi tới => trả về phía client >client nhận dữ liệu, chạy JS có trong file trả về. Vì JS chạy sau cùng trên client, nên không thể thêm fragment vào file html.

{% tabs %}
{% tab title="Tổng quát" %}
```
#{{@Đường_dẫn_đến_fragment}}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Cách thêm fragment trên web  Aladin" %}
```
#{{/fragment/@Tên_fragment_cần_cho_trang}}
```
{% endtab %}
{% endtabs %}

### &#x20;Ví dụ:&#x20;

Trong hệ Aladin có các fragment không thể thiếu như : header, footer

* file  header:&#x20;

![](../.gitbook/assets/screenshot-from-2021-04-26-21-42-01.png)

* file footer  :

![](../.gitbook/assets/screenshot-from-2021-04-26-21-43-47.png)

Khi ta import 2 file header.html và footer.html vào trong 1 trang web như sau:

* file html:

![](../.gitbook/assets/screenshot-from-2021-04-26-21-47-00.png)

* Hiển  thị trên giao diện:

![](../.gitbook/assets/screenshot-from-2021-04-26-21-52-03.png)

* Còn đây là code phía client hiểu được

![](../.gitbook/assets/screenshot-from-2021-04-26-21-55-25.png)

&#x20;

Ví dụ:&#x20;



