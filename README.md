1. ¿Cómo funciona el algoritmo usando diferentes hiperparámetros?
    Learning rate alto ($LR \ge 0.001$ o $0.1$):
      El modelo diverge de forma instantánea. Como las variables no están escaladas (la superficie está en torno a $10^2$ y el precio en torno a $10^5$), el gradiente de la pendiente $da$ adquiere magnitudes de $10^7$ o superiores. Un paso de aprendizaje grande provoca un salto excesivo
      sobre la curva de pérdida, arrojando valores inf y NaN en las primeras iteraciones.
    Learning rate excesivamente bajo ($LR \le 10^{-7}$ o $10^{-8}$):
      El modelo es matemáticamente estable pero prácticamente inútil sin miles de épocas. En 50 o 100 épocas apenas actualiza la pendiente desde su inicialización en $0.0$, quedando subajustado (underfitting severo).
    Learning rate calibrado ($LR = 0.00001$):
      Permite un descenso continuo y controlado del error cuadrático medio (MSE), reduciendo la pérdida época a época sin oscilaciones caóticas.
2. ¿Con qué hiperparámetros se obtiene el mejor modelo?
    Para este conjunto de datos sin estandarizar, la combinación más equilibrada es:
      learning_rate = 0.00001 ($10^{-5}$)
      epochs = 50 a 100
    Con esta configuración, el algoritmo converge a una pendiente aproximada de a = 1800  –  2100€/m²,lo cual tiene coherencia con el valor medio de mercado por metro cuadrado y minimiza el MAE en torno a los 70.000-80.000€ € en el conjunto de prueba.
3. ¿Hay algún número de épocas a partir del cual el modelo ya no aprende más?
    Sí. Alrededor de las 80–100 épocas (con $LR = 0.00001$), el modelo alcanza la zona de convergencia:
     La variación del gradiente disminuye drásticamente ($\nabla \approx 0$) y el valor de $a$ apenas fluctúa en decimales.
     A partir de ese umbral, incrementar el número de épocas a 500 o 1000 no aporta mejoras reales en el MSE y corre el riesgo de ralentizar la ejecución innecesariamente o derivar en un ligero sobreajuste (overfitting) a la muestra de entrenamiento.
