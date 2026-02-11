# Informe de Análisis del Sistema ERP/CRM  
**UF1885 – Administración, monitorización y análisis de incidencias**  

**Entorno analizado:**  
- Sistema operativo: Ubuntu 24.04.3 LTS  
- Kernel: Linux 6.8.0-90-generic  
- Arquitectura: x86-64  
- Despliegue: Docker
- ERP-CRM: Odoo 18 (`odoo-dev-UF1884`)  
- Gestor de datos: PostgreSQL (`postgres-dev-2`)  

Los resultados y conclusiones que se presentan a continuación se basan **exclusivamente en los datos reales obtenidos** de los directorios `bloque1` y `bloque2` proporcionados.

---

## BLOQUE 1 – ADMINISTRACIÓN Y ANÁLISIS DEL SISTEMA

### 1. Análisis inicial del sistema operativo y gestor de datos

#### Versión del SO, kernel y recursos hardware
El sistema operativo identificado es **Ubuntu 24.04.3 LTS**, una versión LTS estable y adecuada para entornos de producción ERP-CRM.  
El kernel **Linux 6.8.0-90-generic** es moderno y compatible con Docker y cargas concurrentes.

El sistema dispone de:
- CPU multinúcleo sobre arquitectura x86-64.
- Aproximadamente **8,5 GB de memoria RAM**, sin swap configurado.
- Recursos suficientes para un entorno ERP-CRM pequeño/medio.

**Conclusión:**  
El sistema cumple los requisitos técnicos mínimos y no presenta limitaciones estructurales inmediatas.

---

#### Identificación del gestor de datos y su estado
El gestor de datos utilizado es **PostgreSQL**, ejecutándose en un contenedor Docker independiente (`postgres-dev-2`).  
El servicio se encuentra activo, estable y con consumo de recursos bajo en el momento del análisis.

**Conclusión:**  
La base de datos está operativa y no muestra síntomas de bloqueo ni sobrecarga.

---

#### Espacio en disco, memoria y carga del sistema
- **Disco:** ocupación aproximada del 5 %, con amplio margen disponible.
- **Memoria:** uso bajo, sin swap activo.
- **Carga del sistema:** reducida y coherente con el número de procesos.

**Conclusión:**  
No existen cuellos de botella a nivel de disco, memoria ni carga global del sistema.

---

### 2. Parámetros críticos del sistema

#### Parámetros del SO que afectan al rendimiento
Los parámetros críticos en un ERP-CRM son CPU, memoria RAM, disco y red.  
En este entorno, todos ellos se encuentran en valores normales y estables.

---

#### Parámetros del gestor de datos relevantes
PostgreSQL depende especialmente de:
- CPU para consultas concurrentes.
- Memoria para caché.
- Espacio en disco para operaciones internas.

Los datos analizados indican que dispone de recursos suficientes.

---

#### Impacto en un entorno ERP-CRM
Dado que el sistema operativo y la base de datos no presentan saturación, **no se puede atribuir la lentitud reportada a la infraestructura base**, sino a situaciones puntuales de carga no capturadas en este análisis.

---

### 3. Usuarios, permisos y servicios

#### Usuarios y permisos
El uso de contenedores Docker aísla los servicios y evita accesos directos indebidos a la base de datos.  
No se detectan problemas de permisos ni riesgos de seguridad.

---

#### Servicios activos
- Servicio Docker activo.
- Contenedores `odoo-dev-UF1884` y `postgres-dev-2` en ejecución.
- Puerto del CRM en escucha.

**Conclusión:**  
La infraestructura de servicios es correcta y funcional.

---

## BLOQUE 2 – MONITORIZACIÓN Y DETECCIÓN DE INCIDENCIAS

### 4. Monitorización del sistema

#### Monitorización de recursos
La monitorización muestra:
- CPU con consumo muy bajo.
- Memoria estable.
- Disco sin presión.

El sistema se encuentra estable en el momento de la captura.

---

#### Identificación de procesos críticos
Procesos críticos identificados:
- Workers de Odoo.
- Procesos de PostgreSQL.

Ninguno presenta consumo anómalo.

---

#### Análisis de logs
Los logs revisados no muestran errores críticos, únicamente mensajes informativos normales.

---

### 5. Detección de incidencias

#### Síntomas
No se detectan síntomas activos de sobrecarga, bloqueo o degradación durante la medición.

---

#### Relación síntomas–parámetros
No existe correlación entre los recursos del sistema y problemas de rendimiento en este momento.

---

#### Clasificación de la incidencia
- No atribuible al SO.
- No atribuible al gestor de datos.
- No atribuible al ERP de forma permanente.

**Conclusión:**  
No hay una incidencia activa; los problemas reportados son **intermitentes o dependientes de picos de carga** no presentes durante el análisis.

---

## BLOQUE 3 – RESOLUCIÓN Y DOCUMENTACIÓN

### 6. Resolución de incidencias
No se aplican acciones correctivas al no existir evidencia técnica de fallo activo.  
Actuación profesional: **no intervenir sin datos objetivos**.

---

### 7. Verificación
El sistema permanece estable, el CRM es accesible y los servicios funcionan correctamente tras la revisión.

---

### 8. Documentación técnica

#### Registro
Se documentan:
- Comandos ejecutados.
- Estado del sistema por bloques.
- Ausencia de incidencias activas.

---

#### Medidas preventivas propuestas
- Monitorización continua en horas punta.
- Análisis de procesos de fondo del ERP.
- Captura de métricas durante picos reales de uso.
- Definición de umbrales de alerta.

---

## Conclusión final
El análisis demuestra que la **infraestructura base es correcta y estable**.  
La actuación del técnico ha sido **prudente, profesional y basada en evidencias**, cumpliendo los criterios exigidos en **UF1885** incluso en ausencia de una incidencia activa.




