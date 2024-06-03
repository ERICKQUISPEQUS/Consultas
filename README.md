## TAREA 11
#### Ejercicios Propuestos 
##### 1. ¿Cuáles son los identificadores y nombres de todos los proyectos existentes en la empresa?
SELECT IDProyecto, NombreProyecto
FROM Proyecto;
##### 2. ¿Cuáles son los proyectos que se desarrollan en 'CHICAGO'?
SELECT IDProyecto, NombreProyecto
FROM Proyecto
WHERE Ubicacion = 'CHICAGO';
##### 3. ¿Cuáles son los proyectos que pertenecen al departamento con identificador 2?
SELECT IDProyecto, NombreProyecto
FROM Proyecto
WHERE IDDepartamento = 2;
##### 4. ¿Cuáles son los nombres y ubicaciones de los proyectos junto con los nombres de sus departamentos asociados?
SELECT p.NombreProyecto, p.Ubicacion, d.NombreDepartamento
FROM Proyecto p
JOIN Departamento d ON p.IDDepartamento = d.IDDepartamento;
##### 5. ¿Qué empleados están asignados al proyecto identificado con el número 4, y cuáles son sus nombres?
SELECT e.IDEmpleado, e.NombreEmpleado
FROM EmpleadoProyecto ep
JOIN Empleado e ON ep.IDEmpleado = e.IDEmpleado
WHERE ep.IDProyecto = 4;
##### 6. ¿En qué proyectos está participando el empleado con el identificador 4, y cuáles son los nombres de esos proyectos?
SELECT p.IDProyecto, p.NombreProyecto
FROM EmpleadoProyecto ep
JOIN Proyecto p ON ep.IDProyecto = p.IDProyecto
WHERE ep.IDEmpleado = 4;
##### 7. ¿Cuántas horas han trabajado en total los empleados en el proyecto con identificador 2?
SELECT SUM(HorasTrabajadas) AS TotalHoras
FROM EmpleadoProyecto
WHERE IDProyecto = 2;
##### 8. ¿Cuáles son los empleados que han trabajado más de 10 horas en el proyecto con identificador 2?
SELECT e.IDEmpleado, e.NombreEmpleado
FROM EmpleadoProyecto ep
JOIN Empleado e ON ep.IDEmpleado = e.IDEmpleado
WHERE ep.IDProyecto = 2
  AND ep.HorasTrabajadas > 10;
##### 9. ¿Cuál es el total de horas trabajadas por cada empleado en todos los proyectos?
SELECT e.IDEmpleado, e.NombreEmpleado, SUM(ep.HorasTrabajadas) AS TotalHoras
FROM Empleado e
JOIN EmpleadoProyecto ep ON e.IDEmpleado = ep.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado;
##### 10. ¿Cuáles son los empleados que trabajan en más de un proyecto?
SELECT e.IDEmpleado, e.NombreEmpleado, COUNT(ep.IDProyecto) AS NumeroProyectos
FROM Empleado e
JOIN EmpleadoProyecto ep ON e.IDEmpleado = ep.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING COUNT(ep.IDProyecto) > 1;
##### 11. ¿Cuáles son los empleados que han trabajado más de 30 horas en total en todos los proyectos?
SELECT e.IDEmpleado, e.NombreEmpleado, SUM(ep.HorasTrabajadas) AS TotalHoras
FROM Empleado e
JOIN EmpleadoProyecto ep ON e.IDEmpleado = ep.IDEmpleado
GROUP BY e.IDEmpleado, e.NombreEmpleado
HAVING SUM(ep.HorasTrabajadas) > 30;
##### 12. ¿Cuál es el promedio de horas trabajadas por proyecto?
SELECT p.IDProyecto, p.NombreProyecto, AVG(ep.HorasTrabajadas) AS HorasPromedio
FROM Proyecto p
JOIN EmpleadoProyecto ep ON p.IDProyecto = ep.IDProyecto
GROUP BY p.IDProyecto, p.NombreProyecto;
