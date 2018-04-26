
## 安装 Bootstrap Table 环境

#### 安装样式

```html
<link href='assets/bootstrap/3.3.7/css/bootstrap.min.css' rel='stylesheet'>

<link href='assets/bootstrap-table/1.12.1/bootstrap-table.min.css' rel='stylesheet'>
```

#### 安装脚本

```html
<script src='assets/jquery-1.12.4.min.js'></script>

<script src='assets/bootstrap/3.3.7/js/bootstrap.min.js'></script>

<script src='assets/bootstrap-table/1.12.1/bootstrap-table.min.js'></script>

<script src='assets/bootstrap-table/1.12.1/locale/bootstrap-table-zh-CN.min.js'></script>
```

## 基本用法

#### 静态表格

```html
<table data-toggle="table">
	<thead>
		<tr>
			<th>Item ID</th>
			<th>Item Name</th>
			<th>Item Price</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>1</td>
			<td>Item 1</td>
			<td>$1</td>
		</tr>
		<tr>
			<td>2</td>
			<td>Item 2</td>
			<td>$2</td>
		</tr>
	</tbody>
</table>
```

#### 动态表格（用 data-url 加载指定URL的数据）

```html
<table data-toggle="table" data-url="data1.json">
	<thead>
		<tr>
			<th data-field="id">Item ID</th>
			<th data-field="name">Item Name</th>
			<th data-field="price">Item Price</th>
		</tr>
	</thead>
</table>
```

data1.json 内容格式：

```
[
{"id":"1", "name":"Item 1", "price":"$1"},
{"id":"2", "name":"Item 2", "price":"$2"}
]
```

#### 动态表格（用 JavaScript 加载表结构和数据）

```html
<table id="table"></table>

<script>
		$('#table').bootstrapTable({
			columns : [ {
				field : 'id',
				title : 'Item ID'
			}, {
				field : 'name',
				title : 'Item Name'
			}, {
				field : 'price',
				title : 'Item Price'
			} ],
			data : [ {
				id : 1,
				name : 'Item 1',
				price : '$1'
			}, {
				id : 2,
				name : 'Item 2',
				price : '$2'
			} ]
		});
	</script>
```

