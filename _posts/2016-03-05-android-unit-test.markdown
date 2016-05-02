---
layout: post
title:  "Introducción a los Test Unitarios en Android"
date:   2016-03-05 19:46:15 +0100
categories: Android Test
comments: true
---
Crearemos un nuevo proyecto en Android Studio, **_File > New > New Project..._** con el nombre **TestingExample**  y dejando las demás opciones por defecto.

Antes de empezar a escribir test unitarios debemos comprobar que tenemos creado el directorio `src/test/java` viendo el proyecto con la perspectiva Project, aquí se incluirán los test unitarios. Bajo la ruta `src/androidTest/java` se crearán los test de instrumentación, que requieren ser ejecutados en un terminal físico o en un emulador.
![]({{ site.url }}/images/testproject.png){: .center-image }
Comprobamos también que `build.gradle Module:app` tiene las siguientes dependencias, si no es así, debemos incluirlas y sincronizar Gradle:

{% highlight groovy %}
  dependencies {
      compile fileTree(dir: 'libs', include: ['*.jar'])
      compile 'com.android.support:appcompat-v7:23.1.1'
      testCompile 'junit:junit:4.12'
  }
{% endhighlight %}

Una vez configurado el entorno, ya podemos empezar a escribir nuestros test, pero antes necesitamos tener alguna clase que testear, por lo que vamos a crear la clase `Concatenator` en `src/java`
![]({{ site.url }}/images/concatenator.png){: .center-image }
Esta clase tendrá un método que servirá para concatenar dos textos, por el momento este método devolverá null.

{% highlight java %}
public class Concatenator {

    public String concatenate(String firstText , String secondText) {
        return "";
    }
}
{% endhighlight %}

Ahora crearemos nuestra clase de test haciendo click sobre la clase que acabamos de escribir y pulsando `ctrl+shift+t` o haciendo click derecho sobre el editor de texto y seleccionando **_Go To > Test > Create New Test..._**, esto nos permitirá crear una nueva clase de test para `Concatenator`. En esta clase de test escribiremos un test que pruebe la funcionalidad del método `concatenate()` .

![]({{ site.url }}/images/concatenatorTest.png){: .center-image }

Elegimos la ruta de destino de nuestra nueva clase de test: `app/src/test/java/com/example/testingexample/`

![]({{ site.url }}/images/concatenatorTestDestination.png){: .center-image }

Nuestra clase de test `ConcatenatorTest` quedará de la siguiente forma:

{% highlight java %}
import org.junit.Test;
import static org.junit.Assert.*;

public class ConcatenatorTest {

    private Concatenator mConcatenator;

    @Before
    public void setUp() throws Exception {
        mConcatenator = new Concatenator();
    }

    @Test
    public void testConcatenate() throws Exception {
        String result = mConcatenator.concatenate("Hello", " World");
        assertEquals("Hello World", result);
    }
}
{% endhighlight %}

Para ejecutar nuestro test hacemos click derecho sobre `CalculatorTest` y seleccionamos **_Run > CalculatorTest_**, nuestro test fallará ya que todavía nos queda por implementar la lógica del método `concatenate()`:

  {% highlight java %}
  public class Concatenator {

      public String concatenate(String firstText , String secondText) {
          return firstText + secondText;
      }
  }
  {% endhighlight %}

  Ahora que ya tenemos implementado nuestro método, volvemos a ejecutar nuestro test y comprobamos que que el resultado es correcto.
![]({{ site.url }}/images/testResult.png){: .center-image }
