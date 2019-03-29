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

SELECT ?z WHERE {
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

SELECT ?x WHERE {
    ?x a b:flow;
       b:flowOf ?z;
       b:hasTemporalExtent ?y.
    ?z a b:flow-object.
    ?y time:hasBeginning ?low;
       time:hasEnd ?up;
       a time:ProperInterval
}
```

---

__What is the location of the agent performing the activity $y$?__

```sparql
PREFIX b: <http://ontology.bonsai.uno/core#>

SELECT ?a ?loc WHERE {
    ?a b:performs y;
       a agent;
       b:location ?loc
}
```

---

__What other agents performing the same type of activity of agent $z$ are present in the same location $w$?__
 
The other agents I called $a$ and here z is a constant instead of a variable in sparql so I’ll leave it as a z. I also removed z from the result set since this is a given.

```
PREFIX b: <http://ontology.bonsai.uno/core#>

SELECT ?a WHERE {
    z a b:agent;
      b:performs ?w;
      b:location ?l.
    ?y b:performs ?w;
       b:location ?l.
    MINUS { z }
}
```

---
 
__How are the flow objects quantified? / Which units of measure are used?__

```
PREFIX b: <http://ontology.bonsai.uno/core#>
PREFIX om: <http://www.ontology-of-units-of-measure.org/resource/om-2/>

SELECT ?x ?unit WHERE {
    ?x a b:flowObject.
    ?z a b:flow;
       b:objectType ?x;
       om:hasUnit ?unit
}
```
