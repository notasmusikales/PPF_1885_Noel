# E2 UF1885 - Detección, análisis y resolución de incidencias (ERP-CRM)

**Alumno:** Gonzalez, Noel  
**Fecha:** 2026-02-04  
**Entorno:** Ubuntu Server + Docker  
**Contenedores:** odoo-dev-UF1884 (CRM) | postgres-dev-2 (BD)

---

## 1. Análisis inicial del sistema y parámetros de rendimiento
### 1.1 Servicios de acceso al CRM
- Descripción: 
	- Acceso al ERP/CRM (aplicacion web): contenedor odoo
	- El servicio de base de datos: contenedor postgres-dev-2 (PostgrSQL 16)
	- Servicio de publicación de puerto / acceso web: Docker publica 8069/tcp
	- Red y DNS del sistema: interfaz la IP 192.168.1.130
	- Acceso administrativo remoto: SSH en 22/tcp para tareas de soporte.  
- Evidencias: evidencias/01_analisis/

### 1.2 Parámetros (CPU / RAM / Disco / Red) y relación con CRM+BD
- CPU ~ 97,7 idle, load average: 0.07, 0.05, 0.74
- Conclusiones: No hay saturación de CPU.

- RAM 10Gi total;       1.0Gi usado;       8.7Gi libre
- Conclusiones: Hay suficiente memoria, no hay presión ahora mismo en la RAM.

- Disco: /dev/sda2   tamaño:254G usado: 9.7G  (5%)
- Conclusiones: Hay suficiente espacio de memoria, no hay problemas de almacenamiento.

## 2. Monitorización de procesos y detección de sobrecarga
### 2.1 Proceso problemático detectado
- Proceso/servicio:
	- Contenedor postgres-dev-2 (servicio PostgreSQL para ERP/CRM)
	- Proceso interno forzado por el sistema: yes > /dev/null & (generador de carga del CPU) 
- Datos y justificación:
	- CPU % (postgres-dev-2): 20078%, indica saturación del docker.
	- Consumo de memoria bajo (67.28MiB / 10.6GiB)
	- Saturacion se produce a nivel del CPU.
- Impacto en el CRM:
	- Lentitud extrema en operaciones que dependen de la base de datos.
	- Usuarios perciben bloqueos y esperas prolongadas.
---

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
- Los usuarios no pueden acceder al CRM.
- La URL del servicio no responde.
### 3.2 Diagnóstico
- Verificar el estado de los contenedores (docker ps)
- El contenedor odoo-dev-UF1885 no se encuentra en ejecución. 
### 3.3 Acción aplicada
- Se procede a reestablecer el servicio del contenedor, arrancando nuevamente.
  ```
  sudo docker start odoo-dev-UF1884
  ```
### 3.4 Verificación
- Verificamos el estado del contenedor.
  ```
  sudo docker ps
  ```
### 3.5 Rollback
- Esta situación consiste en arrancar el contenedor como se indica en la acción anterior.
---
## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada: Simulación de saturación de la memoria RAM mediante la ejecución de procesos que consumen grandes bloques de memoria o mediante herramientas de prueba de estrés de memoria
	 (por ejemplo, stress en Linux, Memory Load en Windows).
- Datos capturados: free -h -> antes y despues de la simulación vmstat 1 5 -> antes y despues de la simulación
- Análisis: Antes de la simulación el sistema disponia de 4.5Gi de memoria libre. 
 Tras la simulación, la memoria utilizada aumentó a 8.4Gi, el sistema no ha llegado a nivel crítico, 
 pero si un escenario de riesgo.;
- Verificación requisitos HW/SW: El sistema cuenta con 10 GiB RAM y no tiene swap configurada. 
 Para entornos ERP/CRM con carga recurrente, esta configuración puede ser insuficiente en picos de consumo de memoria. 
 Aumentar memoria RAM disponible, o configurar swap como medida preventiva
- Registro: La simulación se realizó de forma controlada y reversible sin perdida de datos.

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN): “Docker provides built-in commands to monitor container resource usage, including CPU,
 memory, and network I/O, which helps identify performance bottlenecks.”
- Interpretación (ES): Docker proporciona comandos integrados que permiten monitorizar el uso de recursos de los contenedores, como CPU y memoria,
 lo que facilita la identificación de cuellos de botella que pueden afectar al rendimiento del sistema ERP-CRM.
- Fragmento 2 (EN): “High memory usage can significantly impact application performance, potentially leading 
to slower response times or service instability.”
- Interpretación (ES): El alto uso de memoria puede afectar significativamente el rendimiento de la aplicación, 
lo que podría provocar tiempos de respuesta más lentos o inestabilidad del servicio. 
- Fragmento 3 (EN): “Odoo performance issues are often related to system resource constraints, background jobs,
 or database load, making monitoring and proper sizing essential.”
- Interpretación (ES): Los problemas de rendimiento de Odoo suelen estar relacionados con limitaciones de recursos del sistema, trabajos en segundo plano o carga de la base de datos,
 lo que hace que el monitoreo y el dimensionamiento adecuado sean esenciales.
