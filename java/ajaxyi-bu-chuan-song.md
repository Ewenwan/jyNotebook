```
	$.ajax({
		type: "get",
		url: "datagrid_data1.json",
		async: true,
		datatype: 'json',
		success: function(datas) {
//			console.log(datas["rows"][0].id)
			var rows = []
			var data = datas["rows"]
			for(var i = 0; i < data.length; i++) {
				rows.push({
					id: data[i].id,
					name: data[i].name,
					price: data[i].price
				})
				console.log(data[i])
			}
			
			$('#dg').datagrid({
		//		url: 'datagrid_data1.json',
//		method: 'get',
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
			
//			 更新页脚行并载入新数据
			$('#dg').datagrid({ data: rows }).datagrid('clientPaging');
//			alert(rows)
		}
	});
```



