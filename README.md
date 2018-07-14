# CSV to HTML Table

Display any CSV file as a sortable HTML table.

## Usage

#### Add your CSV file to the `data/` folder

#### In `index.html` set your options in the `CsvToHtmlTable.init()` function

``` html
<script>
  CsvToHtmlTable.init({
    csv_path: 'data/Health Clinics in Chicago.csv', 
    element: 'table-container', 
    allow_download: true,
    csv_options: {separator: ',', delimiter: '"'},
    datatables_options: {"paging": false}
  });
</script>
```

##### Available options

* `csv_path` Path to your CSV file.
* `element` The HTML element to render your table to. Defaults to `table-container`
* `allow_download` if true, shows a link to download the CSV file. Defaults to `false`
* `csv_options` jQuery CSV configuration. Use this if you want to use a custom `delimiter` or `separator` in your input file. See [their documentation](https://code.google.com/p/jquery-csv/wiki/API#$.csv.toArrays%28%29).
* `datatables_options` DataTables configuration. See [their documentation](http://datatables.net/reference/option/).
* `custom_formatting` **New!** A list of column indexes and custom functions to format your data (see below)


##### Custom formatting
If you want to do custom formatting for one or more column, you can pass in an array of arrays containing the index of the column and a custom function for formatting it. You can pass in multiple formatters and they will be executed in order.

The custom functions must take in one parameter (the value in the cell) and return a string:

Example:

``` html
<script>

  //my custom function that creates a hyperlink
  function format_link(link){
    if (link)
      return "<a href='" + link + "' target='_blank'>" + link + "</a>";
    else
      return "";
  }

  //initializing the table
  CsvToHtmlTable.init({
    csv_path: 'data/Health Clinics in Chicago.csv', 
    element: 'table-container', 
    allow_download: true,
    csv_options: {separator: ',', delimiter: '"'},
    datatables_options: {"paging": false},
    custom_formatting: [[4, format_link]] //execute the function on the 4th column of every row
  });
</script>
```

#### Run it

You can run this locally using this handy python command:

```bash
python -m SimpleHTTPServer
```

navigate to http://localhost:8000/

## Dependencies

* [Bootstrap](http://getbootstrap.com/) - Responsive HTML, CSS and Javascript framework
* [jQuery](https://jquery.com/) - a fast, small, and feature-rich JavaScript library
* [jQuery CSV](https://github.com/evanplaice/jquery-csv/) - Parse CSV (Comma Separated Values) to Javascript arrays or dictionaries.
* [DataTables](http://datatables.net/) - add advanced interaction controls to any HTML table.

