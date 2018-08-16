# 100 Days Of Code - Log

### Día 0: 15/08/2018

**Progreso**: Lectura de variables del input, clases Card y Player.

**Consideraciones:** 

Para almacenar las cartas en las distintas partes del campo he decidido hacerlo con unerdered_map, usando la instanceId de la carta como clave. He tenido en cuenta la complejidad de 4 operaciones: insert (constante), erase (constante), find (constante) e iteraciones (linear). Creo que unordered_set cumpliría la misma función, pero veo más intuitivo usar un map.

No me ha quedado claro cual es la mejor forma para concatenar strings o si siquiera es necesario hacerlo, por ahora estoy escribiendo directamente en el output.

Definitivamente no me ha quedado del todo claro como trabajar con punteros y referencias, [esta respuesta de stackoverflow](https://stackoverflow.com/a/28778902) me ha ayudado mucho.

**Acción tomada:** Siempre pasa.

**Código:** [Día 0](https://github.com/Orzzet/codingame/commit/82b3a4a1b842aa9e96c367c0fcf2512f38c8aa03)
