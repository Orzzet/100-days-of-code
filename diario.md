# 100 Days Of Code - Log

### Día 0: 15/08/2018

**Progreso**: Lectura de variables del input, clases Card y Player.

**Consideraciones:** 

Para almacenar las cartas en las distintas partes del campo he decidido hacerlo con unerdered_map, usando la instanceId de la carta como clave. He tenido en cuenta la complejidad de 4 operaciones: insert (constante), erase (constante), find (constante) e iteraciones (linear). Creo que unordered_set cumpliría la misma función, pero veo más intuitivo usar un map.

No me ha quedado claro cual es la mejor forma para concatenar strings o si siquiera es necesario hacerlo, por ahora estoy escribiendo directamente en el output.

Definitivamente no me ha quedado del todo claro como trabajar con punteros y referencias, [esta respuesta de stackoverflow](https://stackoverflow.com/a/28778902) me ha ayudado mucho.

**Acción tomada:** Siempre pasa.

**Código:** [Día 0](https://github.com/Orzzet/codingame/commit/82b3a4a1b842aa9e96c367c0fcf2512f38c8aa03)

### Día 1: 16/08/2018

**Progreso**: 
Wood 3 -> Bronze

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
