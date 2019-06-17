# HTML

### what is HTML

Hyper Text Markup Language

### Basic elements in HTML 

#### List 

{% code-tabs %}
{% code-tabs-item title="HTML list" %}
```markup
<ul>
    <li>Coffe</li>
    <li>Milk</li>
    <li>Water</li>
</ul>
// order list
<ol>
    <li>Coffe</li>
    <li>Milk</li>
    <li>Water</li>
</ol>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Table

```markup
<table> 
    <tr>
        <th>FristName</th>
        <th>LastMame</th>
    </tr>
    <tr>
        <td>Mandy</td>
        <td>Xu</td>
    </tr>
</table>

table, th, td {
    border : 1px, solid, black
    border-collapse: collapse
}
```

#### Form

```markup
<form>
    <input type="text" value = "name" placehorder = "name">
    <input type = "password" value = "password" placehorder = "password" >
    <input type = "radio" name = "gender" value = "male" checked> male <br>
    <input type = "radio" name = gender" value = "female" > female <br>
    <input type = "submit" value = "Submit>
</form>
```

### New Feature in HTML5

* semantic elements : &lt;header&gt; &lt;footer&gt; &lt;article&gt;  &lt;dialog&gt; &lt;section&gt;
* new form elements: &lt;datalist&gt; &lt;output&gt;
* new input types: color date email month, number
* Graphics: &lt;canvas&gt; &lt;svg&gt;
* new media elements: &lt;audio&gt; &lt;video&gt;

{% code-tabs %}
{% code-tabs-item title="datalist" %}
```markup
<form>
    <input list = "browser" name = "browser">
    <datalist id = "browser" >
        <option value = "Chrome">
        <option value = "Safari">
        <option value ="Firefox">
    </datalist>
    <input type = "submit">
</form>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Attribute vs Property

Attribute are defined on the HTML but property defined on the DOM

### Cookie vs SessionStorage vs LocalStorage

* LocalStorage: store data locally within user browser 
* SessionStorage: store data also locally but when tab closed, data disappear
* cookie: cookie store data on computer

|  | Cookie | LocalStorage | SessionStorage |
| :--- | :--- | :--- | :--- |
| initiator | client or server, can use set-cookie header | client  | client |
| Expiry | manually set | forever | on tab  close |
| persistent  across browser sessions | whether expiration is set | yes | no |
| sent to server with every HTTP request | being sent via cookie | no | no |
| capacity | 4kb | 5mb | 5mb |
| accessibility | any window | any window | same tab |

{% code-tabs %}
{% code-tabs-item title="localStorage" %}
```markup

<html>
<body>
<div id="result"></div>
<script>
// Check browser support
if (typeof(Storage) !== "undefined") {
  // Store
  localStorage.setItem("lastname", "Smith");
  // Retrieve
  document.getElementById("result").innerHTML = localStorage.getItem("lastname");
} else {
  document.getElementById("result").innerHTML = "Sorry, your browser does not support Web Storage...";
}
</script>
</body>
</html>

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Form Validation

HTML5 constraint validation is based on:

* HTML input Attributes: disabled, max, required
* CSS Pseudo Seletors: :disabled, :valid, :required
* DOM Properties and Methods

