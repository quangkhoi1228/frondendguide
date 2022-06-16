# Mapping.js

## Mapping.js là gì?

mapping.js là một thư viện đơn giản để tương tác với giao diện dựa trên dữ liệu kiểu JSON và một số thao tác khác như:

* Gán dữ liệu từ dữ liệu định dạng JSON lên giao diện
* Lấy dữ liệu từ giao diện trả về giá trị theo định dạng JSON
* Chuyển các element form HTML thành element dạng text HTML
* Xóa dữ liệu trên giao diện

## Thuật ngữ/Khái niệm

### selector

DOM query selector đầu vào của hàm `document.querySelector` hoặc `document.querySelectorAll`

```markup
#id1
.class1
.class1.class2
```

### json

dữ liệu có định dạng JSON

```css
{
    name : "Khôi",
    age: 23,
}
```

### jsonString

chuỗi chứa nội dung có định dạng JSON

```javascript
'{"name":"Khôi","age":23}'
```

### element

Phần tử HTML

```markup
<div>Tôi là phần tử HTML</div>
```

### snbKey

thuộc tính của thẻ HTML, trong mapping.js snbKey giúp quy định giá trị được áp dụng cho thẻ hoặc đăng ký thẻ là một phần tử bị ảnh hưởng bởi mapping.js

```markup
<div snb-key="key1">Tôi là phần tử HTML</div>
```

### callback

hàm sẽ được gọi sau khi thực hiện 1 số xử lý gì đó

```javascript
var callback = function(){
    console.log('Tôi là 1 hàm callback');
}
```

### options

một biến kiểu JSON quy định một số khai báo phụ của hàm

```typescript
{
    checkNull: true,
    callback: function(){
        console.log('Tôi là một callback');
    } 
}
```

### snbKeyValue

giá trị của phần tử

```javascript
12
'Giá trị'
```

### form HTML

các thẻ thuộc dạng form như input,select,textarea,...

```markup
<input type="text">
<select>
    <option>option1</option>
    <option>option2</option>
    <option>option3</option>
</select>
<textarea>some text</textarea>
```

## Gán dữ liệu lên giao diện

### Bước 1

Khởi tạo đoạn script sau trong file html

```
<script>
   document.addEventListener('DOMContentLoaded', function() {
       shinobi.demorender.build();
   });
</script>
```

### Bước 2

Khởi tạo file js tương ứng, với cấu trúc như sau

```
// Some code
shinobi.demorender = {
   build: function() {
       // functions
   },
}
```

### Bước 3

Dữ liệu đầu vào là một jsonString, tương ứng với mỗi key trong Json String là một thuộc tính snb-key trong mỗi elements

```
// Some code
<div id="container" class="container">
    <input type="text" class="input" snb-key="a">
    <input type="text" class="input" snb-key="b">
    <input type="text" class="input" snb-key="c">
</div>
```

```
// Some code
shinobi.demorender = {
   build: function() {
       // functions
       getInfo();
   },
   getInfo: function() {
       var data = {
           a: "quoc hoang",
           b: "kim hoang",
           c: "truong thinh",
       }
   },
}
```

### Bước 4

Sử dụng câu lệnh sau thuộc shinobi để mapping, “#container” là id của element cha chứa các elements con (các thuộc tính snb-key thuộc các elements con này)

```
// Some code
shinobi.mapping.render('#container', JSON.stringify(data));
```

### render/renderElement

{% tabs %}
{% tab title="code" %}
```markup
<p id="demo" snb-key="name"></p>
<p class="demo1" snb-key="age"></p>
<script>
    document.addEventListener('DOMContentLoaded', () => {
        var json = {
            name: 'Khôi',
            age: 23,
        };
        shinobi.mapping.render('#demo', JSON.stringify(json));
        var container = document.querySelector('demo1');
        shinobi.mapping.renderElement(container,json);
    });
</script>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <p id="demo" snb-key="name"></p>
    <p class="demo1" snb-key="age"></p>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            var json = {
                name: 'Khôi',
                age: 23,
            };
            shinobi.mapping.render('#demo', JSON.stringify(json));
            var container = document.querySelector('demo1');
            shinobi.mapping.renderElement(container,json);
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (8) (1).png>)
{% endtab %}
{% endtabs %}

Cả hàm `render` và hàm `renderElement` giống nhau cách sử dụng và các cấu hình, chỉ khác nhau input đầu vào của hàm.

hai hàm này đều có nhiệm vụ đưa dữ liệu dạng JSON lên giao diện cụ thể hơn các cặp key-value của `json` sẽ được đưa vào các thẻ con của phần tử `selector` hoặc `element` khai báo tại input của hàm

### snb-key

thuộc tính này dùng để xác định giá trị `value` thuộc `key` nào của `json` sẽ được gán vào giao diện, cụ thể hơn giá trị `value` của key sẽ được thêm vào nội dung thẻ hoặc thẻ được gán giá trị bằng `value` nếu thẻ là form HTML

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyName"> some default content </tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <p>Giá trị của key "name": <span snb-key="name"></span></p>
    <p>Giá trị của key "age": <span snb-key="age"></span></p>
</div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <div id="container">
        <p>Giá trị của key "name": <span snb-key="name"></span></p>
        <p>Giá trị của key "age": <span snb-key="age"></span></p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            var json = {
                name: 'Khôi',
                age: 23,
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (4).png>)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Các trường hợp gán giá trị:

* Với thẻ HTML bình thường: value sẽ gán làm innerHTML của thẻ
* Với thẻ form HTML:
  * input (dựa vào thuộc tính `type` của input)
    * checkbox: giá trị gán vào thuộc tính `checked`
    * radio: nếu `value` khớp với thuộc tính `radio-value` thì thuộc tính `checked=true` và ngược lại
    * còn lại gán vào thuộc tính `value` của thẻ
  * select: gán vào thuộc tính `value` của thẻ
  * còn lại: gán vào thuộc tính `value` của thẻ
{% endhint %}

### snb-format

thuộc tính này dùng để format giá trị dạng số, khai báo `snb-format="number"` để sử dụng

{% hint style="info" %}
Cần thêm util.js để sử dụng thuộc tính này
{% endhint %}

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyName" snb-format="number"> some default content </tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <p>Giá trị của key "name": <span snb-key="name"></span></p>
    <p>key "myMoney": <span snb-key="myMoney"></span></p>
    <p>key "myMoney": <span snb-key="myMoney" snb-format="number"></span>
    </p>
    <p>key "myMoney": <span snb-key="myMoney" snb-format="string"></span>
    </p>
</div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
    <script
        src="https://www.aladin.finance/static/js/component/util.js"></script>
</head>

<body>
    <div id="container">
        <p>Giá trị của key "name": <span snb-key="name"></span></p>
        <p>key "myMoney": <span snb-key="myMoney"></span></p>
        <p>key "myMoney": <span snb-key="myMoney" snb-format="number"></span>
        </p>
        <p>key "myMoney": <span snb-key="myMoney" snb-format="string"></span>
        </p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            var json = {
                name: 'Khôi',
                age: 23,
                myMoney: 1234567890
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (12).png>)
{% endtab %}
{% endtabs %}

### snb-render

Đôi khi ta cần xử lý giá trị trước khi đưa lên giao diện hoặc thực hiện các thao tác khác liên quan đến thẻ HTML đang quan tâm, ta sử dụng `snb-render`

`snb-render`là một hàm có 3 biến đầu vào `element`, `snbKeyValue`, và `json`

{% hint style="info" %}
Lưu ý:

* Khi có `snb-render` giá trị sẽ không tự động được gán vào phần tử
* khi có`snb-render` trong phần tử sẽ vô hiệu hóa thuộc tính `snb-format`
{% endhint %}

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
function functionName(element,snbKeyValue,json){
    ...
}
```
{% endtab %}

{% tab title="code" %}
```javascript
function dynamicColor(element, snbKeyValue, json) {
    if (snbKeyValue < 40) {
        element.style.color = 'red';
    } else {
        element.style.color = 'green';
    }
    element.innerHTML = snbKeyValue;
};
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
    <script
        src="https://www.aladin.finance/static/js/component/util.js"></script>
</head>

<body>
    <div id="container">
        <p>Giá trị của key "name": <span snb-key="name"></span></p>
        <p>key "age": <span snb-key="age" snb-render="dynamicColor"></span>
        </p>
        <p>key "myMoney": <span snb-key="myMoney" snb-render="dynamicColor"></span>
        </p>
    </div>

    <script>
        function dynamicColor(element, snbKeyValue, json) {
            if (snbKeyValue < 40) {
                element.style.color = 'red';
            } else {
                element.style.color = 'green';
            }
            element.innerHTML = snbKeyValue;
        };
        document.addEventListener('DOMContentLoaded', () => {
            var json = {
                name: 'Khôi',
                age: 23,
                myMoney: 1234567890
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (11).png>)
{% endtab %}
{% endtabs %}

### snb-editor-index

khi muốn sử dụng mapping.js để gán hoặc lấy dữ liệu của 1 editor ta thêm thuộc tính snb-editor-index cho thẻ init của editor

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyname" snb-editor-index="editorIndex"></tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="editor" snb-key="name" snb-editor-index="0"></div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
    <script defer=""
        src="https://cdn.ckeditor.com/4.14.0/full/ckeditor.js"></script>

</head>

<body>
    <div id="container">
        <p>Giá trị của key "name": <span snb-key="name"></span></p>
        <div id="editor" snb-key="name" snb-editor-index="0"></div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            CKEDITOR.replace('editor');

            var json = {
                name: 'Khôi',
                age: 23,
                myMoney: 1234567890
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (3) (1).png>)
{% endtab %}
{% endtabs %}

### multiple snbKeyValue

Đôi khi ta cần gán nhiều giá trị `value` của `json` vào các thuộc tính khác nhau lên cùng 1 thẻ mà không cần sử dụng `snb-render`, ta sử dụng `multiple snbKeyValue`

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname 
snb-key="rootKey" 
snb-key-attribute1="keyName1" 
snb-key-attribute2="keyName2" 
snb-key-innerhtml="keyName3"
> 
content 
</tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <p>key "name":
        <a snb-key="name" snb-key-title="name" snb-key-alt="age"
            snb-key-href="myPage">Nội dung không có innerHTML</a>
    </p>

    <p>
        <input type="text" snb-key="name" snb-key-name="name"
            snb-key-placeholder="myPage" style="
            width: 20rem;
        ">
    </p>

    <p>key "name":
        <a snb-key="name" snb-key-title="name" snb-key-alt="age"
            snb-key-href="myPage" snb-key-innerhtml="name">Nội dung không có
            innerHTML</a>
    </p>

    <p>
        <input type="text" snb-key="name" snb-key-name="name"
            snb-key-placeholder="myPage" snb-key-value="name" style="
            width: 20rem;
        ">
    </p>
</div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <div id="container">
        <p>key "name": <a snb-key="name" snb-key-title="name" snb-key-alt="age"
                snb-key-href="myPage">Nội dung không có innerHTML</a></p>
        <p><input type="text" snb-key="name" snb-key-name="name"
                snb-key-placeholder="myPage" style="
                width: 20rem;
            "></p>
        <p>key "name": <a snb-key="name" snb-key-title="name" snb-key-alt="age"
                snb-key-href="myPage" snb-key-innerhtml="name">Nội dung không có
                innerHTML</a></p>
        <p><input type="text" snb-key="name" snb-key-name="name"
                snb-key-placeholder="myPage" snb-key-value="name" style="
                width: 20rem;
            "></p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            var json = {
                name: 'Khôi',
                age: 23,
                myMoney: 1234567890,
                myPage: 'https://quangkhoi1228.gitbook.io/'
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (10) (1).png>)
{% endtab %}
{% endtabs %}

Ta cần khai báo thuộc tính `snb-key="keyName"` để đánh dấu sự ảnh hưởng của mapping.js lên thẻ, khai báo giá trị được gán cho thuộc tính của thẻ theo cú pháp `snb-key-attributeName="keyName"`

{% hint style="info" %}
Lưu ý:

* Luôn cần khai báo thuộc tính mồi `snb-key="keyName"`
* mapping.js không tự thêm giá trị của `snb-key`, muốn thêm giá trị html ta khai báo `snb-key-html="keyName"` và `snb-key-value="keyName"` nếu muốn thêm giá trị `value` cho các thẻ form HTML
{% endhint %}

## Lấy dữ liệu từ giao diện

### getValue/getValueElement

{% tabs %}
{% tab title="code" %}
```markup
<div id="container">
    <p> tên <input type="text" snb-key="name" value="Khôi"></p>
    <p> tuổi <input type="text" snb-key="age" value="23"></p>
    <p>giới tính </p>
    <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
            checked="true"> nam
        <input type="radio" name="gender" snb-key="gender" radio-value="MS">
        nữ
    </p>
    <p>
        <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
    </p>
</div>

<script>
    document.addEventListener('DOMContentLoaded', () => {
        shinobi.mapping.getValue('#container', function (jsonMapping) {
            console.log(jsonMapping);
        });

        var container = document.getElementById('container');
        shinobi.mapping.getValueElement(container, function (jsonMapping) {
            console.log(jsonMapping)
        })
    });

</script>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <div id="container">
        <p> tên <input type="text" snb-key="name" value="Khôi"></p>
        <p> tuổi <input type="text" snb-key="age" value="23"></p>
        <p>giới tính </p>
        <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
                checked="true"> nam
            <input type="radio" name="gender" snb-key="gender" radio-value="MS">
            nữ
        </p>
        <p>
            <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
        </p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            shinobi.mapping.getValue('#container', function (jsonMapping) {
                console.log(jsonMapping);
            });

            var container = document.getElementById('container');
            shinobi.mapping.getValueElement(container, function (jsonMapping) {
                console.log(jsonMapping)
            })
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (7).png>)
{% endtab %}
{% endtabs %}

hàm `getValue` và hàm `getValueElement` giống nhau cách sử dụng và các cấu hình, chỉ khác nhau input đầu vào của hàm.

hai hàm này đều có nhiệm vụ lấy dữ liệu dạng JSON từ giao diện cụ thể hơn các cặp key-value của `json` trả về sẽ được lấy từ các thẻ con của phần tử `selector` hoặc `element` khai báo tại input của hàm dựa vào cách khai báo tại các thẻ con.

Mặc định mapping.js chỉ lấy giá trị của các form HTML, nếu muốn lấy thêm giá trị của các thẻ HTML thường, có thể tham khảo bảng các thuộc tính `options` sau đây

| Thuộc tính | Mặc định | Diễn giải                                                                                                        |
| ---------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| getHtml    | false    | Khi bằng `true` lấy giá trị cả các phần tử HTML thường, `key`: `snb-key` của phần tử, `value`: innerHTML của thẻ |
| getText    | false    | Khi bằng `true` lấy giá trị cả các phần tử HTML thường, `key`: `snb-key` của phần tử, `value`: innerText của thẻ |
| checkEmpty | false    | Khi bằng `true` nếu thẻ form HTML lấy giá trị chưa có giá trị, phần tử sẽ bị hightlight đỏ theo các class Bulma  |

### snb-key

thuộc tính này dùng để xác định phần tử con này có thể được lấy giá trị bằng hàm `getValue` hoặc `getValueElement` , còn giá trị `key-value` được lấy ra tùy thuộc vào cách khai báo trên các phần tử con dựa vào các cấu hình của `options`

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyName"> some default content </tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<input type="text" snb-key="name" value="Khôi">
<input type="text" snb-key="age" value="23">
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <div id="container">
        <input type="text" snb-key="name" value="Khôi">
        <input type="text" snb-key="age" value="23">
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            shinobi.mapping.getValue('#container', function (jsonMapping) {
                console.log(jsonMapping);
            });

            var container = document.getElementById('container');
            shinobi.mapping.getValueElement(container, function (jsonMapping) {
                console.log(jsonMapping)
            })
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (14).png>)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
mặc định mapping.js chỉ lấy giá trị của các thẻ form HTML và editor, nếu bạn muốn lấy giá trị value của tag HTML thường thì phải cấu hình thêm trong biến `options`
{% endhint %}

### snb-editor-index

khi muốn sử dụng mapping.js để lấy dữ liệu của 1 editor ta thêm thuộc tính snb-editor-index cho thẻ init của editor

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyname" snb-editor-index="editorIndex"></tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <div id="editor" snb-key="name" snb-editor-index="0">editor content</div>
</div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
    <script defer=""
        src="https://cdn.ckeditor.com/4.14.0/full/ckeditor.js"></script>

</head>

<body>
    <div id="container">
        <div id="editor" snb-key="name" snb-editor-index="0">editor content</div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            CKEDITOR.replace('editor');

            shinobi.mapping.getValue('#container', function (jsonMapping) {
                console.log(jsonMapping);
            });

            var container = document.getElementById('container');
            shinobi.mapping.getValueElement(container, function (jsonMapping) {
                console.log(jsonMapping)
            })
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (13).png>)
{% endtab %}
{% endtabs %}

### snb-date-filter

khi muốn sử dụng thuộc tính `options` là `isEmpty: true` cho component bulma-calendar ta phải thêm thuộc tính `snb-date-filter` lên thẻ html gốc của bulma-calendar

```markup
<input class="input date-filter" snb-key="start" type="date" snb-date-filter>
```

### radio-value

Khi muốn lấy giá trị từ `input` kiểu `radio`ta cần gán giá trị của từng input bằng thuộc tính `radio-value` để xác định input hiện tại có đang `checked` hay không.

```markup
<input type="radio" name="gender" snb-key="gender" radio-value="MR">
```

### image-url

Khi muốn lấy `input` dạng `file` ta cần gán giá trị `image-url` bằng `value`

```markup
<input type="file"  snb-key="file" image-url="file.jpg">
```

### snb-preprocess

Khi muốn xử lý giá trị của thẻ trước khi gán vào `json` trả về, ta sử dụng hàm snb-preprocess

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
function functionName(snbKeyValue){
    ...
}
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <input type="text" value="20" snb-key="name" snb-preprocess="checkNull">
</div>

<script>
    function checkNull(snbKeyValue) {
        if (snbKeyValue != '') {
            snbKeyValue = snbKeyValue + ' không rỗng';
        }
        return snbKeyValue;
    }
</script>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
    <script defer=""
        src="https://cdn.ckeditor.com/4.14.0/full/ckeditor.js"></script>

</head>

<body>
    <div id="container">
        <input type="text" value="20" snb-key="name" snb-preprocess="checkNull">
    </div>

    <script>
        function checkNull(snbKeyValue) {
            if (snbKeyValue != '') {
                snbKeyValue = snbKeyValue + ' không rỗng';
            }
            return snbKeyValue;
        }
        document.addEventListener('DOMContentLoaded', () => {

            shinobi.mapping.getValue('#container', function (jsonMapping) {
                console.log(jsonMapping);
            });

            var container = document.getElementById('container');
            shinobi.mapping.getValueElement(container, function (jsonMapping) {
                console.log(jsonMapping)
            })
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (16).png>)
{% endtab %}
{% endtabs %}

### snb-datatype

Khi muốn chuẩn hóa kiểu dữ liệu của giá trị trước khi gán vào `json` trả về, ta sử dụng `snb-datatype`

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="rootKey" snb-datatype="dataType">content</tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<input type="text" value="20" snb-key="name" snb-datatype="number">
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>

</head>

<body>
    <div id="container">
        <input type="text" value="20" snb-key="nameNotConvertDataType">
        <input type="text" value="20" snb-key="name" snb-datatype="number">
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            shinobi.mapping.getValue('#container', function (jsonMapping) {
                console.log(jsonMapping);
            });

            var container = document.getElementById('container');
            shinobi.mapping.getValueElement(container, function (jsonMapping) {
                console.log(jsonMapping)
            })
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="" %}
![](<../.gitbook/assets/image (17).png>)
{% endtab %}
{% endtabs %}

## Xóa dữ liệu trên giao diện

### clear/clearElement

{% tabs %}
{% tab title="code" %}
```markup
<p>container</p>
    <div id="container">
        <p> tên <input type="text" snb-key="name" value="Khôi"></p>
        <p> tuổi <input type="text" snb-key="age" value="23"></p>
        <p>giới tính </p>
        <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
                checked="true"> nam
            <input type="radio" name="gender" snb-key="gender" radio-value="MS">
            nữ
        </p>
        <p>
            <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
        </p>
    </div>
    <p>container1</p>
    <div id="container1">
        <p> tên <input type="text" snb-key="name" value="Khôi"></p>
        <p> tuổi <input type="text" snb-key="age" value="23"></p>
        <p>giới tính </p>
        <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
                checked="true"> nam
            <input type="radio" name="gender" snb-key="gender" radio-value="MS">
            nữ
        </p>
        <p>
            <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
        </p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            shinobi.mapping.clear('#container');

            var container = document.getElementById('container1');
            shinobi.mapping.clearElement(container)
        });

    </script>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <p>container</p>
    <div id="container">
        <p> tên <input type="text" snb-key="name" value="Khôi"></p>
        <p> tuổi <input type="text" snb-key="age" value="23"></p>
        <p>giới tính </p>
        <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
                checked="true"> nam
            <input type="radio" name="gender" snb-key="gender" radio-value="MS">
            nữ
        </p>
        <p>
            <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
        </p>
    </div>
    <p>container1</p>
    <div id="container1">
        <p> tên <input type="text" snb-key="name" value="Khôi"></p>
        <p> tuổi <input type="text" snb-key="age" value="23"></p>
        <p>giới tính </p>
        <p><input type="radio" name="gender" snb-key="gender" radio-value="MR"
                checked="true"> nam
            <input type="radio" name="gender" snb-key="gender" radio-value="MS">
            nữ
        </p>
        <p>
            <input type="checkbox" snb-key="isHandsome" checked="true"> đẹp trai
        </p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            shinobi.mapping.clear('#container');

            var container = document.getElementById('container1');
            shinobi.mapping.clearElement(container)
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (8) (1).png>)
{% endtab %}
{% endtabs %}

hàm `render` và hàm `renderElement` giống nhau cách sử dụng và các cấu hình, chỉ khác nhau input đầu vào của hàm.

hai hàm này đều có nhiệm vụ đưa dữ liệu dạng JSON lên giao diện cụ thể hơn các cặp key-value của `json` sẽ được đưa vào các thẻ con của phần tử `selector` hoặc `element` khai báo tại input của hàm

### snb-key

thuộc tính này dùng để xác định giá trị `value` thuộc `key` nào của `json` sẽ được gán vào giao diện, cụ thể hơn giá trị `value` của key sẽ được thêm vào nội dung thẻ hoặc thẻ được gán giá trị bằng `value` nếu thẻ là form HTML

{% tabs %}
{% tab title="Cú pháp" %}
```markup
<tagname snb-key="keyName"> some default content </tagname>
```
{% endtab %}

{% tab title="code" %}
```markup
<div id="container">
    <p>Giá trị của key "name": <span snb-key="name"></span></p>
    <p>Giá trị của key "age": <span snb-key="age"></span></p>
</div>
```
{% endtab %}

{% tab title="ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <script>
        shinobi = {};
    </script>
    <script
        src="https://www.aladin.finance/static/js/component/mapping.js"></script>
</head>

<body>
    <div id="container">
        <p>Giá trị của key "name": <span snb-key="name"></span></p>
        <p>Giá trị của key "age": <span snb-key="age"></span></p>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            var json = {
                name: 'Khôi',
                age: 23,
            };
            shinobi.mapping.render('#container', JSON.stringify(json));
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="kết quả" %}
![](<../.gitbook/assets/image (4).png>)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Các trường hợp gán giá trị:

* Với thẻ HTML bình thường: value sẽ gán làm innerHTML của thẻ
* Với thẻ form HTML:
  * input (dựa vào thuộc tính `type` của input)
    * checkbox: giá trị gán vào thuộc tính `checked`
    * radio: nếu `value` khớp với thuộc tính `radio-value` thì thuộc tính `checked=true` và ngược lại
    * còn lại gán vào thuộc tính `value` của thẻ
  * select: gán vào thuộc tính `value` của thẻ
  * còn lại: gán vào thuộc tính `value` của thẻ
{% endhint %}

### snb-format

## Các hàm hỗ trợ

### render (selector, jsonString)

Đưa dữ liệu lên giao diện

```
shinobi.mapping.render(selector,jsonString)
```

### renderElement(element,json)

Đưa dữ liệu lên giao diện

```javascript
shinobi.mapping.renderElement(element,json)
```

### renderSelector(element,json,snbKey)

Đưa dữ liệu vài phần tử

```javascript
shinobi.mapping.renderSelector(element,json,snbKey)
```

### getValue(selector,callback,options)

Lấy dữ liệu có thể có trong tập con của phần tử và trả về dữ liệu dạng JSON

```julia
shinobi.mapping.getValue(selector,callback,options)
```

### getValueElement(element,callback,options)

Lấy dữ liệu có thể có trong tập con của phần tử và trả về dữ liệu dạng JSON

```julia
shinobi.mapping.getValueElement(element,callback,options)
```

### handleOptionMapping(element,snbKeyValue,options)

áp dụng các thay đổi lên phần tử dựa theo các `options` được khai báo

```javascript
shinobi.mapping.handleOptionMapping(element,snbKeyValue,options)
```

### getValueMappingNormalTag(element,options)

lấy giá trị của element HTML

```javascript
shinobi.mapping.getValueMappingNormalTag(element,options)
```

### replaceFormWithLabel(selector)

đổi các phần tử con của phần tử `selector` từ form HTML thành dạng text HTML

```javascript
shinobi.mapping.replaceFormWithLabel(selector)
```

### replaceFormWithLabelElement(element)

đổi các phần tử con của phần tử `element` từ form HTML thành dạng text HTML

```javascript
shinobi.mapping.replaceFormWithLabelElement(element)
```

### replaceFormWithLabelSnbKey(element)

đổi phần tử form HTML thành dạng text HTML

```javascript
shinobi.mapping.replaceFormWithLabelSnbKey(element)
```

### checkPreProcess(element,options)

biến đổi dữ liệu trả về tùy vào các thuộc tính `options`

```javascript
shinobi.mapping.checkPreProcess(element,options)
```

### getValueShinobiEditor(element,options)

lấy dữ liệu từ phần tử dạng editor dựa vào các thuộc tính `options`

```javascript
shinobi.mapping.getValueShinobiEditor(element,options)
```

### clear(selector,callback,options)

xóa dữ liệu các phần tử có chứa snbKey dựa vào các cấu hình `options`

```javascript
shinobi.mapping.clear(selector,callback,options)
```

### clearElement(element,callback,options)

xóa dữ liệu các phần tử có chứa snbKey dựa vào các cấu hình `options`

```javascript
shinobi.mapping.clearElement(element,callback,options)
```
