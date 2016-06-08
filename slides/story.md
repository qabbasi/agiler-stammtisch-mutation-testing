 <!--.slide: data-background="img/background-green-16x9.png" -->

## A long time ago in a galaxy far, far away...

<aside class="notes" data-markdown>
- neues projekt
- anforderung: "wir brauchen 100% testabdeckung" (kundenprojekt)
- tests ohne asserts sind zu trivial
- kleine auswahl von bekannten test pattern
</aside>

---
 <!--.slide: data-background="img/background-green-16x9.png" -->

### The untested side effect <!-- .element: class="fragment" data-fragment-index="2" -->

<!-- .element: class="fragment" data-fragment-index="1" -->
```
public static String foo(boolean b) {
  if ( b ) {
    performVitallyImportantBusinessFunction();
    return "OK";
  }

  return "FAIL";
}

@Test
public void shouldFailWhenGivenFalse() {
  assertEquals("FAIL", foo(false));
}

@Test
public void shouldBeOkWhenGivenTrue() {
  assertEquals("OK", foo(true));
}
```

<aside class="notes">
- No check is ever made that performVitallyImportantBusinessFunction is called.
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### The missing boundary test <!-- .element: class="fragment" data-fragment-index="2" -->

<!-- .element: class="fragment" data-fragment-index="1" -->
```
public static String foo(int i) {
  if ( i >= 0 ) {
      return "foo";
  } else {
      return "bar";
  }
}

@Test
public void shouldReturnBarWhenGiven1() {
  assertEquals("bar", foo(1));
}

@Test
public void shouldReturnFooWhenGivenMinus1() {
  assertEquals("foo", foo(-1));
}
```

<aside class="notes" data-markdown>
- The behaviour when i == 0 is never tested.
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### The myopic mockist <!-- .element: class="fragment" data-fragment-index="2" -->

<!-- .element: class="fragment" data-fragment-index="1" -->
```
public static String foo(Collaborator c, boolean b) {
  if ( b ) {
      return c.performAction();
  }

  return "FOO";
}

@Test
public void shouldPerformActionWhenGivenTrue() {
  foo(mockCollaborator, true);
  verify(mockCollaborator).performAction();
}

@Test
public void shouldNotPerformActionWhenGivenFalse() {
  foo(mockCollaborator, false);
  verify(never(), mockCollaborator).performAction();
}
```

<aside class="notes" data-markdown>
- The return value of the function is never checked.
</aside>

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### Try to describe the very nature of the problem here

---
<!--.slide: data-background="img/background-green-16x9.png" -->

### How do we ensure that our test suite copes well with the relevant stuff?
<aside class="notes" data-markdown>
- die wichtige frage ist...
- am besten automatisiert
</aside>