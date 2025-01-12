---
author: "Matías Di Bernardo"
title: "Z-Plane Visualizer"
date: "2023-08-12"
description: "Aplicación para visualizar en tiempo real el efecto de los ceros y polos en al plano z."
categories: [
    "Programming",
    "DSP",
]
tags: [
    "Personal Project",
]
image: "frontz.PNG"
math: True
---
En el curso de *Procesamiento Digital de Señales* (DSP) en la UNTREF, exploramos el plano Z para el diseño de filtros con variables discretas. Durante la clase, el profesor presentó una herramienta construida en MatLab que visualiza los gráficos de transferencia y fase en relación con las posiciones de los ceros y polos en el plano Z. 

Inspirado en esto, decidí recrear esta herramienta en Python. Aprovechando mi experiencia con la biblioteca PyGame, logré construir una aplicación en tiempo real que permite mover los polos y ceros, permitiendo a los usuarios ver cómo cambia la función de transferencia en tiempo real.

## Cómo Funciona
Primero, mapeo las posiciones de los píxeles en el plano Z a coordenadas de acuerdo con la representación del círculo unitario. Luego, construyo la función de transferencia, donde cada cero $z_{n}$ es un término en el numerador y cada polo $z_{i}$ es un término en el denominador. Con la función de transferencia $H(z)$, puedo graficar tanto el magnitud como el gráfico de fase, que también son representaciones mapeadas de la respuesta normalizada dentro de la aplicación.

$$ 
H(z) = \frac{\sum_{n=0}^{N} (z - z_{n})}{\sum_{i=0}^{N} (z - z_{i})}
$$

Cada fotograma recalcula la función de transferencia. El programa funciona de manera eficiente porque almaceno los ceros y polos en arreglos, lo que permite cálculos más rápidos gracias a numpy, que ya está altamente optimizado. Esto permite visualizar los cambios en tiempo real y proporciona una comprensión más intuitiva del comportamiento del plano Z. El siguiente fragmento de código muestra como se calcula la magnitud y fase utilizando exponenciales complejas.

```python
def e(w, root):
    return (np.exp(1j*w) - root)

def transfer_function(zeros, poles):
    w = np.linspace(-np.pi, np.pi, RES)

    for zero in zeros:
        num = e(w, zero)

    for pole in poles:
        den = e(w, pole)
    
    H_z = num/den

    mag = np.abs(H_z)
    ang = np.angle(H_z)

    return mag, ang
```
Este proyecto está diseñado como material educativo, proporcionando a los estudiantes una herramienta práctica para comprender mejor las interacciones entre los polos y ceros en el plano Z. No está destinado como una herramienta profesional para el diseño de filtros.

## Funcionalidad
La aplicación ofrece las siguientes características:

- **Mostrar y mover polos/ceros**: Los usuarios pueden seleccionar y mover los polos y ceros en el plano Z. Cuando la opción de simetría está activa, todos los polos y ceros seleccionados o movidos se colocan de manera simétrica respecto al eje imaginario.

- **Orden**: Los usuarios pueden ajustar el orden de los polos y ceros desplazando la rueda del mouse. El orden puede incrementarse o disminuirse, con soporte hasta un orden de 4. El color de cada polo o cero cambia según su orden.

- **Información**: Al pasar el cursor sobre un polo o cero, se muestra información sobre su posición, simetría y orden.

- **Zoom**: El usuario puede acercar o alejar el plano Z usando los botones de más y menos.

- **Eliminar**: El ícono de la papelera elimina todos los polos y ceros del plano. Los usuarios también pueden eliminar polos o ceros individuales haciendo clic derecho sobre ellos.

- **Gráfico de Magnitud**: El espectro de magnitud mostrado en la aplicación está normalizado. Esta decisión asegura que el enfoque permanezca en la forma de la magnitud, haciendo que el gráfico sea visualmente significativo para los usuarios. Sin embargo, no captura la diferencia en los valores máximos.

- **Gráfico de Fase**: La fase se muestra sin envolver entre $-\pi$ y $\pi$.

## Demo
Aquí tienes una demostración rápida de la aplicación en acción:

{{< vimeo 1045497647 >}}

El código fuente de este proyecto se encuentra en este [repositorio](https://github.com/MatiasDiBernardo/Z-Plane_Visualizer).
