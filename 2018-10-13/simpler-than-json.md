# Simpler than JSON -> Scheme or Python tuple

2018-10-13

Source:

* https://jsdelfino.blogspot.com/2009/11/simpler-than-json.html

## Comparing

## XML

```xml
<ns2:root xmlns:ns2="http://tuscany.apache.org/xmlns/sca/databinding/jaxb/1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="cart">
  <items xsi:type="fruit">
    <name xmlns="">Apple</name>
    <price xmlns="">2.99</price>
  </items>
  <items xsi:type="fruit">
    <name xmlns="">Orange</name>
    <price xmlns="">3.55</price>
  </items>
  <items xsi:type="vegetable">
    <name xmlns="">Broccoli</name>
    <price xmlns="">1.99</price>
  </items>
</ns2:root>
```

### XML without the namespace mess -> a little better

```xml
<cart>
  <fruit>
    <name>Apple</name>
    <price>2.99</price>
  </fruit>
  <fruit>
    <name>Orange</name>
    <price>3.55</price>
  </fruit>
  <vegetable>
    <name>Broccoli</name>
    <price>1.99</price>
  </vegetable>
</cart>
```

### XML with attributes instead of elements -> shorter

```xml
<cart>
  <fruit name="Apple" price="2.99"/>
  <fruit name="Orange" price="3.55"/>
  <vegetable name="Broccoli" price="1.99"/>
</cart>
```

### JSON -> not simpler than XML

```json
{"cart":[
  {"fruit":{"name":"Apple","price":2.99}},
  {"fruit":{"name":"Orange","price":3.55}},
  {"vegetable":{"name":"Broccoli","price":1.99}}]}
```

and then

```json
{"cart":{  "fruit":[
    {"name":"Apple","price":2.99},
    {"name":"Orange","price":3.55}],
  "vegetable":{"name":"Broccoli","price",1.99}
}}
```

### YAML -> not bad, need some artificial attributes to each item or awkard with more levels of nesting

```yaml
cart:
  - type: fruit
    name: Apple
    price: 2.99
  - type: fruit
    name: Orange
    price: Pear
  - type: fruit
    name: Orange
    price: 3.55
  - type: vegetable
    name: Broccoli
    price: 1.99
```

### Scheme -> not bad at all

```scheme
'(cart
  (fruit (name "Apple")(price 2.99))
  (fruit (name "Orange")(price 3.55))
  (vegetable (name "Broccoli")(price 1.99)))
```

> That Scheme language representation is not bad at all!
> - it's really concise;
> - the Scheme syntax is simple and easy to parse, () for lists, space as a separator;
> - as the above expression is just constructing lists, I don't need to make my shopping cart data fit in Objects, Arrays or Maps;
> - it's easy to distinguish symbols like fruit or name and user data like "Apple".
> - a list can simply be tagged with a fruit or vegetable symbol to indicate its type;
> - like JSON, the above expression is a piece of code easy to evaluate and test in a Scheme interpreter.

### Python tuple -> A little more verbose than scheme, but not bad

```python
('cart',
  ('fruit',('name','Apple'),('price',2.99)),
  ('fruit',('name','Orange'),('price',3.55)),
  ('vegetable',('name','Broccoli'),('price',1.99)))
```

## Summary

> So, I must admit... I think I much prefer the [Scheme](http://groups.csail.mit.edu/mac/projects/scheme/)
> representation, or the Python tuple syntax. I realize that Scheme was created in the 70's, but hey, that doesn't mean
> it's bad :) -- see the [Wikipedia entry on Scheme](http://groups.csail.mit.edu/mac/projects/scheme/) for its history.

> I also realize that JSON is natively supported by the JavaScript interpreters used in Web browsers... but it looks
> like most people are using handcrafted JSON [parser](https://www.json.org/) implementations (written in JavaScript)
> instead of the native JavaScript eval() or JSON.parse() so that argument is not very solid... and it shouldn't be
> hard to write similar parsers for the Scheme or Python syntaxes as well.
