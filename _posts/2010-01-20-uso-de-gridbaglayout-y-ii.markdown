---
title: "Uso de GridBagLayout (y II)"
date: 2010-01-20 07:54
author: Rubén Chavarría
categories: 
- java
- swing
- gridbaglayout
- swing layout manager
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

Antes de leer esta entrada deberías leer
[Uso de GridBagLayout (I)]({{ site.baseurl }}{% post_url 2009-12-21-uso-de-gridbaglayout-i %}),
si no lo has hecho ya.

Veamos algunos parámetros que nos permitirán configurar cómo se verán nuestros 
componentes con más flexibilidad que la conseguida con los parámetros vistos en 
el post anterior:

<!-- more -->

## fill

Define la forma en la que el componente crecerá o no cuando se cambie el tamaño 
del panel al que pertenece. Los valores posibles están definidas como constantes 
en `GridBagConstraints` y son:

- `NONE`: valor por defecto. Indica que el componente no cambiará su tamaño
- `HORIZONTAL`: hará crecer el componente hasta completar el tamaño horizontal 
de la celda o celdas donde se encuentra el componente
- `VERTICAL`: igual que `HORIZONTAL` pero en sentido vertical

## anchor

Este parámetro se utiliza cuando el componente es más pequeño que su área de 
dibujo - la celda o celdas donde yace el componente - e indica el lugar al que 
el componente quedará fijado cuando se modifique el tamaño del panel. Los 
valores están definidos como constantes en `GridBadConstraints`. Podemos ver 
los valores y el lugar donde el componente quedará fijado en la siguiente tabla:

<div style="display: block; margin: 0 auto">
<table style="text-align:center;border:solid black;background-color:#f0f0f0;">
<tbody>
<tr>
<td>FIRST_LINE_START</td>
<td>PAGE_START</td>
<td>FIRST_LINE_END</td>
</tr>
<tr>
<td>LINE_START</td>
<td>CENTER</td>
<td>LINE_END</td>
</tr>
<tr>
<td>LAST_LINE_START</td>
<td>PAGE_END</td>
<td>LAST_LINE_END</td>
</tr>
</tbody>
</table>
</div>

## weightx y weighty

Estos parámetros especifican cómo distribuir el espacio entre las 
columnas - weightx -  y las filas - weighty -. Los valores que pueden tomar
varían entre 0.0 y 1.0, siendo 1.0 el de más peso, lo que indicaría que ese 
componente ocuparía el mayor espacio posible. Si no se indica lo contrario, 
ambos parámetros toman el valor 0.0, lo que indica a `GridBagLayout` que el 
espacio extra al cambiar el tamaño al panel se dibujará entre el borde de las 
fila y columnas y el borde del contenedor, dejando un espacio libre entre ellos. 

Ahora veamos el código que genera el panel con el gestor `GridBagLayout`:

```java
package es.rchavarria.gridbaglayouthowto;

public class GridBagLayoutDemo extends javax.swing.JPanel {
  public GridBagLayoutDemo() {
    initComponents();
  }

 private void initComponents() {
   java.awt.GridBagConstraints gridBagConstraints;

   btn5 = new javax.swing.JButton();
   btn1 = new javax.swing.JButton();
   btn2 = new javax.swing.JButton();
   btn4 = new javax.swing.JButton();
   btn6 = new javax.swing.JButton();
   btn3 = new javax.swing.JButton();

   setLayout(new java.awt.GridBagLayout());

   btn1.setText(&quot;btn 01&quot;);
   add(btn1, new java.awt.GridBagConstraints());

   btn2.setText(&quot;btn 02&quot;);
   gridBagConstraints = new java.awt.GridBagConstraints();
   gridBagConstraints.gridwidth = 2;
   add(btn2, gridBagConstraints);

   btn3.setText(&quot;btn 03&quot;);
   gridBagConstraints = new java.awt.GridBagConstraints();
   gridBagConstraints.gridx = 0;
   gridBagConstraints.gridy = 1;
   add(btn3, gridBagConstraints);

   btn4.setText(&quot;btn 04&quot;);
   gridBagConstraints = new java.awt.GridBagConstraints();
   gridBagConstraints.gridx = 0;
   gridBagConstraints.gridy = 2;
   gridBagConstraints.fill = java.awt.GridBagConstraints.VERTICAL;
   gridBagConstraints.anchor = java.awt.GridBagConstraints.SOUTH;
   add(btn4, gridBagConstraints);

   btn5.setText(&quot;btn 05&quot;);
   gridBagConstraints = new java.awt.GridBagConstraints();
   gridBagConstraints.gridx = 2;
   gridBagConstraints.gridy = 3;
   gridBagConstraints.fill = java.awt.GridBagConstraints.BOTH;
   add(btn5, gridBagConstraints);

   btn6.setText(&quot;large btn&quot;);
   gridBagConstraints = new java.awt.GridBagConstraints();
   gridBagConstraints.gridx = 1;
   gridBagConstraints.gridy = 1;
   gridBagConstraints.gridwidth = 2;
   gridBagConstraints.gridheight = 2;
   gridBagConstraints.fill = java.awt.GridBagConstraints.BOTH;
   gridBagConstraints.weightx = 1.0;
   gridBagConstraints.weighty = 1.0;
   add(btn6, gridBagConstraints);
 }

 private javax.swing.JButton btn1;
 private javax.swing.JButton btn2;
 private javax.swing.JButton btn3;
 private javax.swing.JButton btn4;
 private javax.swing.JButton btn5;
 private javax.swing.JButton btn6;
}
```

Mediante las líneas del código del tipo: `add(componente, gridBagConstraint);` se especifican las restricciones para cada componente. Es posible utilizar el mismo objeto para especificar las restricciones pero es recomendable utilizar distintas instancias.

Para ver el resultado de este código, simplemente podemos probarlo mediante la siguiente clase:

```java
package es.rchavarria.gridbaglayouthowto;

import javax.swing.JFrame;
import javax.swing.SwingUtilities;

public class RunDemo {
public static void main(String[] args) {
  SwingUtilities.invokeLater(new Runnable() {
    public void run() {
      JFrame frm = new JFrame(&quot;GridBagLayout HowTo&quot;);
      frm.getContentPane().add(new GridBagLayoutDemo());
      frm.pack();
      frm.setVisible(true);
    }
  });
}
}
```
