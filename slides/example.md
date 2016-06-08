<!--.slide: data-background="img/background-green-16x9.png" -->

### Pitest – „Real world mutation testing“
**[pitest.org](pitest.org)**

- Most popular framework for Java <!-- .element: class="fragment" data-fragment-index="1" -->
- Active development & support <!-- .element: class="fragment" data-fragment-index="2" -->
- Works with Ant, Maven, Gradle and others <!-- .element: class="fragment" data-fragment-index="3" -->
- Human-readable reports containing line and mutation coverage information <!-- .element: class="fragment" data-fragment-index="4" -->
  
<aside class="notes" data-markdown>
- mostly slow, difficult to use, academic research rather than real development teams
- auf github zu finden
- basic concepts: building blocks, einfach zu verstehen
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Mutators

Apply mutation operators to the byte code

<aside class="notes" data-markdown>
- einheit der verändung (operation)
- diverse operationen wie removing methods calls, inverting logic statements, altering return values
- voraussetzung: im byte code sind folgende debug informationen vorhanden: line number, source file name
- allerdings kein problem, da diese üblicherweise von build systemen enabled sind
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Conditionals Boundary Mutator

```
 if ( i >= 0 ) {
     return "foo";
 } else {
     return "bar";
 }
```

mutated into

```
if ( i > 0 ) {
    return "foo";
} else {
    return "bar";
}
```

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Mutants

Java classes containing the injected fault

<aside class="notes" data-markdown>
- pit führt zur testlaufzeit tests gegen die mutanten aus
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Available Mutators
[http://pitest.org/quickstart/mutators/](http://pitest.org/quickstart/mutators/)

- Conditionals Boundary Mutator
- Increments Mutator 
- Invert Negatives Mutator 
- Math Mutator 
- Return Values Mutator 
- Void Method Calls Mutator
- ...

<aside class="notes" data-markdown>
- gut dokumentiert mit beispielen
- vergleichsoperation
- kehrt negation von integer oder floats um -1 wird 1
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Return Values Mutator

```
 public Object foo() {
   return new Object();
 }
```

mutated into

```
public Object foo() {
  new Object();
  return null;
}
```

<aside class="notes" data-markdown>
- return values werden vom counterpart ersetzt, boolean true -> false
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Void Method Calls Mutator
```
 public void someVoidMethod(int i) {
   // serious business logic
 }
 
 public int foo() {
   int i = 5;
   doSomething(i);
   return i;
 }

```

mutated into

```
public void someVoidMethod(int i) {
  // serious business logic
}

public int foo() {
  int i = 5;
  return i;
}
```

<aside class="notes" data-markdown>
- constructor calls are not considered void method calls
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Running The Tests

Attack the suspicious ones!

<aside class="notes" data-markdown>
- ausgefallenes laufzeit system (2 dimensionen)
- traditional line coverage analysis for the tests
- gather data: run time for the tests
- generate mutants based on these 2 inputs
- erlaubt es die ganze code basis zu testen, anstatt nur eine klasse
- für große projekte: incremental analysis. 
</aside>