# telecom-analysis-AGD: Análisis de Clientes ConnectaTel

Análisis exploratorio del comportamiento de clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con datos registrados hasta 2024.

##  Objetivo del proyecto

Evaluar cómo usan los clientes los servicios de llamadas y mensajes para:

- Construir un perfil estadístico de los usuarios.
- Detectar problemas de calidad de datos y comportamientos atípicos.
- Segmentar a los clientes por edad y nivel de uso.
- Proponer mejoras a los planes actuales y estrategias de retención.

##  Datasets utilizados

| Archivo | Registros | Descripción |
|---|---|---|
| `plans.csv` | 2 | Planes disponibles (Básico y Premium): precio mensual, minutos, mensajes y GB incluidos, y costo por excedente. |
| `users_latam.csv` | 4,000 | Información de clientes: edad, ciudad, fecha de registro, plan contratado y fecha de cancelación (churn). |
| `usage.csv` | 40,000 | Detalle de uso real: tipo de evento (llamada o mensaje), fecha, duración de llamadas y longitud de mensajes. |

##  Etapas del análisis

1. **Carga y exploración:** revisión de estructura, tipos de datos y primeras filas de cada dataset.
2. **Calidad de datos:** identificación de valores nulos, valores centinela (`-999` en edad, `"?"` en ciudad) y fechas fuera de rango (registros con año 2026).
3. **Limpieza:** reemplazo de centinelas, conversión de fechas y verificación de que los nulos en `duration` y `length` son MAR (dependen del tipo de evento).
4. **Métricas por usuario:** agregación de mensajes, llamadas y minutos por cliente, y unión con la tabla de usuarios.
5. **Distribuciones y outliers:** histogramas por plan, boxplots y cálculo de límites con el método IQR.
6. **Segmentación:** clasificación de clientes por nivel de uso (Bajo, Medio, Alto) y por edad (Joven, Adulto, Adulto Mayor).
7. **Insight ejecutivo:** conclusiones y recomendaciones de negocio.

##  Hallazgos principales

- El 73% de los clientes tiene un uso medio; solo el 7% es de alto uso.
- La edad y el tipo de plan no cambian significativamente los patrones de uso: los clientes Premium consumen prácticamente lo mismo que los Básico.
- El consumo real está muy por debajo de lo que incluyen los planes, lo que sugiere que la oferta está sobredimensionada y que el plan Premium necesita diferenciarse por otros beneficios.

##  Herramientas

- Python 3
- pandas
- seaborn
- matplotlib
- Jupyter Notebook / Google Colab

##  Cómo ejecutar el notebook

### Opción 1: Google Colab (recomendada)

1. Abre [Google Colab](https://colab.research.google.com/).
2. Ve a **Archivo → Abrir cuaderno → GitHub** y pega la URL de este repositorio.
3. Selecciona el notebook del proyecto.
4. Sube los tres archivos CSV desde el panel de archivos (ícono de carpeta a la izquierda).
5. Ajusta las rutas de carga en la celda correspondiente (ver guía de reproducción).
6. Ejecuta todo con **Entorno de ejecución → Ejecutar todas**.

### Opción 2: Local con Jupyter

```bash
git clone https://github.com/<tu-usuario>/telecom-analysis-AGD.git
cd telecom-analysis-AGD
pip install pandas seaborn matplotlib jupyter
jupyter notebook
```

## 🔁 Guía de reproducción

1. Coloca los archivos `plans.csv`, `users_latam.csv` y `usage.csv` en una carpeta `datasets/` dentro del proyecto.
2. El notebook original carga los datos desde `/datasets/`. Si es localmente o en Colab, cambia las rutas según tu ubicación, por ejemplo:

```python
plans = pd.read_csv('datasets/plans.csv')
users = pd.read_csv('datasets/users_latam.csv')
usage = pd.read_csv('datasets/usage.csv')
```

3. Ejecuta las celdas. Las celdas de limpieza modifican los datos, así que si necesitas repetir el proceso, reinicia el kernel y vuelve a ejecutar todo desde el inicio.
4. Si aparece un error como `NameError: name 'user_profile' is not defined`, significa que el kernel se reinició; vuelve a ejecutar todas las celdas anteriores.

## Autor

**Alfredo Dueñas**
[LinkedIn](https://linkedin.com/in/alfredo-gonzalez-dueñas)
