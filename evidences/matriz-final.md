1. Proyecto: Sistema de Trámites QA
Ambiente: QA Local (Docker)
URL: http://localhost:8000
Fecha de ejecución: 
Ejecutado por:
Rol:
Build/Versión: 1.0
Navegador: Chrome / Edge (versión ___)
DB: PostgreSQL (Docker)
Herramientas: Postman + DBeaver + Terminal logs


ID Caso
	
Nombre Caso
	
Objetivo
	
Precondición
	
Datos de prueba
	
Pasos resumidos
	
Resultado esperado
	
Resultado obtenido
	
Estado (PASS/FAIL)
	
Severidad (si falla)
	
Evidencia UI
	
Evidencia Postman
	
Evidencia DB
	
Evidencia Logs
	
Observaciones / Defectos


R1
	
Login válido Usuario
	
Validar login correcto
	
Usuario activo
	
usuario1/Usuario123!
	
Login
	
Entra + audit

Se loguea de manera correcta

PASS



R1/UI/R1.png

En el modulo de loguin se realizan las pruebas correctamente
	 	 	 	 	 	 	 	 

R2
	
Login inválido
	
Validar rechazo
	
Usuario activo
	
usuario1/xxx
	
Login
	
Error + audit fail
	 	 	 	 	 	 	 	 

R3
	
Bloqueo 5 intentos
	
Validar LOCKED
	
Usuario activo
	
5 fails
	
Login x5
	
LOCKED + audit
	 	 	 	 	 	 	 	 

R4
	
RBAC 403
	
Validar acceso solo propio
	
Existe usuario2 + trámite
	
tramite usuario2
	
abrir detalle
	
403
	 	 	 	 	 	 	 	 

R5
	
Crear trámite + PDF
	
Validar alta completa
	
Login user1
	
PDF válido
	
Crear trámite
	
ENVIADO + adjunto
	 	 	 	 	 	 	 	 

R6
	
NO-PDF
	
Validar validación adjunto
	
Login user1
	
png/docx
	
Crear
	
Error 400
	 	 	 	 	 	 	 	 

R7
	
PDF >10MB
	
Validar límite tamaño
	
Login user1
	
big.pdf
	
Crear
	
Error 400
	 	 	 	 	 	 	 	 

R8
	
Bandeja solo propios
	
Validar listado
	
trámites user1 y user2
	
n/a
	
Ver bandeja
	
Solo user1
	 	 	 	 	 	 	 	 

R9
	
Filtro por estado
	
Validar filtros
	
tener APROBADO y RECHAZADO
	
n/a
	
filtrar
	
resultados correctos
	 	 	 	 	 	 	 	 

R10
	
Bandeja DEAJ global
	
Validar visibilidad total
	
DEAJ logueado
	
n/a
	
ver bandeja
	
ve todos
	 	 	 	 	 	 	 	 

R11
	
Tomar trámite
	
Validar EN_REVISION
	
existe ENVIADO
	
tramite_id
	
Tomar
	
EN_REVISION + assigned
	 	 	 	 	 	 	 	 

R12
	
Concurrencia take
	
Validar 409
	
deaj1 y deaj2
	
mismo tramite
	
take simultáneo
	
1 ok 1 409
	 	 	 	 	 	 	 	 

R13
	
Aprobar + PDF resp
	
Validar aprobación
	
EN_REVISION
	
PDF resp
	
aprobar
	
APROBADO + RESPONSE_PDF
	 	 	 	 	 	 	 	 

R14
	
Rechazo motivo
	
Validar rechazo
	
EN_REVISION
	
motivo vacío y luego texto
	
reject
	
400 y luego RECHAZADO
	 	 	 	 	 	 	 	 

R15
	
Descargar PDF
	
Validar descarga + audit
	
trámite con adjunto
	
attachment_id
	
download
	
200 + DOWNLOAD_PDF
	 	 	 	 	 	 	 	 