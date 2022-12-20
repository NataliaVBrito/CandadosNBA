>CANDADO A

Consulta para saber la posición:

Teniendo el máximo de asistencias por partido, muestre cuantas veces se logró dicho máximo.

	SELECT COUNT(asistencias_por_partido)
	FROM estadistica
	WHERE asistencias_por_partido = (SELECT MAX(asistencias_por_partido)
					 FROM estadistica);
					 
Consulta para saber la clave:

Muestre la suma total del peso de los jugadores, donde la conferencia sea Este y la posición sea centro o esté comprendida en otras posiciones.

	SELECT SUM(j.peso), e.conferencia, j.posicion  FROM jugador j, equipo e
	WHERE j.nombre_equipo = e.nombre
	AND e.conferencia = "east"
	AND j.posicion LIKE '%C%';
	
>CANDADO B

Consulta para saber la posición:

Muestre la cantidad de jugadores que poseen más asistencias por partidos, que el numero de jugadores que tiene el equipo Heat.

	SELECT COUNT(*), e.asistencias_por_partido FROM jugador j, estadistica e
	WHERE j.codigo = e.jugador
	AND e.asistencias_por_partido > (SELECT COUNT(*)
					 FROM jugador 
					 WHERE nombre_equipo = (SELECT nombre 
					 			FROM equipo WHERE nombre = "Heat"));
								
Consulta para saber la clave:

La clave será igual al conteo de partidos jugados durante las temporadas del año 1999.

	SELECT COUNT(*)
	FROM partido
	WHERE temporada LIKE '%99%';
	
>CANDADO C

Consulta para saber la posición:

La posición del código será igual a la cantidad de jugadores que proceden de Michigan y forman parte de equipos de la conferencia oeste.

	SELECT COUNT(*)
	FROM jugador j, equipo e 
	WHERE j.nombre_equipo = e.nombre 
	AND j.procedencia = "Michigan" 
	AND e.conferencia = "west";
	
Al resultado obtenido lo dividiremos por la cantidad de jugadores cuyo peso es mayor o igual a 195, y a eso le vamos a sumar 0.9945

	SELECT 2/COUNT(*) + 0.9945
	FROM jugador
	WHERE peso >= 195;
	
Consulta para saber la clave:

Para obtener el siguiente código deberás redondear hacia abajo el resultado que se devuelve de sumar: el promedio de puntos por partido, el conteo de asistencias por partido, y la suma de tapones por partido.
Además, este resultado debe ser, donde la división sea central

	SELECT FLOOR(AVG(e.puntos_por_partido) + COUNT(e.asistencias_por_partido) + SUM(e.tapones_por_partido))
	FROM estadistica e, jugador j
	WHERE e.jugador = j.codigo
	AND j.nombre_equipo IN (SELECT nombre FROM equipo WHERE division = "central");
	
>CANDADO D

Consulta para saber la posición:

Muestre los tapones por partido del jugador Corey Maggette durante la temporada 00/01. Este resultado debe ser redondeado.

	SELECT ROUND(e.tapones_por_partido), j.nombre, p.temporada
	FROM estadistica e, jugador j, partido p
	WHERE e.jugador = j.codigo
	AND j.nombre = "Corey Maggette"
	AND p.temporada = "00/01";
	
Consulta para saber la clave:

Para obtener el siguiente código deberás redondear hacia abajo, la suma de puntos por partido de todos los jugadores de procedencia argentina.

	SELECT FLOOR(SUM(e.puntos_por_partido))
	FROM estadistica e, jugador j
	WHERE e.jugador = j.codigo
	AND j.procedencia = "argentina";
