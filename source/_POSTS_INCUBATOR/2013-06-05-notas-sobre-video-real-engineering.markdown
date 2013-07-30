
- La ingeniería del software, tal y como se enseña en la universidad, no funciona.
- No funciona porque no es capaz de controlar de forma fiable ni costes, ni planificiación
ni calidad.
- Ingeniería -> Conceptos que funcionan.
- Una definición de ingeniería, independientemente del campo donde se aplique, podría ser:
técnicas, herramientas e ideas que han demostrado a través de la experiencia de la experiencia
de quien las practica que funciona fiablemente en su campo de actuación.
- 3 puntos a favor del desarrollo software como ingeniería:
1. Un software se diseña mejor mediante tests que realizando los tests al final.
2. Una simulacioón de los requisitos controla el diseño del sistema.
3. El diseño total se consigue repitiendo esos pasos en módulso cada vez más profundos.
- Estos puntos, enunciados en 1968 durante la 1ª conferencia sobre ingeniería del software,
nos recuerdan a TDD, diseño evolutivo o emergente, simuladores, desarrollo iterativo, 
metodologías ágiles, ...
- Si ya en 1968 se detectaron algunas buenas prácticas, que pasó a partir de entonces?
Puede que una razón sea que se malentendió un paper de 
[Winston W. Royce](https://en.wikipedia.org/wiki/Winston_W._Royce) donde describía un proceso
de desarrollo software que NO funcionaría, pero resulta que se entendió como todo lo contrario.
- 1970. Royce, Winston (1970), 
"[Managing the Development of Large Software Systems](http://www.cs.umd.edu/class/spring2003/cmsc838p/Process/waterfall.pdf)", 
Proceedings of IEEE WESCON 26 (August): 1–9.
- En ingeniería, la gente diseña a través de documentación, por lo que si no haces cálculos y lo 
demuestras matemáticamente, no sabes si funcionará.

- Entonces, a qué se parece la verdadera ingeniería? Es una actividad fundamentalmente
creativa formada por falsos inicios, extrañas ideas, errores, callejones sin salida e
indirecciones en el diseño.

- Cada rama de ingeniería es diferente a las demás (materiales, restricciones, fuerzas,
diseños, artefactos, ..). Así pues, porqué nos empeñamos en que la ingeniería del software
sea *igual* a alguna de ellas?
- Proceso empírico: proporciona y ejerce control a través de inspecciones frecuentes y adaptación
de los procesos que han sido definidos imperfectamente y que no generan salidas predecibles y repetibles.

- El coste es siempre un **objeto** en ingeniería, algo a tener en cuenta en el diseño.

- Ingeniería es el arte de optimizar un diseño dadas unas restricciones, y una de ellas es siempre
el *coste*.

- Los ingenieros construyen modelos, los prueban, prueban sus límites, los hacen de distintos
tamaños para comprobar cómo escalan y sobretodo comprueban que sus suposiciones se corresponden
con la realidad.

- Los avances en ingeniería vienen de aquellos que la practican, no de los teóricos.
- El desarrollo de software no es la única rama que ha perdido el sentido de lo que significa
la ingeniería.
- Los modelos matemáticos sirven para ahorrar costes evitando sobredimensionar, evitando construir
grandes y caros modelos físicos.
- Los ingenieros estructurales no dibujan su diseño y lo lanzan para que lo construyan. Si no
que hacen un seguimiento de la construcción y aprenden durante el proceso.
- Tanto el coste como el atractivo (belleza) son temas a tener en cuenta en la ingeniería.

- El software no es como un puente que debe soportar enormes fuerzas. El software es *blando*, 
lo que debe hacer es adaptarse a los cambios.

- La diferencia más importante con otras ingenierías es la estructura de costes. En otras el 
material y la construcción es el mayor coste. En software es el diseño (el código fuente) 
lo que más cuesta. Construirlo (generar la aplicación) cuesta cero.

- [El código fuente es el diseño](http://c2.com/xp/TheSourceCodeIsTheDesign.html)

- El código fuente es el modelo de la realidad, es un modelo estático de una realidad dinámica. 
Y para saber que funciona hay que probarlo. Pero esas pruebas pueden tener un coste ínfimo 
(automatizándolas) si se comparan con tests de otras ingenierías.

- En otras ingenierías se diseña mediante documentos. Nuestros tests (junit, cucumber, 
fitness, ...) son documentos, pero que además pueden hacer trabajo por nosotros.
- ¿Cómo sería un proceso empírico en el desarrollo de software? Parecido a metodologías ágiles
o eXtreme Programming, donde existen muchos puntos de controlo (tests) a distintas escalas:
pair programming, tests unitarios, de integración, release del sprint, ...

- La realidad de la ingeniería del software:
* El software no se parece *nada* a construir puentes o casas.
* Al ser más complejo (debido a que creamos artefactos multidimensionales abstracto, sea lo 
que sea eso) es más difícil tomar requisitos y realizar el diseño en base a ellos.
* El código fuente es nuestro modelo y nuestras matemáticas.
* Construir y probar se puede considerar que tiene coste cero.
* Los procesos empíricos son los que funcionan con el desarrollo de software.
- ¿Qué es lo que viene?:
* Aprender de los practicantes.
* Tender hacia los procesos empíricos, no hacia procesos definidos y estáticos.
* Impulsar la innovación contínua.
* Llamemos ingeniería a 'lo que funciona', luego, las metodologías ágiles es lo que podríamos
llamar hoy en día INGENIERÍA DEL SOFTWARE, ya que es un proceso empírico, que funciona, 
demostrado día a día por practicantes del desarrollo.
