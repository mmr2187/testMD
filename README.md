# Competency Questions and corresponding Sparql


---
__Is the flow $x$ a determining product for the activity $y$__

Since flow here is a product, I translated it into flow-object. Also, I reread and the flow $x$ and the activity $y$ seems to be a constant. In which case this is a true or false statement.

```sparql
PREFIX b: <http://ontology.bonsai.uno/core#>

SELECT ?z WHERE {
    bind ( exists{
        x b:outputOf y;
        b:determiningFlow y
    } as ?z)
}
```

---
 

__Is input flow $x$ required for activity $y$?__
 
```sparql
PREFIX b: <http://ontology.bonsai.uno/core#>

Select ?z where {
    bind (exists{
        x b:inputOf y;
        b:determiningFlow y
    } as ?z)
}
```

---
  
__What is the amount of flow $x$ emitted as output during the time period $y$ ?__
 
I think $y$ here would be expressed as a lower $low$ bound and an upper $up$ bound. What do we do if we don’t have the actual data but we have to aggregate data in the database?

```sparql
PREFIX b: <http://ontology.bonsai.uno/core#>
PREFIX time: <http://www.w3.org/2006/time#>

Select ?x where {
    ?x a b:flow;
       b:flowOf ?z;
       b:hasTemporalExtent ?y.
    ?z a b:flow-object.
    ?y time:hasBeginning ?low;
       time:hasEnd ?up;
       a time:ProperInterval
}
```
