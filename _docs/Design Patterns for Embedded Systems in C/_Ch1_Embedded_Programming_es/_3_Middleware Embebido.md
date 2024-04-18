# Middleware embebido

El middleware es un software que conecta componentes de software de alguna manera. El término middleware se remonta a la Conferencia de Ingeniería de Software de la OTAN de 1968. Al igual que los sistemas operativos, existe soporte comercial para el middleware, pero en sistemas pequeños puede desarrollarse como parte del software de aplicación. Los middlewares más comunes para sistemas embebidos y en tiempo real incluyen la Arquitectura de agente de solicitud de objetos comunes (CORBA) y sus numerosas variantes, y el Servicio de distribución de datos (DDS). Ambas arquitecturas de middleware se basan en estándares publicados por Object Management Group (OMG). En el caso de CORBA, existen muchas variantes de estándares especializados entre los que elegir, incluidos RealTime CORBA, Embedded CORBA y Mínimo CORBA.
Como se puede imaginar, el middleware es apropiado para aplicaciones integradas de mayor escala: aquellas que constan de múltiples componentes de software o aplicaciones que pueden distribuirse en múltiples procesadores y redes. En particular, cuando los componentes van a ser desarrollados por diferentes organizaciones, el sistema será ampliado por diferentes organizaciones, o cuando el sistema tiene una vida particularmente larga, el uso de middleware estándar proporciona beneficios significativos al desarrollador. Estas arquitecturas de middleware, al igual que los sistemas operativos, son colecciones integradas de patrones de diseño, como Proxy, Data Bus y Broker Pattern.

## Codesarrollo con Hardware
Muchos proyectos integrados implican el desarrollo de hardware electrónico y mecánico simultáneamente con el software. Esto introduce desafíos especiales para el desarrollador de software, que debe desarrollar software únicamente sobre la base de especificaciones de diseño previo de cómo se pretende que funcione el hardware. Con demasiada frecuencia, esas especificaciones no son más que nociones de funcionalidad, lo que hace imposible crear el software correcto hasta que finalmente se entregue el hardware. Cualquier error en la programación del hardware induce directamente errores en la programación del software, por lo que los desarrolladores de software “se llevan la culpa”. Recuerdo haber trabajado en contra de una especificación de hardware para un sistema de telemetría en la década de 1980.
En este sistema, se suponía que el hardware codificaría bits por pulsos: ocho pulsos para un bit “0” y 15 pulsos para un bit “1”, con un período de tiempo específico entre pulsos y un tiempo específico más largo entre bits. Escribí el software basándose en esa especificación pero, para mi sorpresa8, cuando llegó el hardware real sólo pude comunicarme de forma intermitente con el dispositivo.

A pesar de una depuración intensiva, no pude descubrir dónde estaba fallando el software, claro está, hasta que saqué el osciloscopio. Con el osciloscopio pude ver que cuando el software colocaba un bit “0”, la bobina pulsaba entre seis y 12 veces. Para un bit "1", pulsó entre 10 y 18 veces (tenga en cuenta que los rangos para los bits "0" y "1" en realidad se superponen). La solución fue escribir un algoritmo predictor-corrector que estimara las probabilidades de error de bits y las corrigiera sobre la marcha en función del CRC del mensaje, los valores de los bits y sus certezas. ¡El software era ciertamente más complejo de lo que esperaba! Así es la vida del programador integrado.
Aunque gran parte de los problemas de integración de hardware y software pueden eliminarse con buenas especificaciones y la entrega temprana de prototipos de hardware, gran parte de ellos no es posible. Una de las verdades del desarrollo de software es que la reingeniería es una consecuencia necesaria del codesarrollo.
Los métodos ágiles abordan esta preocupación de dos maneras diferentes9. En primer lugar, con los métodos ágiles, el software se desarrolla constantemente durante todo el ciclo de vida del software. Cada día, se escribe, depura, prueba unitariamente y entrega software. Y cada día, diferentes unidades de software se integran y prueban como un todo coherente en un flujo de trabajo conocido como integración continua. Esto permite detectar los defectos del software lo antes posible. Esta integración puede (y debe) incluir también el hardware inicial.