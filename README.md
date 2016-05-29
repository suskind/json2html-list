# json2html-list
Converts JSON to HTML UL-LI list

## Install 

### Bower 
```bash
bower install --save json2html-list 
```

```html
<script src="./bower_components/json2html-list/index.js"></script>
```

### Npm
```bash
npm install --save json2html-list
```

```js
var JSON2HTMLList = require('json2html-list');
```


## How To: 

```html

<div id="output">
</div> 

<script>

var jsonObj = {
    prop1: 'value 1',
    prop_obj: {
        prop2: 'value 2',
        prop3: 3,
        prop4: [
            'item 5',
            'item 6'
        ]
    }
};

var html = JSON2HTMLList(jsonObj);

document.getElementById('output').appendChild(html);

</script>

```

## Options 
 * *container:* (default: *div*) tag name to list container, this container will be returned
 * *formatContainer:* function to format container element. Will receive container element as parameter 
 * *formatUl:* function to format each UL element. Will receive UL elements as parameter 
 * *formatLi:* function to format each LI element. Will receive LI elements as parameter 
 * *formatProperty:* function to format each found object property. Will receive a object property as text node 
 * *formatValue:* function to format each object or array value. Will receive the value as text node and the correspondent property (if array will receive array index)

## How To with Options: 

```html

<div id="output">
</div> 

<script>

var jsonObj = {
    prop1: 'value 1',
    prop_obj: {
        prop2: 'value 2',
        prop3: 3,
        propPre: 'This \nwill be \n a pre',
        prop4: [
            'item 5',
            'item 6'
        ]
    }
};

var options = {
    formatContainer: function(cont) {
        cont.className = 'my-container-class';
        return cont;
    }, 
    formatUl: function(ul) {
        ul.className = 'my-ul-class';
        return ul;
    },
    formatLi: function(li) {
        li.className = 'my-li-class';
        return li;
    },
    formatProperty: function(prop) {
        var strong = document.createElement('strong');
        strong.appendChild(prop);
        strong.appendChild(document.createTextNode(': '));

        return strong;
    },
    formatValue: function(value, prop) {
        var elm;
        if(prop === 'propPre') {
            elm = document.createElement('pre');
        } else {
            elm = document.createElement('span');
        }
        elm.appendChild(value);
    
        return elm; 
    }
};

var html = JSON2HTMLList(jsonObj, options);

document.getElementById('output').appendChild(html);

</script>

```



## Converts this JSON 
```js
{
    "glossary": {
        "title": "example glossary",
        "GlossDiv": {
            "title": "S",
            "GlossList": {
                "GlossEntry": {
                    "ID": "SGML",
                    "SortAs": "SGML",
                    "GlossTerm": "Standard Generalized Markup Language",
                    "Acronym": "SGML",
                    "Abbrev": "ISO 8879:1986",
                    "GlossDef": {
                        "para": "A meta-markup language, used to create markup languages such as DocBook.",
                        "GlossSeeAlso": [
                            "GML",
                            "XML"
                        ]
                    },
                    "GlossSee": "markup"
                }
            }
        }
    }
}
```
## Into this HTML 
```html
<div class="container">
    <ul class="ul-item">
        <li class="li-item"><strong>glossary</strong>
            <ul class="ul-item">
                <li class="li-item"><strong>title</strong><span>example glossary</span></li>
                <li class="li-item"><strong>GlossDiv</strong>
                    <ul class="ul-item">
                        <li class="li-item"><strong>title</strong><span>S</span></li>
                        <li class="li-item"><strong>GlossList</strong>
                            <ul class="ul-item">
                                <li class="li-item"><strong>GlossEntry</strong>
                                    <ul class="ul-item">
                                        <li class="li-item"><strong>ID</strong><span>SGML</span></li>
                                        <li class="li-item"><strong>SortAs</strong><span>SGML</span></li>
                                        <li class="li-item"><strong>GlossTerm</strong><span>Standard Generalized Markup Language</span></li>
                                        <li class="li-item"><strong>Acronym</strong><span>SGML</span></li>
                                        <li class="li-item"><strong>Abbrev</strong><span>ISO 8879:1986</span></li>
                                        <li class="li-item"><strong>GlossDef</strong>
                                            <ul class="ul-item">
                                                <li class="li-item"><strong>para</strong><span>A meta-markup language, used to create markup languages such as DocBook.</span></li>
                                                <li class="li-item"><strong>GlossSeeAlso</strong>
                                                    <ul class="ul-item">
                                                        <li class="li-item"><span>GML</span></li>
                                                        <li class="li-item"><span>XML</span></li>
                                                    </ul>
                                                </li>
                                            </ul>
                                        </li>
                                        <li class="li-item"><strong>GlossSee</strong><span>markup</span></li>
                                    </ul>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
            </ul>
        </li>
    </ul>
</div>
```
