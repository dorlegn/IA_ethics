# Unit 3: Counterfactual Fairness Framework

## 1) Fundamento y relevancia
- **Idea central:** Preguntar “¿qué pasaría si esta misma persona tuviera otros atributos protegidos (p. ej., género/etnia) y todo lo demás se mantuviera igual?”  
- **Por qué importa:** Supera métricas puramente estadísticas (DP, EO) porque distingue **correlaciones** de **mecanismos causales** de discriminación.  
- **Base:** Se apoya en los modelos causales de la Unit 2 y los convierte en un **criterio operativo de equidad**.

---

## 2) Conceptos clave
### Definición (Kusner et al., 2017)
Una predicción Ŷ es **contrafácticamente justa** si **no cambia** al intervenir sobre A (atributos protegidos) manteniendo constantes las variables no causadas por A.  
> Intuición: misma persona, mismos méritos → misma predicción, independientemente de A.

### Modelos causales estructurales (SCM)
- Componentes: variables exógenas **U**, endógenas **V**, ecuaciones **F**, distribución **P(U)**.  
- Pipeline de contrafactuales (Pearl): **Abducción → Acción → Predicción**.

### Equidad contrafactual **por rutas** (path-specific)
- No todas las influencias de A son necesariamente injustas.  
- Se **bloquean** rutas designadas como **injustas** y se **preservan** rutas **legítimas** (Chiappa & Isaac, 2019).

### Implementación práctica
- **Fair representation learning** (quitar influencia de A en rutas injustas).  
- **Incorporar restricciones**/regularización de equidad contrafactual en entrenamiento.  
- **Enfoques causales**: estimar efectos y controlar rutas específicas.

### Evaluación
- **Counterfactual Effect Size**: media de cambios entre factual vs. contrafactual.  
- **Violation Rate**: % de casos que cambian más allá de un umbral.  
- **Path-specific metrics**: contribución de rutas concretas a la desigualdad.

### Interseccionalidad
- Consultar combinaciones (p. ej., mujer negra) con **consultas contrafactuales conjuntas** y **análisis por rutas compuestas** (Yang et al., 2020).

---

## 3) Marco práctico (paso a paso)
1. **Formular consultas contrafactuales** (qué cambia, qué se mantiene).  
2. **Clasificar rutas**: justas vs. injustas (con personas expertas y principios éticos).  
3. **Generar contrafactuales** con el SCM y **medir disparidades**.  
4. **Diseñar intervenciones**:
   - Datos: transformar/filtrar características.
   - Modelo: pérdidas con restricciones de equidad, representaciones equitativas.
   - Post-proceso: calibración/ajustes controlados.
5. **Evaluar y iterar** con métricas contrafactuales + rendimiento.

---

## 4) Retos habituales
- **Incertidumbre causal:** usar **modelos alternativos**, **sensibilidad** y **documentar supuestos**.  
- **Trade-offs con accuracy:** preferir **path-specific**, nociones **relajadas** y revisar si la **tarea** está bien planteada.

---

## 5) Encaje en el método (Units 2–5)
- **Unit 2 →** aporta el **DAG/SCM** para generar contrafactuales.  
- **Unit 3 →** define **criterios y métricas** contrafactuales (y por rutas).  
- **Unit 4 →** técnicas de inferencia/estimación bajo limitaciones reales.  
- **Unit 5 →** metodología completa: consultas, clasificación de rutas, intervención y evaluación continua.

---

## 6) Referencias esenciales
- **Kusner et al. (2017)** Counterfactual Fairness.  
- **Pearl (2009)** Causality (SCM, abducción-acción-predicción).  
- **Chiappa (2019); Chiappa & Isaac (2019); Chiappa et al. (2020)** Path-specific & general CF.  
- **Black et al. (2020)** Métricas/Testing contrafactual.  
- **Wu et al. (2019)** Evaluación bajo incertidumbre causal.  
- **Crenshaw (1989)** Interseccionalidad.  
- **Yang et al. (2020)** Causal intersectionality.
