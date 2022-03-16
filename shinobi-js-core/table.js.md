# Table.js

## Table.js là gì?

table.js là một thư viện dùng để hiển thị dữ liệu dạng list JSON hoặc [dữ liệu dạng findDataList](https://quangkhoi1228.gitbook.io/guide/shinobi-js-core/gioi-thieu-shinobi-js-core#du-lieu-dang-finddatalist) lên giao diện, các dữ liệu này thể hiện trên giao diện theo dạng 1 table\`

![](<../.gitbook/assets/image (40).png>)

## Cách dùng

### Cách khai báo HTML chung

các hàm JS gọi ra để thực thi đều có chung khai báo HTML&#x20;

#### Bước 1: Thêm JS, CSS vào trang&#x20;

{% tabs %}
{% tab title="JS" %}
```markup
<script src="https://naruto.finance/static/js/component/exportfile.js"></script>
<script src="https://naruto.finance/static/js/component/mapping.js"></script>
<script src="https://naruto.finance/static/js/component/api.js"></script>
<script src="https://naruto.finance/static/js/component/util.js"></script>
<script src="https://naruto.finance/static/js/library/all.min.js"></script>
<script src="https://naruto.finance/static/js/component/table.js"></script>
```
{% endtab %}

{% tab title="CSS" %}
```markup
<style>
    @keyframes spinAround {
        from {
            transform: rotate(0deg);
        }

        to {
            transform: rotate(359deg);
        }
    }

    @keyframes spinAround {
        from {
            transform: rotate(0deg);
        }

        to {
            transform: rotate(359deg);
        }
    }

    .table-pagination {
        margin-top: 0.75rem;
        margin-bottom: 0.75rem;
        padding: 0.75rem;
        display: flex;
        justify-content: flex-end;
    }

    .table-pagination .select-record-per-page-container,
    .table-pagination .select-page-container {
        display: flex;
        padding: 0;
        margin-left: 2rem;
    }

    .table-pagination .select-page-container {
        display: flex;
        padding: 0;
        margin-left: 2rem;
    }

    .table-pagination .table-pagination-row-total,
    .table-pagination .table-pagination-page-total,
    .table-pagination .shinobi-pagination-curpage,
    .table-pagination .shinobi-recordperpage {
        font-weight: 700;
    }

    .table-pagination .table-pagination-row-total,
    .table-pagination .table-pagination-page-total,
    .table-pagination .shinobi-pagination-curpage {
        line-height: 1.75;
    }

    .table-pagination .table-pagination-label {
        margin-left: 0.5rem;
        margin-right: 0.5rem;
        line-height: 1.75;
    }

    .table-pagination .table-pagination-label:last-child {
        margin-right: 0;
    }

    .table-pagination .table-pagination-label:first-child {
        margin-left: 0;
    }

    .table-pagination .shinobi-pagination-prev,
    .table-pagination .shinobi-pagination-next {
        min-width: 2rem;
    }

    .table-pagination .shinobi-pagination-curpage {
        width: 3rem;
        text-align: center;
    }

    .table-pagination .field {
        margin-bottom: 0;
    }

    .table-pagination .label-mobile {
        display: block;
    }

    .table-pagination .label-mobile {
        display: none;
    }

    @media screen and (max-width: 768px) {
        .table-pagination .label-desktop {
            display: none;
        }

        .table-pagination .label-mobile {
            display: block;
        }
    }

    .table-pagination-small .table-pagination .select-record-per-page-container {
        display: none;
    }
</style>
```
{% endtab %}
{% endtabs %}

#### Bước 2: Thêm HTML

{% tabs %}
{% tab title="Cú pháp" %}
```markup
 <table id="tableId" >
     <thead>
         <tr>
             <th>...</th>
             <th>...</th>
             ...
             <th>...</th>
         </tr>
     </thead>
     <tbody></tbody>
</table>
#{{paginationHTML}}
```
{% endtab %}

{% tab title="Ví dụ" %}
```markup
 <table id="table1" class="table is-fullwidth">
    <thead>
        <tr>
            <th snb-colname="id">Id</th>
            <th snb-colname="name">name</th>
            <th snb-colname="age">age</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>
#{{paginationHTML}}
```
{% endtab %}

{% tab title="paginationHTML" %}
```markup
<div class="table-pagination">
    <div class="columns is-mobile">
        <div class="column select-record-per-page-container">
            <span class="table-pagination-label"> Hiện</span>
            <div class="select is-primary is-small">
                <select class="shinobi-recordperpage"
                    snb-key="recordPerPage">
                    <option value="5">5</option>
                    <option value="10">10</option>
                    <option value="15">15</option>
                </select>
            </div>
            <span class="table-pagination-label"><span
                    class="label-desktop">trong số</span><span
                    class="label-mobile">/</span></span>
            <span class="table-pagination-row-total"
                snb-key="rowTotal">30</span>
        </div>
        <div class="column select-page-container">
            <span class="table-pagination-label">Trang</span>
            <div class="field has-addons">
                <p class="control">
                    <a
                        class="button is-primary is-small shinobi-pagination-prev"><span
                            class="icon"><i
                                class="fa fa-chevron-left"></i></span>
                    </a>
                </p>
                <p class="control">
                    <input
                        class="input is-primary is-small shinobi-pagination-curpage"
                        snb-key="currentpage" value="1" />
                </p>
                <p class="control">
                    <a
                        class="button is-primary is-small shinobi-pagination-next">
                        <span class="icon"><i
                                class="fa fa-chevron-right"></i></span>
                    </a>
                </p>
            </div>
            <span class="table-pagination-label"><span
                    class="label-desktop">trong</span><span
                    class="label-mobile">/</span></span>
            <span class="table-pagination-page-total"
                snb-key="pageTotal" snb-format="true">1</span>
        </div>
    </div>
</div>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Diễn giải:

datalist HTML bao gồm 3 thành phần:

1. table HTML khai báo:
   1. `id`: id của tableObject
   2. &#x20;thẻ thead bao gồm các thẻ th khai báo các thuộc tính của table
2. Container chứa đoạn HTML **nằm kế dưới table** trong file HTML chứa nội dung phân trang, nội dung được để trong  tab **paginationHTML**

**\*Khi thực thi JS table.js các thẻ `tr` con sẽ được loop dựa theo số lượng dữ liệu và nằm trong `tbody` **&#x20;
{% endhint %}

### Các thuộc tính của thẻ th header

#### snb-colname&#x20;

thể hiện key nào trong JSON sẽ được đưa vào cột này

```markup
<th snb-colname="name">Name</th>
```

{% hint style="info" %}
Nếu cột này không cần render dữ liệu từ JSON thì khai báo

```markup
<th snb-colname="">Không có data</th>
```
{% endhint %}

#### snb-header-control

khi muốn thao tác trực tiếp trên giao diện như sort, filter lại dữ liệu ta sử dụng thuộc tính này

```markup
<!-- sort only -->
<th snb-colname="name" snb-header-control="1">Name</th>
<!-- sort and filter -->
<th snb-colname="name" snb-header-control="1,2">Name</th>
```

#### snb-render

khi muốn custom dữ liệu của 1 cột ta sử dụng `snb-render` trên `header` cột đó

{% tabs %}
{% tab title="Cú pháp " %}
```javascript
function renderFunction(cellIsHandling, rowIndex, colIndex, allData)
```
{% endtab %}

{% tab title="Ví dụ" %}
```markup
<script>
    function customRender(cell,row,col,all){
        var value = cell.innerHTML;
        cell.innerHTML = value + 'Đã custom';
    }
</script>

<th snb-colname="name" snb-render="customRender">Name</th>
```
{% endtab %}
{% endtabs %}

#### snb-filter-preprocess

khi muốn custom giá trị của input `filter` trước khi đưa vào `request` để gọi data, sử dụng `snb-filter-preprocess`

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
function preProcessFunction(filterInput){
    ...
    return filterInputCustom;
}
```
{% endtab %}

{% tab title="Ví dụ" %}
```markup
<script>
    function customFilterInput(input){
        return input + 'Đã custom';
    }
</script>

<th snb-colname="name" snb-header-control="1,2" 
snb-preprocess="customFilterInput">Name</th>
```
{% endtab %}
{% endtabs %}

### Khởi tạo đối tượng datalist

&#x20;Để sử dụng các chức năng của datalist.js ta cần phải khởi tạo đối tượng shinobi.datalist bằng cú pháp:

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
var datalistObject = new shinobi.datalist(datalistId)
```
{% endtab %}

{% tab title="Ví dụ" %}
```javascript
var datalistObject = new shinobi.datalist('datalistId');
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Phải có HTML chung rồi với khởi tạo được hàm shinobi.datalist
{% endhint %}



### Render danh sách JSON lên giao diện

&#x20;Để render danh sách JSON lên giao diện ta sử dụng hàm  `renderTable`

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
var dataJsonList = [{...},{...},...,{...}];
var tableObject = new shinobi.table(tableId);

tableObject.renderTable(colnames, dataJsonList, renders)
```
{% endtab %}

{% tab title="Code" %}
```javascript
 var dataJsonList = [
    {
        id: 1,
        name: 'Khôi',
        age: 2,
    },
    {
        id: 2,
        name: 'Khôi_1',
        age: 22,
    },
    {
        id: 3,
        name: 'Khôi_3',
        age: 222,
    },
];
var colnames = shinobi.tableHelper.getColname('table1');
var renders = [];
var tableObject = new shinobi.table('table1');
tableObject.renderTable(colnames, dataJsonList, renders);
```
{% endtab %}

{% tab title="Ví dụ" %}
```markup
<!DOCTYPE html>
<html>

<head>
    <link rel="stylesheet"
        href="https://cdn.jsdelivr.net/npm/bulma@0.9.2/css/bulma.min.css">
    <link rel="stylesheet"
        href="https://naruto.finance/static/css/component/shinobicomponent.css">
    <script>
        shinobi = {};
    </script>
    <script
        src="https://naruto.finance/static/js/component/language.js"></script>
    <script
        src="https://naruto.finance/static/js/component/exportfile.js"></script>
    <script
        src="https://naruto.finance/static/js/component/mapping.js"></script>
    <script src="https://naruto.finance/static/js/component/api.js"></script>
    <script src="https://naruto.finance/static/js/component/util.js"></script>
    <script src="https://naruto.finance/static/js/library/all.min.js"></script>
    <script src="https://naruto.finance/static/js/component/table.js"></script>
    <script
        src="https://naruto.finance/static/js/component/initbulma.js"></script>
    <script
        src="https://naruto.finance/static/js/component/notification.js"></script>
    <style>
        @keyframes spinAround {
            from {
                transform: rotate(0deg);
            }

            to {
                transform: rotate(359deg);
            }
        }

        @keyframes spinAround {
            from {
                transform: rotate(0deg);
            }

            to {
                transform: rotate(359deg);
            }
        }

        .table-pagination {
            margin-top: 0.75rem;
            margin-bottom: 0.75rem;
            padding: 0.75rem;
            display: flex;
            justify-content: flex-end;
        }

        .table-pagination .select-record-per-page-container,
        .table-pagination .select-page-container {
            display: flex;
            padding: 0;
            margin-left: 2rem;
        }

        .table-pagination .select-page-container {
            display: flex;
            padding: 0;
            margin-left: 2rem;
        }

        .table-pagination .table-pagination-row-total,
        .table-pagination .table-pagination-page-total,
        .table-pagination .shinobi-pagination-curpage,
        .table-pagination .shinobi-recordperpage {
            font-weight: 700;
        }

        .table-pagination .table-pagination-row-total,
        .table-pagination .table-pagination-page-total,
        .table-pagination .shinobi-pagination-curpage {
            line-height: 1.75;
        }

        .table-pagination .table-pagination-label {
            margin-left: 0.5rem;
            margin-right: 0.5rem;
            line-height: 1.75;
        }

        .table-pagination .table-pagination-label:last-child {
            margin-right: 0;
        }

        .table-pagination .table-pagination-label:first-child {
            margin-left: 0;
        }

        .table-pagination .shinobi-pagination-prev,
        .table-pagination .shinobi-pagination-next {
            min-width: 2rem;
        }

        .table-pagination .shinobi-pagination-curpage {
            width: 3rem;
            text-align: center;
        }

        .table-pagination .field {
            margin-bottom: 0;
        }

        .table-pagination .label-mobile {
            display: block;
        }

        .table-pagination .label-mobile {
            display: none;
        }

        @media screen and (max-width: 768px) {
            .table-pagination .label-desktop {
                display: none;
            }

            .table-pagination .label-mobile {
                display: block;
            }
        }

        .table-pagination-small .table-pagination .select-record-per-page-container {
            display: none;
        }
    </style>
</head>

<body>

    <div class="hero">
        <div class="hero-body">
            <table id="table1" class="table is-fullwidth">
                <thead>
                    <tr>
                        <th snb-colname="id">Id</th>
                        <th snb-colname="name">name</th>
                        <th snb-colname="age">age</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
            <div class="table-pagination">
                <div class="columns is-mobile">
                    <div class="column select-record-per-page-container">
                        <span class="table-pagination-label"> Hiện</span>
                        <div class="select is-primary is-small">
                            <select class="shinobi-recordperpage"
                                snb-key="recordPerPage">
                                <option value="5">5</option>
                                <option value="10">10</option>
                                <option value="15">15</option>
                            </select>
                        </div>
                        <span class="table-pagination-label"><span
                                class="label-desktop">trong số</span><span
                                class="label-mobile">/</span></span>
                        <span class="table-pagination-row-total"
                            snb-key="rowTotal">30</span>
                    </div>
                    <div class="column select-page-container">
                        <span class="table-pagination-label">Trang</span>
                        <div class="field has-addons">
                            <p class="control">
                                <a
                                    class="button is-primary is-small shinobi-pagination-prev"><span
                                        class="icon"><i
                                            class="fa fa-chevron-left"></i></span>
                                </a>
                            </p>
                            <p class="control">
                                <input
                                    class="input is-primary is-small shinobi-pagination-curpage"
                                    snb-key="currentpage" value="1" />
                            </p>
                            <p class="control">
                                <a
                                    class="button is-primary is-small shinobi-pagination-next">
                                    <span class="icon"><i
                                            class="fa fa-chevron-right"></i></span>
                                </a>
                            </p>
                        </div>
                        <span class="table-pagination-label"><span
                                class="label-desktop">trong</span><span
                                class="label-mobile">/</span></span>
                        <span class="table-pagination-page-total"
                            snb-key="pageTotal" snb-format="true">1</span>
                    </div>
                </div>
            </div>
        </div>

    </div>
    <div id="confirmPanel" class="modal is-small">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
                <p class="modal-card-title" snb-lang="PAGECODE_WARNING">Cảnh báo
                </p>
                <button class="delete" aria-label="close"></button>
            </header>
            <section class="modal-card-body" snb-lang="PAGECODE_ARE_YOU_SURE">
                Bạn
                chắc chắn?</section>
            <footer class="modal-card-foot">
                <button class="button is-success yes"
                    snb-lang="PAGECODE_CONFIRM">Xác
                    nhận</button>
                <button class="button cancel"
                    snb-lang="PAGECODE_CANCEL">Hủy</button>
            </footer>
        </div>
    </div>

    <div id="shinobinotification" class="notification  shinobinotification">
        <button class="delete"></button>
        <div class="notificationcontent" snb-lang="PAGECODE_UPDATE_SUCCESS">
            Update
            success</div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            var dataJsonList = [
                {
                    id: 1,
                    name: 'Khôi',
                    age: 2,
                },
                {
                    id: 2,
                    name: 'Khôi_1',
                    age: 22,
                },
                {
                    id: 3,
                    name: 'Khôi_3',
                    age: 222,
                },
            ];
            var colnames = shinobi.tableHelper.getColname('table1');
            var renders = [];
            var tableObject = new shinobi.table('table1');
            tableObject.renderTable(colnames, dataJsonList, renders);
        });

    </script>
</body>

</html>
```
{% endtab %}

{% tab title="Kết quả" %}
![](<../.gitbook/assets/image (41).png>)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Lưu ý: pagination chưa có chức năng khi sử dụng `renderTable` nên ta có thể thêm class `is-hidden` vào pagination container để ẩn đi pagination
{% endhint %}

#### callback

là hàm được gọi sau khi dữ liệu được render xong lên giao diện

```javascript
function(){
    ...
}
```

#### options

| Thuộc tính              | Mặc định | Diễn giải                                                                    |
| ----------------------- | -------- | ---------------------------------------------------------------------------- |
| lazyload                | false    | Khi bằng `true` dữ liệu được chia ra nhiều lần để đưa lên giao diện          |
| lazyloadSplitDataLength | 20       | số lượng phần tử được đưa vào mỗi lần lazy load lên giao diện                |
| lazySplitDataInterval   | 20       | thời gian giữa 2 lần lazy load lên giao diện                                 |
| insertType              | end      | khi bằng `start` dữ liệu sẽ được insert vào đầu của danh sách trên giao diện |

### Render dựa theo API findDataList

ngoài chức năng render 1 list JSON lên giao diện datalist.js còn có thể phối hợp với shinobi server để có thể tạo ra giao diện động có chức năng phân trang đi kèm.

#### initLoadApi

{% tabs %}
{% tab title="Cú pháp" %}
```javascript
datalistObject.initLoadApi(url,request,callback)
```
{% endtab %}

{% tab title="Code" %}
```javascript
var request = {};
request.recordPerPage = 3;
request.pageNum = 1;

request.filters = [
    {'colname':'username','operator':': ','value':'831'}
];

request.sorts = [
    {"colname":"createddate","value":"desc"}
]

datalist1.initLoadApi("/api/coretest/findDataList", request);
```
{% endtab %}
{% endtabs %}

Diễn giải:

* `url`: api lấy dữ liệu có dạng findDataList
* `request`: JSON cấu hình các thông số của `datalistObject` có các thuộc tính sau:
  * `recordPerPage`: số dòng mỗi trang
  * `pageNum`: số trang hiện tại
  * `filters`: danh sách các [filter object](https://quangkhoi1228.gitbook.io/guide/shinobi-js-core/gioi-thieu-shinobi-js-core#filter-object)
  * `sorts`: danh sách các [sort object](https://quangkhoi1228.gitbook.io/guide/shinobi-js-core/gioi-thieu-shinobi-js-core#sort-object)
* `callback`: hàm chạy sau khi render xong dữ liệu&#x20;

### Load dữ liệu 1 trang cụ thể

Sau khi khởi tạo đối tượng thông qua hàm `initLoadApi` ta có thể sử dụng hàm `reloadApi` để load dữ liệu 1 trang cụ thể lên giao diện

```javascript
//load data 1 trang cụ thể 
datalistObject.reloadApi(pageNum)

//chạy hàm sau khi load data xong
datalistObject.reloadApi(pageNum,callback)

//load lại data trang hiện tại
datalistObject.reloadApi()
```

### Xóa dữ liệu của datalist

Ta có thể xóa dữ liệu đang render trên giao diện bằng hàm `clear`

```javascript
datalistObject.clear()
```

## Các thuộc tính và hàm hỗ trợ

| Diễn giải          |                                                                     |
| ------------------ | ------------------------------------------------------------------- |
| loadingContainer   | container chứa loading khi call dữ liệu                             |
| url                | API gọi dữ liệu                                                     |
| filters            | Mảng các filter object đang áp dụng cho datalist                    |
| staticfilters      | Mảng các filter object được khai báo không thông qua datalistObject |
| sorts              | Mảng các sort object đang áp dụng cho datalist                      |
| staticsorts        | Mảng các sort object được khai báo không thông qua datalistObject   |
| paramsList         | 1 custom key sẽ được thêm vào request khi gọi data API              |
| tableRows          | List JSON object data hiện tại của datalistObject                   |
| pageNum            | Số trang đang hiển thị                                              |
| recordPerPage      | Số phần tử mỗi trang                                                |
| pageTotal          | Tổng số trang tối đa                                                |
| rowTotal           | Tổng số dòng dữ liệu tối đa                                         |
| tableNode          | snb-datalist-node container element                                 |
| tableContainerNode | Container cha của tableNode                                         |
| sampleNode         | Phần tử con mẫu                                                     |

