# Unit 4: Causal Inference With Limited Data

## 1) Fundamento y relevancia
- **Problema central:** nunca podemos observar el contrafactual (cómo le habría ido a la misma persona con otros atributos protegidos).  
- **Reto:** el marco causal es sólido en teoría, pero en la práctica faltan datos y causalidad perfecta.  
- **Objetivo:** aprender métodos prácticos para **aproximar efectos causales y equidad contrafactual** con datos limitados.

---

## 2) Conceptos clave
### El reto fundamental
- No se pueden observar mundos contradictorios → necesitamos inferencia.  
- “Ladder of causation” (Pearl):  
  1. Asociación  
  2. Intervención  
  3. Contrafactual  

### Métodos observacionales
- **Matching / Propensity scores** (Rubin, 2006) → simular aleatorización emparejando casos similares.  
- **Instrumental Variables (IV)** (Angrist & Pischke, 2008) → usar variables externas que afectan A pero no Y directamente.  
- **Regression Discontinuity** (Imbens & Lemieux, 2008) → comparar justo en umbrales.  
- **Difference-in-Differences** (Card & Krueger, 1994) → comparar grupos en cambios de política.

### Sensibilidad a confusión no medida
- Nunca observamos todos los confusores → usar **sensitivity analysis**.  
- **E-value (VanderWeele & Ding, 2017):** qué tan fuerte tendría que ser un confusor no medido para anular el efecto.

### Descubrimiento causal
- Inferir estructura causal directamente de datos.  
- Métodos: **PC algorithm** (independencias), **score-based** (fit+simplicidad), **FCI** (manejo de latentes).  
- Puede revelar proxys o mecanismos inesperados.

### Adaptación entre dominios
- **Transportabilidad** (Bareinboim & Pearl, 2016): trasladar inferencias causales de un contexto a otro.  
- Ejemplo: un modelo justo en un país puede no serlo en otro (cambian causalidades).  
- Se usan *selection diagrams* para razonar sobre qué se puede transferir.

### Interseccionalidad
- Datos aún más escasos en intersecciones (p. ej. mujeres mayores migrantes).  
- Usar **Bayesian hierarchical models** (Yang et al., 2020) para “prestar fuerza” estadística entre grupos relacionados.  
- Transparencia: comunicar incertidumbre explícita.

---

## 3) Marco práctico
1. **Inventario causal** → listar lo que sabemos (expertos, literatura).  
2. **Elegir método** → matching, IV, discontinuidad, diff-in-diff.  
3. **Cuantificar incertidumbre** → sensibilidad (E-value, bounds).  
4. **Documentar supuestos** → claridad sobre lo que se da por hecho.  
5. **Combinar métodos** → usar varios para comprobar consistencia.  

---

## 4) Retos típicos
- **Equilibrar conocimiento experto y data-driven.**  
- **Gestión de expectativas:** no prometer certezas donde hay incertidumbre.  
- **Comunicación de incertidumbre** → usar rangos y no solo estimaciones puntuales.  

---

## 5) Evaluación
- **Consistencia entre métodos** → si coinciden, mayor confianza.  
- **Validación predictiva** → comparar predicciones bajo intervenciones/naturales.  
- **Monitoreo continuo** → causalidad cambia en el tiempo y en contextos.

---

## 6) Caso: algoritmo de riesgo penal
- **Problema:** predicciones más altas para personas negras.  
- **Métodos aplicados:** matching, IV (jueces asignados al azar), diff-in-diff tras reformas.  
- **Hallazgos:** 30–40% de disparidad atribuida a discriminación o proxys.  
- **Interseccionalidad:** especialmente grave en jóvenes hombres negros pobres.  
- **Lecciones:**  
  - Usar **múltiples métodos**.  
  - Incorporar **análisis de sensibilidad**.  
  - Integrar **conocimiento experto**.  
  - Documentar **incertidumbre y trade-offs**.

---

##
