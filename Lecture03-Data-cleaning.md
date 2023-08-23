

### Ejemplo 1: Valores faltantes
**Datos sucios**:
```python
data = {
    'Nombre': ['Ana', 'Juan', 'Miguel', None],
    'Edad': [25, 31, None, 28],
}
```

**Código para limpiar**:
```python
import pandas as pd

df = pd.DataFrame(data)
df.fillna('Desconocido', inplace=True)
```

### Ejemplo 2: Texto con espacios al inicio o al final
**Datos sucios**:
```python
data = {
    'Nombre': [' Ana ', 'Juan ', ' Miguel'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Nombre'] = df['Nombre'].str.strip()
```

### Ejemplo 3: Números en formato texto con comas
**Datos sucios**:
```python
data = {
    'Salario': ['1,200', '2,500', '3,300'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Salario'] = df['Salario'].str.replace(',', '').astype(float)
```

### Ejemplo 4: Fechas en formatos inconsistentes
**Datos sucios**:
```python
data = {
    'Fecha': ['01/02/2020', '2020-03-04', 'May 5, 2020'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Fecha'] = pd.to_datetime(df['Fecha'])
```

### Ejemplo 5: Datos duplicados
**Datos sucios**:
```python
data = {
    'Nombre': ['Ana', 'Ana', 'Juan'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df.drop_duplicates(inplace=True)
```

### Ejemplo 6: Caracteres especiales en texto
**Datos sucios**:
```python
data = {
    'Nombre': ['An@', 'Ju#an', '*Miguel'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Nombre'] = df['Nombre'].str.replace('[^a-zA-Z ]', '')
```

### Ejemplo 7: Texto en diferentes casos (mayúsculas/minúsculas)
**Datos sucios**:
```python
data = {
    'Nombre': ['ANA', 'juan', 'MiGuel'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Nombre'] = df['Nombre'].str.title()
```

### Ejemplo 8: Datos booleanos en formato texto
**Datos sucios**:
```python
data = {
    'Tiene mascota': ['sí', 'no', 'Sí', 'NO'],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Tiene mascota'] = df['Tiene mascota'].str.lower().map({'sí': True, 'no': False})
```

### Ejemplo 9: Valores erróneos en una columna
**Datos sucios**:
```python
data = {
    'Edad': [25, 150, 31, -5],
}
```

**Código para limpiar**:
```python
df = pd.DataFrame(data)
df['Edad'] = df['Edad'].apply(lambda x: x if 0 < x < 120 else None)
```

### Ejemplo 10: Emails mal formateados
**Datos sucios**:
```python
data = {
    'Email': ['ana.gmail.com', 'juan@yahoo', 'miguel@outlook.com'],
}
```

**Código para limpiar**:
```python
import re

df = pd.DataFrame(data)
pattern = '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}'
df['Email'] = df['Email'].apply(lambda x: x if re.match(pattern, x) else None)
```

Es importante notar que la limpieza de datos es un proceso iterativo y, en muchos casos, depende del contexto y las necesidades específicas del análisis. Estos son solo ejemplos básicos, y podría haber situaciones más complejas que requieran soluciones personalizadas.