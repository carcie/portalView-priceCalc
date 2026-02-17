# Marco Matemático para Costos de Proyectos y Cotizaciones

## 1. Objetivo
El propósito de este documento es definir los marcos matemáticos utilizados para calcular los costos de proyectos y generar cotizaciones para clientes. Este marco distingue entre el Estándar de Ventas (Modelo A), utilizado para una fijación de precios y cotización segura, y el Estándar Operativo (Modelo B), utilizado para el seguimiento interno de pérdidas y ganancias (P&G) y la gestión de capacidad.

## 2. Definiciones y Parámetros Globales
Las siguientes variables dictan la estructura de costos para todos los proyectos.

### 2.1 Constantes Anuales Fijas ($F$)
Estos costos se incurren independientemente del volumen del proyecto y deben ser cubiertos por el margen bruto del portafolio.

- Salario ($S$): $42,000 / año ($3,500/mes)
- Software - MS Project ($M$): $360 / año ($30/mes)
- Software - Autodesk ($A$): Variable ($925 – $3,675 / año). Nota: Solo se requiere una licencia para todo el portafolio.
- Amortización de Hardware ($E$): $1,000 / año (Basado en $1,500 CAPEX amortizado en 18 meses).

Base de Costo Fijo Total ($F_{base}$):
$$F_{base} = 43,360 + A$$

### 2.2 Parámetros Operativos Variables
- Costo de Bloque Cupix ($C_{block}$): $6,200 por cada 10,000 $m^2$ al año.
- Tarifa de Rastreo de Objetos ($C_{obj}$): $0.50 por objeto (Tarifa única de configuración).
- Costo Base de Visita a Sitio ($V_{base}$): $50 por visita.
- Frecuencia de Visitas: Semanal.

Nota Operativa: Las visitas se realizan preferentemente los viernes después de la jornada laboral, para asegurar una captura de datos óptima sin interferencia humana ni luz artificial.

Cálculo Mensual Promedio: Dado que algunos meses tienen 5 semanas, se utiliza el promedio anual:
$$50 \text{ USD/visita} \times \frac{52 \text{ semanas}}{12 \text{ meses}} \approx 217 \text{ USD/mes}$$

### 2.3 Variables Específicas del Proyecto
Para cualquier proyecto dado $i$:

- $a_i$: Área del proyecto en metros cuadrados ($m^2$).
- $o_i$: Número de objetos rastreados.
- $d_i$: Duración del proyecto en meses.
- $\lambda_i$: Factor de Ubicación (Multiplicador para costos de visita a sitio).
  - $\lambda = 1.0$: Radio local estándar.
  - $\lambda > 1.0$: Acceso remoto/difícil (ej. sitios mineros).

## 3. Modelo A: El Estándar de Ventas (Precios Segregados)
**Caso de Uso:** Cotizaciones a Clientes, Generación de Propuestas.

**Principio:** Cada proyecto se cotiza como si requiriera su propia capacidad independiente. Esto protege al negocio contra desbordamientos de capacidad y asegura que cada cliente contribuya a un bloque completo de licencia.

### 3.1 Fórmula de Cálculo de Costos
El precio piso mínimo ($P_{floor}$) para el Proyecto $i$ se calcula como:

$$P_{floor, i} = \underbrace{(217 \cdot \lambda_i \cdot d_i)}_{\text{Visitas a Sitio (Semanal)}} + \underbrace{(0.50 \cdot o_i)}_{\text{Configuración de Objetos}} + \underbrace{\left( 6,200 \cdot \left\lceil \frac{a_i}{10,000} \right\rceil \right)}_{\text{Licencia Segregada}} + \underbrace{\left( \frac{d_i}{12} \cdot \frac{F_{base}}{N_{target}} \right)}_{\text{Asignación de Gastos Fijos}}$$

Donde $N_{target}$ es el número objetivo de proyectos concurrentes (ej. 3) y el factor 217 representa el costo promedio mensual de visitas semanales.

### 3.2 Implicación Estratégica
Al usar la función techo (redondeo hacia arriba) $\lceil a_i / 10,000 \rceil$ a nivel de proyecto, cobramos al cliente por el bloque completo de capacidad que activan, independientemente de si utilizamos la capacidad restante para otros clientes.

## 4. Modelo B: El Estándar Operativo (Costeo Agregado)
**Caso de Uso:** P&G Interno, Análisis de Margen, Cálculo de Punto de Equilibrio.

**Principio:** Los costos se calculan basándose en la demanda agregada total del portafolio. Esto refleja el flujo de caja real que sale del negocio.

### 4.1 Fórmula de Costo Total del Portafolio
El costo anual real ($C_{actual}$) para gestionar $n$ proyectos activos es:

$$C_{actual} = F_{base} + \underbrace{\left( 6,200 \cdot \left\lceil \frac{\sum_{i=1}^{n} a_i}{10,000} \right\rceil \right)}_{\text{Licencia Agregada}} + \sum_{i=1}^{n} \left( 217 \cdot \lambda_i \cdot d_i + 0.50 \cdot o_i \right)$$

### 4.2 Implicación Estratégica
La función techo se aplica a la suma de todas las áreas ($\sum a_i$). Esto permite al negocio "apilar" proyectos más pequeños en un solo bloque de licencia, creando eficiencia operativa.

## 5. Análisis Comparativo: La Ganancia por "Arbitraje"
La diferencia entre el Precio cobrado (Modelo A) y el Costo incurrido (Modelo B) genera un flujo de ganancias secundario conocido como Arbitraje de Licencias.

### 5.1 Simulación: Portafolio de 30,000 $m^2$
Asumiendo un portafolio de 5 proyectos pequeños ($6,000 m^2$ cada uno):

| Métrica | Modelo A (Cotización Ventas) | Modelo B (Ops Real) | Variación (Ganancia) |
|---------|-------------------------------|----------------------|-----------------------|
| Lógica | 5 Proyectos $\times$ 1 Licencia c/u | 1 Portafolio de $30,000 m^2$ | |
| Matemática | $5 \times \$6,200$ | $3 \times \$6,200$ | |
| Costo Licencia | $31,000 | $18,600 | +$12,400 |

### 5.2 Asignación de Ganancias
El excedente de $12,400 generado en este escenario es ganancia pura derivada de una gestión eficiente de la capacidad. Este excedente subsidia efectivamente:

- El Costo Anual de la Licencia Autodesk ($A$).
- Actualizaciones de Hardware.
- Sobrecostos inesperados por ubicación (variación de $\lambda$).

## 6. Directrices Operativas

### 6.1 Directivas para el Equipo de Ventas
- **Cotizar Siempre Modelo A:** Nunca trasladar los ahorros de la agregación al cliente a menos que sea necesario para ganar una licitación competitiva.
- **Traslado de Tarifa de Objetos:** La Tarifa de Configuración de Objetos ($0.50 \cdot o_i$) es un costo directo "duro". Debe cobrarse por adelantado o amortizarse estrictamente durante el plazo garantizado del contrato.
- **Factor de Ubicación:** Ventas debe confirmar el multiplicador de ubicación del sitio ($\lambda$) con Operaciones antes de finalizar una cotización.

### 6.2 Directivas para el Equipo de Operaciones
- **Monitoreo de Capacidad:** Rastrear el Área Total ($\sum a_i$) mensualmente.
- **Alerta de Umbral:** Alertar a Ventas cuando $\sum a_i$ se acerque a un múltiplo de 10,000 $m^2$ (ej. 9,500 $m^2$, 19,500 $m^2$). Agregar un proyecto pequeño en este umbral activa un costo escalonado de $6,200 en el Modelo B, lo que puede reducir temporalmente los márgenes del portafolio si no se cotiza correctamente.
- **Nivel de Autodesk:** Mantener el nivel de Autodesk viable más bajo hasta que un proyecto requiera específicamente características BIM/Revit ($A > \$925$). Al actualizar, el costo fijo incrementado aplica a todo el portafolio.
