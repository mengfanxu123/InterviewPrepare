# question in interview

### How to validate a from

* Client-side validation :  

  * javaScript validation is coded using JavaScript: validation API and use Regular Expression with required pattern
  * Built-in form validation : use HTML5 form validation feature : HTML5 validation attribute 

* server side validation

{% code title="build-in validation" %}
```markup
<form>
<input type="text" id="choose" name="ilike" required/>
<button>submit</button>
</form>
```
{% endcode %}

```css
input : invalid {
    border : 2px dashed red
}
input: valid {
    border: 2px solid black
```

```markup
<form>  
 <label for="choose">Would you prefer a banana or a cherry?</label> 
 <input id="choose" name="i_like" required pattern="banana|cherry"> 
 <button>Submit</button>
</form>    
```



