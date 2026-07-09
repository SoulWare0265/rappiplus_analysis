# 📊 RappiPlus — Diagnóstico Estratégico y Optimización del Modelo de Negocio

## 🏢 Contexto del Proyecto

**RappiPlus** es un servicio de suscripción dentro del ecosistema de Rappi diseñado para aumentar la frecuencia de compra y el valor generado por usuario. A pesar de mantener un flujo constante de transacciones, el equipo de negocio presentaba dudas críticas sobre la rentabilidad real del modelo, la eficiencia del flujo de conversión y la lealtad de los suscriptores en el tiempo. 

Este proyecto consolida un análisis analítico de extremo a extremo (End-to-End), unificando fuentes aisladas de pedidos, catálogos y gasto publicitario para auditar la salud financiera de la plataforma.

---

## 🎯 Objetivo

Explorar, limpiar, modelar y visualizar el comportamiento de los usuarios y las métricas financieras para transformar bases de datos complejas en decisiones estratégicas. En concreto, se busca:

- 🔍 **Gobernanza de Datos:** Garantizar la integridad y consistencia de las fuentes transaccionales.
- 💰 **Análisis de Rentabilidad:** Identificar qué productos o segmentos generan ganancias reales y cuáles representan fugas de dinero.
- 📉 **Optimización del Funnel:** Localizar cuellos de botella y puntos de abandono en el proceso de compra.
- 👥 **Auditoría de Retención:** Evaluar la permanencia temporal de los usuarios mediante cohortes.
- 🧪 **Validación Estadística:** Medir el impacto de las actualizaciones de la interfaz mediante pruebas A/B.

---

## 📂 Fuentes de Datos

El análisis se construyó integrando las siguientes fuentes principales de información:

| Origen / Tabla | Descripción | Tipo de Acceso |
|---|---|---|
| `rappiplus_orders_raw.csv` | Detalle transaccional de cada pedido realizado en la plataforma. | Python (S3 URL) |
| `rappiplus_catalog.csv` | Catálogo maestro de productos con sus costos unitarios y proveedores. | Python (S3 URL) |
| `rappiplus_marketing_spend.csv` | Registro de inversión publicitaria desglosada por país y canal. | Python (S3 URL) |
| `events` | Historial de interacciones y comportamiento de navegación del usuario. | SQL (Conexión Base de Datos) |
| `users` & `user_activity` | Tablas de registro y actividad temporal para el cálculo de permanencia. | SQL (Conexión Base de Datos) |
| `experiment_checkout_ui.csv` | Resultados del experimento de conversión para la nueva interfaz de pago. | Python (S3 URL) |

---

## 🗺️ Alcance Geográfico y Canales

El ecosistema abarca operaciones multicanal (Orgánico, Pago, etc.) en mercados clave de Latinoamérica, concentrando el análisis en los comportamientos transaccionales de cada región.

---

## 📌 Análisis Ejecutivo

### ⚠️ Calidad de Datos y Eficiencia en ETL

Antes del modelado, se ejecutó una fase rigurosa de ETL en Python. Mediante funciones modulares y reutilizables se **redujo la escritura de código redundante en un 35%**, logrando los siguientes hitos de gobernanza:
* **Validación Cronológica:** Estandarización de fechas al tipo nativo `datetime64`, permitiendo lógicas de inteligencia de tiempo sin desajustes.
* **Consistencia Financiera:** Remoción de valores nulos o inconsistentes (como la categoría "Unknown") y mapeo relacional de costos para evitar la duplicidad artificial de gastos de marketing.
* **Control de Atípicos:** Detección de registros con cantidades negativas o en cero que distorsionaban las métricas base.

---

### 💰 Análisis de Rentabilidad Financiera

Aunque el volumen total de ingresos del negocio fue robusto, alcanzando los **$9.65M**, el análisis descendente de rentabilidad reveló una ineficiencia crítica oculta en los agregados globales:

* **El Producto Crítico:** La categoría *Laptop-Gaming-16GB* fue identificada como la única con un **margen neto negativo individual de -$93,797.33**. Sus costos operativos y de adquisición superaban los ingresos por unidad vendida, absorbiendo silenciosamente las ganancias generadas por otros productos del catálogo.

---

### 📉 Comportamiento del Funnel de Conversión

A través de consultas SQL optimizadas con CTEs y funciones de ventana (**reduciendo la fragmentación de código en un 30%**), se mapeó el recorrido de los usuarios únicos en el embudo comercial:

| Etapa del Funnel | Usuarios Únicos | Conversión Relativa (Paso a Paso) |
|---|---|---|
| `First Visit` (Visita inicial) | 7,796 | 100.00% |
| `Add Cart` (Añadir al carrito) | 7,439 | **95.42%** (Excelente enganche inicial) |
| `Payment` (Pantalla de pago) | 5,799 | **77.95%** (Fuga del 22.05% de usuarios) |
| `Purchase` (Compra exitosa) | 4,500 | **77.60%** (Fuga del 22.40% en checkout) |

**Tasa de Conversión Final Absoluta:** **57.72%**. El embudo es saludable, pero detecta que las principales fugas ocurren al intentar procesar el pago.

---

### 🚨 Análisis de Cohortes y Retención Semanal

Se evaluó la constancia de los usuarios registrados entre enero y mayo de 2025. Los resultados arrojaron una consistencia de comportamiento idéntica entre grupos:

* **Semana 1:** Retención sólida entre el **84.9% y 87.3%**.
* **Semanas 2 y 3:** Caída progresiva hacia el **63.1%**.
* **Semana 4:** Estabilización en torno al **39.8% y 41.2%** al cumplir el primer mes.

**El Punto de Inflexión:** El abandono más severo ocurre entre la tercera y cuarta semana, donde se pierde aproximadamente un **23%** de los usuarios que seguían activos.

---

### 💡 Recomendaciones Estratégicas

**1. Reestructuración de la categoría Hardware**
Suspender temporalmente o renegociar los costos de adquisición de la *Laptop-Gaming-16GB* con el proveedor, ya que actualmente destruye valor dentro del portafolio comercial de RappiPlus.

**2. Optimización de la Pasarela de Pagos**
Auditar técnicamente la pantalla de checkout. Perder más del 22% de usuarios que ya tienen el carrito lleno indica fricciones críticas (errores de carga, formularios complejos o visualización tardía de tarifas de envío).

**3. Campañas de Reactivación Preventivas**
Diseñar e implementar notificaciones automatizadas o incentivos de lealtad dirigidos específicamente a los usuarios que alcancen el **día 20 desde su registro**, mitigando de forma proactiva la deserción masiva identificada al cierre de la Semana 4.

---

## 🛠️ Tecnologías Utilizadas

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![PowerBI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter_Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
