 <!--.slide: data-background="img/background-green-16x9.png" -->

## Mutation Testing

Idea: Mutate the code and the tests should _fail_

<aside class="notes" data-markdown>
- philosophie: umgekehrtes denken, tests müssen fehlschlagen, damit die mutanten (defekte) nicht überleben
- technisch: Während der Unit Testlaufzeit werden autom. modifizierte Versionen des Programms getestet.
modifizierte programme sollten andere ergebnisse produzieren, daher schlagen auch die tests fehl 
- effekt: qualität der abdeckung abhängig von überlebenden mutanten
</aside>