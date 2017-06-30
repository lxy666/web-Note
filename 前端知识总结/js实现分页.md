>大家在展示数据的时候难免会用到表格，而分页的存在会使表格看起来更简洁。

```html
<table class="table table-hover">
        <thead>
        <tr>
            <th>日期</th>
            <th>小时</th>
            <th>温度</th>
        </tr>
    </table>
    <table class="table table-hover table-striped" id="table_result">
        <tbody id="table_body_result">
        <tr>
            <td>2017-01-10</td>
            <td>20</td>
            <td>20</td>
        </tr>
        <tr>
            <td>2017-01-10</td>
            <td>20</td>
            <td>20</td>
        </tr>
        <tr>
            <td>2017-01-10</td>
            <td>20</td>
            <td>20</td>
        </tr>
       <!--中间省略多行数据-->
        </tbody>
    </table>
    <div id="barcon" name="barcon"></div>//空的div用来放分页后的表格
```
>下面是js分页的代码

```javascript
    goPage(1,15);
    function goPage(pno, psize) {
        var itable = document.getElementById("table_result");//通过ID找到表格
        var num = itable.rows.length;//表格所有行数(所有记录数)
        var totalPage = 0;//总页数
        var pageSize = psize;//每页显示行数
        //总共分几页
        if (num / pageSize > parseInt(num / pageSize)) {
            totalPage = parseInt(num / pageSize) + 1;
        } else {
            totalPage = parseInt(num / pageSize);
        }
        var currentPage = pno;//当前页数
        var startRow = (currentPage - 1) * pageSize + 1;//开始显示的行  1
        var endRow = currentPage * pageSize;//结束显示的行   15
        endRow = (endRow > num) ? num : endRow;
        //遍历显示数据实现分页
        for (var i = 1; i < (num + 1); i++) {
            var irow = itable.rows[i - 1];
            if (i >= startRow && i <= endRow) {
                irow.style.display = "block";
            } else {
                irow.style.display = "none";
            }
        }
        var tempStr = "";
        if (currentPage > 1) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage - 1) + "," + psize + ")\"><上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>"
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        } else {
            tempStr += "<上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        }
        if (currentPage < totalPage) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage + 1) + "," + psize + ")\">下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>";
            for (var j = 1; j <= totalPage; j++) {
            }
        } else {
            tempStr += "  下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
            }
        }
        document.getElementById("barcon").innerHTML = tempStr;
    }
```

![效果图 其一](http://upload-images.jianshu.io/upload_images/3229842-1f2765075fae79f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![效果图  其二](http://upload-images.jianshu.io/upload_images/3229842-b35fea151195dcc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>下面对代码进行解读
```javascript
    goPage(1,15);//指的是当前页为第一页，15条数据为一页
```
然后计算出一共分为几页
```javascript
        var totalPage = 0;//总页数
        var pageSize = psize;//每页显示行数
        if (num / pageSize > parseInt(num / pageSize)) {//假设有20条数据，15条数据页 
            totalPage = parseInt(num / pageSize) + 1;//1.333>1 ,所以分为两页
        } else {
            totalPage = parseInt(num / pageSize);//若有45条数据，则分为3页
        }
```
计算开始显示的行数，和最后显示的行数
```javascript
        var currentPage = pno;//当前页数
        var startRow = (currentPage - 1) * pageSize + 1;//开始显示的行  1
        var endRow = currentPage * pageSize;//结束显示的行   15
        endRow = (endRow > num) ? num : endRow;
```
遍历显示数据实现分页
```javascript
 for (var i = 1; i < (num + 1); i++) {
            var irow = itable.rows[i - 1];
            if (i >= startRow && i <= endRow) {
                irow.style.display = "block";//当前页的数据
            } else {
                irow.style.display = "none";//非当前页的数据
            }
        }
```
实现最下方的显示，第几页，上一页，下一页
当前页为第一页时，上一页没有点击事件
当前页为最后一页时，下一页没有点击事件
否则，上一页和下一页均可使用，点击某一页会跳转到那一页
```javascript
 if (currentPage > 1) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage - 1) + "," + psize + ")\"><上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>"
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        } else {
            tempStr += "<上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        }
        if (currentPage < totalPage) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage + 1) + "," + psize + ")\">下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>";
            for (var j = 1; j <= totalPage; j++) {
            }
        } else {
            tempStr += "  下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
            }
        }
```
![屏幕快照 2017-05-09 15.48.00.png](http://upload-images.jianshu.io/upload_images/3229842-e502c860410283b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到此，分页效果已经实现了。

