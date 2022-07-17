---
layout: post
title: Interactive HTML tables using DataTables
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [HTML, JQuery, Tools and Libraries]
---

We all must have tried HTML tables and faced it's limitation of being less interactive. In this blog, We'll discuss a JQuery plugin for creating interactive HTML table. DataTables is a powerful jQuery plugin which can be used to create HTML tables with functionality like searching, sorting and pagination. It can use almost any data source like DOM, Ajax, and server-side processing. It is mobile friendly library which can adapt to the viewport size. Many well known companies are using DataTables plugin in their websites because it is free and open source.

Let's see how we can add this in our website and use its advanced features.

In order to `install` it in our machine we can use one of the below methods:

1. Using DataTables CDN - 

```
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.21/css/jquery.dataTables.css">
  
<script type="text/javascript" charset="utf8" src="https://cdn.datatables.net/1.10.21/js/jquery.dataTables.js"></script>

```

2. Local Installation - We can [download](https://datatables.net/download) the files and place it in our folder.

```
<link rel="stylesheet" type="text/css" href="/DataTables/datatables.css">
 
<script type="text/javascript" charset="utf8" src="/DataTables/datatables.js"></script>
```

3. Using Package manager like npm or bower - 
```
npm install datatables.net    # Core library
npm install datatables.net-dt # Styling
```

```
bower install --save datatables.net
bower install --save datatables.net-dt
```

After installation and importing the library in our HTML page. We need to create a HTML table like this.

```
<table id="table_id" class="display">
    <thead>
        <tr>
            <th>Name</th>
            <th>Age</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>James</td>
            <td>24</td>
        </tr>
        <tr>
            <td>Raj</td>
            <td>25</td>
        </tr>
    </tbody>
</table>
```

In the Javascript, we need to initialise the DataTables.

```
$(document).ready(function () {
    $('#table_id').DataTable();
});
```

That's it. If we run it, we'll get something like this:

![alt text](https://www.dropbox.com/s/3ow3cspdhk9w0ue/Screen%20Shot%202020-06-27%20at%205.20.57%20PM.png?dl=0)

Now let's dynamically create the table and pass the data in Javascript itself.

```
var data = [{"Name":"Paul",
				"Age": 22,
				"Location": "Canada",
				"Contact": "+1290418345"
			},
			{"Name":"Erica",
				"Age": 32,
				"Location": "Miami",
				"Contact": "+1992418345"
			},
			{"Name":"Pritam",
				"Age": 29,
				"Location": "India",
				"Contact": "+91977418345"
			},
			{"Name":"Williams",
				"Age": 20,
				"Location": "England",
				"Contact": "+324290418345"
			}
			];
```

We created an array of JSON objects. Now we can pass this data to DataTable instance.

```
$('#table_id').DataTable({
    	"destroy":true,    			// In order to reinitialize the datatable
    	"pagination": true,    		// For Pagination
    	"sorting": true,				// For sorting
    	"aaData": data,
    	"columns": [{"data":"Name"}, {"data":"Age"}, {"data":"Location"}, {"data":"Contact"}]
    });
```

![alt text](https://www.dropbox.com/s/o81wu4hrtw6t092/Screen%20Shot%202020-06-27%20at%206.03.54%20PM.png?dl=0)

Sometimes we may need to use buttons(or some other HTML element) also in the table itself to process the data of that row. We can do that with the help of DataTables. Following code can help us accomplish that.

```
{"data":null, render: function(data, type, row, meta) {
    		return "<button value=" + data['Contact'] +">Click!</button>"
}}
```

In this example, we put a button by clicking that we can see the contact number of that particular person.

```
$('button').on('click', function(){
    	alert($(this).val());
});
```

![alt text](https://www.dropbox.com/s/x1wzkkmffqdov6s/Screen%20Shot%202020-06-27%20at%206.15.40%20PM.png?dl=0)

Below is the complete code for this tutorial:

```
<!DOCTYPE html>
<html>
<head>
<title>DataTable Tutorial</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.21/css/jquery.dataTables.css">
<script type="text/javascript" charset="utf8" src="https://cdn.datatables.net/1.10.21/js/jquery.dataTables.js"></script>
<script>
	$(document).ready( function () {
	var data = [{"Name":"Paul",
				"Age": 22,
				"Location": "Canada",
				"Contact": "+1290418345"
			},
			{"Name":"Erica",
				"Age": 32,
				"Location": "Miami",
				"Contact": "+1992418345"
			},
			{"Name":"Pritam",
				"Age": 29,
				"Location": "India",
				"Contact": "+91977418345"
			},
			{"Name":"Williams",
				"Age": 20,
				"Location": "England",
				"Contact": "+324290418345"
			}
			];
			

    $('#table_id').DataTable({
    	"destroy":true,    			// In order to reinitialize the datatable
    	"pagination": true,   		// For Pagination
    	"sorting": true,				// For sorting
    	"aaData": data,
    	"columns": [{"data":"Name"}, {"data":"Age"}, {"data":"Location"}, {"data":null, render: function(data, type, row, meta) {
    		return "<button value=" + data['Contact'] +">Click!</button>"
    	}}]
    });

    $('button').on('click', function(){
    	alert($(this).val());
    });
	});
</script>
</head>
<body>

<table id="table_id" class="display">
    <thead>
        <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Location</th>
            <th>Contact</th>
        </tr>
    </thead>
    
</table>

</body>
</html>
```

That's all for now. Hope you guys liked it. Now it's your turn to try it and make your boring HTML table a bit interactive and fun to use. Happy coding :)