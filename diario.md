# 100 Days Of Code - Log

### Día 0: 15/08/2018

**Progreso**: Lectura de variables del input, clases Card y Player.

**Consideraciones:** 

Para almacenar las cartas en las distintas partes del campo he decidido hacerlo con unerdered_map, usando la instanceId de la carta como clave. He tenido en cuenta la complejidad de 4 operaciones: insert (constante), erase (constante), ~~find~~ operador[], at (constante) e iteraciones (linear). Creo que unordered_set cumpliría la misma función, pero veo más intuitivo usar un map.

*nota: Me había confundido con find, parece ser que find devuelve un iterator hasta el elemento que se le pasa o al último elemento si no lo encuentra. A mi el que me interesaba era el de acceso a un elemento, que es con el operador[] o función at*


No me ha quedado claro cual es la mejor forma para concatenar strings o si siquiera es necesario hacerlo, por ahora estoy escribiendo directamente en el output.

Definitivamente no me ha quedado del todo claro como trabajar con punteros y referencias, [esta respuesta de stackoverflow](https://stackoverflow.com/a/28778902) me ha ayudado mucho.

**Acción tomada:** Siempre pasa.

**Código:** [Día 0](https://github.com/Orzzet/codingame/commit/82b3a4a1b842aa9e96c367c0fcf2512f38c8aa03)

### Día 1: 16/08/2018

**Progreso**: 
Wood3 -> Bronze

Comportamiento básico. Sólo toma en cuenta las criaturas y la habilidad Guarda de las criaturas del rival. No toma en cuenta artefactos ni otras habiliades de criatura.

**Consideraciones:** 

He hecho bastante en este día, aunque la mayor parte no será útil ya que las funciones están pensadas para un comportamiento básico del bot, no para simulaciones. De todas formas ha venido bien para llegar a Bronze y desbloquear todas las reglas. En un futuro es posible que use un comportamiento básico como éste para simular al oponente en las simulaciones.

De no ser por la ayuda del IDE (CLion de Jetbrains), me habría costado mucho más trabajar con punteros y referencias, todavía me asombro de lo relativamente sencillo que me ha resultado.

No estoy seguro de que no haya memory leaks. Por ahora no es un problema ya que el programa corre durante muy poco tiempo y no hay limitaciones de memoria, pero es algo que tendré que revisitar constantemente hasta asegurarme.

**Acción tomada:** 

Pick: Elige carta basandose en coste vs ataque y defensa (valor). 

Play: Juega la/s carta/s con mayor coste posible. 

Attack: Ataca basandose en la diferencia de valor, teniendo en cuenta si el oponente tiene Guarda.

**Código:** [Día 1](https://github.com/Orzzet/codingame/commit/f663dbbf2f61b2e010c99692dde0d9e4481aebc1)

### Día 2: 17/08/2018

**Progreso**:
Bronze

Conseguida la creación de nuevos estados aunque sin implementar el motor del juego. Nuevas clases State y StateManager.

**Consideraciones:**

He metido toda la información necesaria para el juego en la clase Player. Cada Player guarda las cartas de su mano y las cartas en juego, además de la vida, mana, runas, nº cartas en deck y nº en mano. Debido a esto para pasar de un estado a otro lo que tengo que hacer es copiar los objetos player1 y player2 y efectuarle los cambios de todo el turno. El nuevo estado tendrá estos nuevos objetos player1 y player2 con los cambios hechos.

Mi principal problema era encontrar un buen método para copiar los objetos y que las copias de todos sus atributos (incluida cartas individuales) ocupen nuevas posiciones de memoria. He optado por modificar el constructor copia de Card y Player, que modifica el comportamiento del operador = . *"Card* newCard = oldCard" disparará el constructor copia*

*nota: me he llevado un buen tiempo detrás de un error al hacer la copia. Tenía que crear el constructor por defecto "Card() = default"*

Para ahorrar un poco de memoria y procesamiento, los atributos de la clase Card que no varían (cardNumber, instanceId, cardType...) ahora son punteros. Al hacer una copia de una carta, simplemente se pasa el puntero sin necesidad de almacenar el dato otra vez. En un futuro sería buena idea hardcodear todas las cartas en el programa en un map con cardNumber como clave, entonces ni siquiera sería necesario almacenar los punteros.

**Acción tomada:** *igual que en el día anterior*

Pick: Elige carta basandose en coste vs ataque y defensa (valor). 

Play: Juega la/s carta/s con mayor coste posible. 

Attack: Ataca basandose en la diferencia de valor, teniendo en cuenta si el oponente tiene Guarda.

**Código:** [Día 2](https://github.com/Orzzet/codingame/commit/3b3017de6a0003024920cdb3a9db2ad8974bc0d0)

### Día 3: 18/08/2018

**Progreso**:
Bronze

Implementada lista de acciones posibles para el jugador 1 dado un estado del juego.

**Consideraciones**

He implementado la función "unordered_set<string> legalActions(State* s)" que devuelve una lista de acciones posibles para el jugador 1. Para empezar sólo quiero simular las acciones posibles en un turno (o quizás dos) sin tener en cuenta el rival.
  
Además he añadido el atributo "canAttack" a las cartas para tener en cuenta el mareo de invocación y si esa carta ha atacado ya. Además si esa carta tiene ataque 0 obligarla a que no pueda atacar poniendo "canAttack" a false. Mi plan es jugar los items primero, luego criaturas y luego atacar.

*Nota: También es necesario añadir el atributo "turnPlayed" para que los items no modifiquen de forma erronea canAttack.*

Este atributo para las cartas que sean items no tiene sentido, pero no quiero tener items y criaturas en clases separadas solo por este atributo, creo que complicaría las cosas.
 
**Acción tomada:** *igual que en el día anterior*

Pick: Elige carta basandose en coste vs ataque y defensa (valor). 

Play: Juega la/s carta/s con mayor coste posible. 

Attack: Ataca basandose en la diferencia de valor, teniendo en cuenta si el oponente tiene Guarda.

**Código:** [Día 3](https://github.com/Orzzet/codingame/commit/a3b596e7cec92b4f34f7aad845b4164e7312b7ce)

### Día 4: 18/08/2018

**Progreso**:
Bronze

Motor de la simulación completo. Función de evaluación. cambiado getValue(). ~1000 sims/ms? Falta el motor de búsqueda.

**Consideraciones**

En la clase Card, he cambiado el nombre del método getValue() a getPickValue(), que te de el valor de la carta en la fase de draft. Falta implementar en la clase Card el método getBoardValue() (o un nombre similar) para que devuelva el valor de la carta una vez jugada (el coste de la carta y los efectos de cuando entra en juego serían irrelevantes)

He implementado una función evaluación que, dado un estado del juego, lo puntúa. A mayor puntuación, mejor es ese estado para el jugador 1. Pasa muchas cosas por alto, como por ejemplo el valor de las criaturas en juego ya que sólo tiene en cuenta el nº de criaturas en cada lado del campo.

He implementado un motor básico del juego. Dado un estado del juego y una acción a tomar por el jugador 1, devuelve un nuevo estado con la modificación producida por esa acción. Parece ser que al menos la mayoría funciona correctamente. Cuando implemente un comportamiento más complejo del bot seguiré mejorandolo.

Y ya por fin, he comprobado la eficacia de c++! He cronometrado el tiempo que tardo en hacer las simulaciones. El método ha sido el siguiente:

- Cada turno hago una lista de todas las jugadas posibles que puedo hacer ese turno.
- Por cada acción posible hago 1000 simulaciones.

Parece ser que por ahora el programa tiene la capacidad de hacer algo menos de 1000 simulaciones por ms. Eso es mucho más que lo que  conseguí en python en el concurso CodeOfKutulu, que conseguí unas 1000 sims en 50ms haciendo muchas concesiones. Es importante notar que he usado optimizaciones de c++, lo cual me ha hecho multiplicar el rendimiento por 5 aproximadamente. Las optimizaciones son:

```cpp
#pragma GCC optimize("-O3", "inline", "omit-frame-pointer", "unroll-loops")
```
"-O3" es la más importante, activa [muchas optimizaciones](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html) distintas, que por lo que he entendido, te permiten usar clases, funciones y estructuras de datos de la Standard Template Library (STL, por ejemplo unordered_map y unordered_set) de una forma eficiente.

**Acción tomada:** 

Pick: Elige carta basandose en un valor calculado de la carta, función getPickValue().

Play: Juega la/s carta/s con mayor coste posible. 

Attack: Ataca basandose en la diferencia de valor dado por la función getPickValue(). Esto no tiene mucho sentido, pero aún no tengo implementada la función getBoardValue().

**Código:** [Día 4](https://github.com/Orzzet/codingame/commit/1d92fe16e9655ee9f21c5e96c136265176571627)
