# CLASIFICADOR DE INFORMES RADIOLOGICOS CRITICOS CON USO DE IA
# Proyect Sebastian Inostroza - USM - DIPLOMADO IA EN SALUD

## RESUMEN ELECCION DEL PROBLEMA ##
La generación diaria de estudios de imagenología ha resultado en un aumento exponencial del volumen de informes radiológicos, presentando un desafío operativo para su revisión oportuna y priorizada. En este escenario, la correcta identificación de 
"Resultados Críticos" aquellos que requieren comunicación urgente con el médico tratante— es un pilar para la seguridad del paciente. Sin embargo, la variabilidad de criterios entre distintos centros y protocolos puede llevar a inconsistencias en esta tarea crucial.
Para abordar este desafío, el presente proyecto se centra en el desarrollo de un modelo de inteligencia artificial como herramienta de apoyo clínico. El objetivo principal es crear un sistema capaz de leer y analizar el texto de los informes radiológicos para sugerir su clasificación como "crítico" o "no crítico". Lejos de reemplazar el juicio del especialista, esta herramienta busca ofrecer una segunda opinión sistemática y estandarizada, reforzando el criterio del radiólogo y aportando a la homogeneización de los protocolos institucionales.


## DATABASE - RECOLECCION DE DATOS
606 archivos en PDF de informes radiologicos de pacientes reales de una clinica de la Region (Anonimizada)
Para el uso de los archivos fue necesario crear un programa de anonimizacion especial para este tipo de archivos, demostrando ante los encargados el producto final y generando asi lu verde para el uso de los archivos.

## PROCESAMIENTO DE DATOS
Se decide trabajar el procesamiento inicial en archivos separados para demostrar resulados a nivel de Clinica.
PASO 1:
PASO DE PDF A TXT para maenjo de archivos. Se realiza con Codigo 

### pdf_a_txt.ipynb
