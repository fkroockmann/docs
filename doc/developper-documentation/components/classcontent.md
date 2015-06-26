# ClassContent

## Parameters

Parameters allow to configure your content easily, he is used usually in the listener but can be used everywhere. Parameters is contributed on front by the user with the gearing button of block.

Parameters is builded from the block's YAML like

```
BlockDemo:
    properties:
        name: Block demo
        description: "Block for demonstration purposes"
        category: [Demo]
    elements:
        text:
            type: BackBee\ClassContent\Element\Text
    parameters:
        mytext:
            label: 'My text'
            type: 'text'
            value: ''
        myselect:
            label: 'My select'
            type: 'select'
            options:
                'foo': 'Foo'
                'bar': 'Bar'
            value: ['foo']

```

### Use parameters

If parameters is not validated by user the content parameters is overrided by revision parameters. 
**Only value of the parameter is saved.**

For get default parameters:
``` PHP
$params = $content->getDefaultParams();

# That return all parameters with definitions and default values
array (size=2)
  'mytext' => 
    array (size=3)
      'label' => string 'My text' (length=7)
      'type' => string 'text' (length=4)
      'value' => string '' (length=0)
  'myselect' => 
    array (size=4)
      'label' => string 'My select' (length=9)
      'type' => string 'select' (length=6)
      'options' => 
        array (size=2)
          'foo' => string 'Foo' (length=3)
          'bar' => string 'Bar' (length=3)string 'yolo' (length=4)
      'value' => 
        array (size=1)
          0 => string 'foo' (length=3)
```

For get all parameters :
``` PHP
$params = $content->getAllParams();

# That return all parameters with definitions and new values
array (size=2)
  'mytext' => 
    array (size=3)
      'label' => string 'My text' (length=7)
      'type' => string 'text' (length=4)
      'value' => string '' (length=0)
  'myselect' => 
    array (size=4)
      'label' => string 'My select' (length=9)
      'type' => string 'select' (length=6)
      'options' => 
        array (size=2)
          'foo' => string 'Foo' (length=3)
          'bar' => string 'Bar' (length=3)
      'value' => 
        array (size=1)
          0 => string 'foo' (length=3)
```

For get one param:

```PHP
$param = $content->getParam('mytext');

#That return the definition and new value
array (size=3)
  'label' => string 'My text' (length=7)
  'type' => string 'text' (length=4)
  'value' => string '' (length=0)
```

For get the value of the param:
```PHP
$paramValue = $content->getParamValue('mytext');

#that return the new value
string '' (length=0)
```

For set a value, you need to set a same type which you declare in YAML file as value:
```PHP
$content->setParam('mytext', 'foo');
$param = $content->getParamValue('mytext')

#That return a new value set
string 'foo' (length=3)

```

## Describe all available parameters

- checkbox
- datetimepicker
- hidden
- linkSelector
- mediaSelector
- nodeSelector
- password
- radio
- select
- text
- textarea

All parameters has default options:

#### Default options

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**label** |  String | Label is display above the field | Empty | No
**value** | Mixed | This field must be set and allow to describe type of the  parameter | None | Yes |
**type** | String | Key of one of available parameters | None | Yes |

***

#### Checkbox

Like HTML checkbox attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**options** |  Array | List of options (key/value) | Empty array | Yes
**inline** | Boolean | Display checkbox inline | false | No |
**value** | Array | List of selected checkbox | Empty array | Yes |

**Exemple**: 

``` 
parameters:
    mycheckbox:
        type: 'checkbox'
        options:
            'foo': 'Foo'
            'bar': 'Bar'
        value: ['foo']
        inline: true
```
```
$param = $content->getParamValue('mycheckbox');
# array('foo')
```
***

#### Datetime picker

Element text with a datetimepicker

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | Number | It is an timestamp value | Empty | Yes |

**Exemple**: 

``` 
parameters:
    mydatetimepicker:
        type: 'datetimepicker'
        value: 1435573740
```
```
$param = $content->getParamValue('mydatetimepicker');
# return 1435573740
```
***

#### Hidden

Like HTML hidden attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | String | The default text  | Empty | Yes |

**Exemple**: 

``` 
parameters:
    myhidden:
        type: 'hidden'
        value: 'foo'
```
```
$param = $content->getParamValue('myhidden');
# foo
```
***

#### Link selector

Link selector allow to choose a link from tree page or external link.

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | Json | Object which contains url / title / pageUid / target  | Empty array | Yes |

**Exemple**: 

``` 
parameters:
    mylinkselector:
        type: 'linkSelector'
        value: []
```
```
# Exemple with select one link
$param = $content->getParamValue('mylinkselector');
# array('url' => '/foo', 'title' => 'Foo', 'pageUid' => 'anPageUid', 'target' => '_self')
```
** Page tree **:
We recommend to retrieve the url from the page entity instead of the url attribute cause the url can change.

** Externak link ** :
pageUid attribute is null

***

#### Media selector

Media selector allow to choose a list of media from the media library.

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | Json | Object which contains folder_uid / image / media_id / title /type / uid  | Empty array | Yes |

**Exemple**: 

``` 
parameters:
    mymediaselector:
        type: 'mediaSelector'
        value: []
```
```
# Exemple with select one media
$param = $content->getParamValue('mymediaselector');
# array(array('folder_uid' => 'anFolderUid', 'image' => 'imageUrl', 'media_id' => '1', 'title' => '_Foo', 'type' => 'Media/Image', 'uid' => 'anUid'))
```
***

#### Node selector

Node selector allow to choose a page from tree

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | Json | Object which contains url  pageUid / title  | Empty array | Yes |

**Exemple**: 

``` 
parameters:
    mynodeselector:
        type: 'nodeSelector'
        value: []
```
```
# Exemple with select one node
$param = $content->getParamValue('mynodeselector');
# array('pageUid' => 'anPageUid', 'title' => 'Foo')
```
We recommend to retrieve the title from the page entity instead of the title attribute cause the title can change.

***

#### Password

Like HTML password attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | String | The default text | Empty | Yes |

**Exemple**: 

``` 
parameters:
    mypassword:
        type: 'password'
        value: 'foo'
```
```
$param = $content->getParamValue('mypassword');
# foo
```
***

#### Radio

Like HTML radio attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**options** |  Array | List of options (key/value) | Empty array | Yes
**inline** | Boolean | Display radio inline | false | No |
**value** | Array | List of selected radio | Empty array | Yes |

**Exemple**: 

``` 
parameters:
    myradio:
        type: 'radio'
        options:
            'foo': 'Foo'
            'bar': 'Bar'
        value: ['foo']
        inline: true
```
```
$param = $content->getParamValue('myradio');
# array('foo')
```
***

#### Select

Like HTML select attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**options** |  Array | List of options (key/value) | Empty array | Yes
**value** | Array | List of selected radio | Empty array | Yes |
**multiple** | Boolean | Allow to multiple selection | false | No

**Exemple**: 

``` 
parameters:
    mypassword:
        type: 'select'
        options:
            'foo': 'Foo'
            'bar': 'Bar'
        value: ['foo']
        multiple: true
```
```
$param = $content->getParamValue('myradio');
# array('foo')
```
***

#### Text

Like HTML text attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | String | The default text | Empty | Yes |

**Exemple**: 

``` 
parameters:
    mytext:
        type: 'text'
        value: 'foo'
```
```
$param = $content->getParamValue('mypassword');
# foo
```
***

#### Textarea

Like HTML textearea attribute

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | String | The default text | Empty | Yes |
**rows** | String | the rows html attribute | 5 | No

**Exemple**: 

``` 
parameters:
    mytextearea:
        type: 'textarea'
        value: 'foo'
	rows: 10
```
```
$param = $content->getParamValue('mytextearea');
# foo
```
***

### Special parameters

#### Rendermode

Rendermode parameters allow to list automatically rendermodes of the content and use it directly.

 |   | Type | Description | Default | Mandatory
--- | --- | --- | --- | ---
**value** | Array | Selected rendermode | Empty | Yes |

``` 
parameters:
    rendermode:
        type: 'select'
        value: []
```
**The key must be 'rendermode'**

