# Trabajo Final - Programación Concurrente

## 📋 Descripción
Este proyecto implementa un sistema de procesamiento de imágenes modelado mediante **Redes de Petri** para gestionar la concurrencia. El sistema simula un pipeline de procesamiento que incluye importación, carga, mejora, corte y exportación de imágenes, garantizando sincronización y evitando condiciones de carrera.

## 🎯 Objetivos
- Modelar un sistema concurrente utilizando Redes de Petri
- Implementar políticas de selección de transiciones
- Garantizar el cumplimiento de invariantes estructurales
- Analizar el comportamiento del sistema bajo diferentes configuraciones

## 🏗️ Arquitectura del Sistema

### Componentes Principales

#### Procesos
- **Importador**: Introduce imágenes al sistema
- **Cargador**: Carga imágenes en el contenedor de procesamiento
- **Mejorador**: Realiza ajustes de calidad en dos etapas
- **Cortador**: Recorta imágenes al tamaño definitivo
- **Exportador**: Exporta imágenes fuera del sistema

#### Elementos de Control
- **Monitor**: Gestiona la sincronización y disparo de transiciones
- **Políticas**: Define estrategias de selección de transiciones
- **Colas**: Implementa semáforos para gestión de recursos
- **PetriNet**: Modela el comportamiento dinámico de la red

### Políticas Implementadas

1. **Aleatoria**: Selección aleatoria entre transiciones habilitadas
2. **Balanceada**: Distribución equitativa entre segmentos
3. **Prioritaria**: Priorización de segmentos específicos con porcentaje configurable

## 🔧 Características Técnicas

### Propiedades de la Red de Petri
- **Tipo**: Extended Simple Net
- **Bounded**: True
- **Safe**: False
- **Deadlock**: False
- **Vivacidad**: Garantizada

### Configuración de Tiempos
- **Tareas**: Tiempos de ejecución para cada proceso
- **Transiciones**: Ventanas temporales (α, β) para transiciones temporizadas

## 📊 Resultados Destacados

### Balance de Carga
- Sistema mantiene equilibrio entre ramas bajo política balanceada
- Capacidad de priorizar segmentos específicos (hasta 83.3% para segmento izquierdo)
- Comportamiento consistente en transiciones inmediatas y temporizadas

### Máximo Paralelismo
- **7 hilos activos simultáneos** incluyendo la transición T0
- **6 hilos** considerando solo las plazas de acción

## 🚀 Ejecución

### Configuración
```java
// Ejemplo de configuración con política prioritaria
Monitor monitor = new Monitor(log, Politica.PRIORITARIA, segmento, prioridad, red);
```

### Parámetros Configurables
- Política de selección (ALEATORIA, BALANCEADA, PRIORITARIA)
- Segmento prioritario (IZQUIERDA, DERECHA)
- Nivel de prioridad (0.0 - 1.0)
- Tiempos de tareas y transiciones
- Número de invariantes objetivo

## ✅ Validación

### Tests Unitarios
- Verificación de inicialización de objetos
- Validación de sincronización
- Comprobación de políticas de selección
- Control de disparo de transiciones

### Análisis de Invariantes
- Script Python para validación de invariantes de transición
- Verificación automática de secuencias válidas
- Detección de violaciones de invariantes

## 📈 Análisis de Performance

### Optimización de Tiempos
- **Importador**: 100ms
- **Cargador**: 100ms
- **Mejorador**: 80ms
- **Cortador**: 100ms
- **Exportador**: 50ms

### Ventanas Temporales Óptimas
- Transiciones T7-T10: (200, 400)ms
- Transición T16: (1, 200)ms
- Demás transiciones: (100, 300)ms

## 🎓 Conclusiones

- Las Redes de Petri son efectivas para modelar sistemas concurrentes
- El sistema garantiza sincronización y evita condiciones de carrera
- Las políticas implementadas permiten adaptar el comportamiento del sistema
- La configuración temporal optimizada mejora significativamente el rendimiento
- El modelo es aplicable a escenarios reales de procesamiento concurrente
