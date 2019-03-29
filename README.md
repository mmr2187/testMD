# Competency Questions and corresponding Sparql


---
__Is the flow $x$ a determining product for the activity $y$__

Since flow here is a product, I translated it into flow-object. Also, I reread and the flow $x$ and the activity $y$ seems to be a constant. In which case this is a true or false statement.

```sparql
SELECT ?z WHERE {
    bind ( exists{
        x b:outputOf y;
        b:determiningFlow y
    } as ?z)
}
```
