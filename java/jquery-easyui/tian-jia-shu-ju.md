* html

```
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title></title>
		<link rel="stylesheet" type="text/css" href="themes/default/easyui.css" />
		<link rel="stylesheet" type="text/css" href="themes/icon.css" />
		<link rel="stylesheet" type="text/css" href="css/index.css" />
		<script type="text/javascript" src="js/jquery.min.js"></script>
		<script type="text/javascript" src="js/jquery.easyui.min.js"></script>
		<script type="text/javascript" src="js/customer.js"></script>
	</head>

	<body>
		<table id="dg"></table>
	</body>

</html>
```

* js

```
$(function() {
	$('#dg').datagrid({
		toolbar:[{
			iconCls:'icon-add',
			text:"添加",
			handler:function(){alert("编辑按钮")}
		}],
		url: 'datagrid_data1.json',
		method: 'get',
		columns: [
			[{
					field: 'id',
					title: '客户ID',
					width: 100
				},
				{
					field: 'name',
					title: '客户名',
					width: 100
				},
				{
					field: 'price',
					title: '价格',
					width: 100,
					align: 'right'
				}
			]
		]
	});
```



