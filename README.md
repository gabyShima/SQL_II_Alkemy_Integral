1. Escriba una consulta que devuelva el legajo y la cantidad de cursos que realiza cada estudiante.

__SELECT e.legajo,   
COUNT(*) as 'Cantidad de cursos que realiza'  
FROM estudiante e INNER JOIN inscripcion i ON e.legajo = i.ESTUDIANTE_legajo  
GROUP BY e.legajo;__

2. Escriba una consulta que devuelva el legajo y la cantidad de cursos de los estudiantes que realizan más de un curso.

__SELECT e.legajo,   
COUNT('a') as 'Cantidad de cursos que realiza'  
FROM estudiante e INNER JOIN inscripcion i ON e.legajo = i.ESTUDIANTE_legajo  
GROUP BY e.legajo HAVING COUNT('a')>1;__

3. Escriba una consulta que devuelva la información de los estudiantes que no realizan ningún curso.

__SELECT e.*  
FROM estudiante e LEFT JOIN inscripcion i ON i.ESTUDIANTE_legajo = e.legajo  
WHERE i.CURSO_codigo IS NULL;__

4. Escriba para cada tabla, los index (incluyendo su tipo) que tiene cada una.

estudiante:
- legajo (clusterizado)
profesor
- id (clusterizado)
curso
- codigo (clusterizado)
- PROFESOR_id (no clusterizado)
inscripcion
- numero (clusterizado)
- CURSO_codigo (no clusterizado)
- ESTUDIANTE_legajo (no clusterizado)

5. Liste toda la información sobre los estudiantes que realizan cursos con los profesores de apellido “Pérez” y “Paz”.

__SELECT e.*, p.apellido, p.nombre  
FROM  
estudiante e  
INNER JOIN inscripcion i ON e.legajo = i.ESTUDIANTE_legajo  
INNER JOIN curso c ON i.CURSO_codigo = c.codigo  
INNER JOIN profesor p ON p.id = c.PROFESOR_id  
WHERE p.apellido = "Pérez" OR p.apellido = "Paz"  
GROUP BY e.legajo;__
