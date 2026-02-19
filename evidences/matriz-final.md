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

Resultado esperado: Se valida que el sistema permita ingresar con un usuario valido y muestre un mensaje de error si el usuario no es valido

Estado: PASS

Ev. UI: 
R2\UI\interfaz.png

Ev. API: 
R2\POSTMAN\postman failed login.png

Ev. BD: 
R2\DB\FAIL.png

Ev. Logs:NA

Comentarios: SN/C
	 	 	 	 	 	 	 	 

R3
	
Bloqueo 5 intentos
	
Validar LOCKED
	
Usuario activo
	
5 fails
	
Login x5
	
LOCKED + audit

Resultado esperado: Se vlaida que el sistema muestre un mensaje de error al intentar ingresar con un usuario no valido

Estado: PASS

Ev. UI: 
R3\UI\bloqueo interfaz.png

Ev. API: 
R3\POSTMAN\login.png
R3\POSTMAN\usuario bloqueado.png

Ev. BD: 
R3\DB\db blocked.png
R3\DB\desbloqueo de usuario.png
R3\DB\locked and fail locked.png
R3\DB\usuario activado.png

Ev. Logs:NA

Comentarios: SN/C
 	 	 	 	 	 	 	 

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
	 	 	 	 	 	 	 	 
Resultado esperado: Se crea el tramite de manera correcta 

Estado: PASS

Ev. UI: 
R5/UI/R5 tramite nuevo.png
R5/UI/R5_error.png
R5/UI/R5_Tramite Generado.png

Ev. API: NA

Ev. BD: 
R5/BD/R5_Validación BD.png
R5/BD/R5_Validación Carga PDF.png

Ev. Logs: NA

Comentarios: SN/C

R6
	
NO-PDF
	
Validar validación adjunto
	
Login user1
	
png/docx
	
Crear
	
Error 400
	 	 	 	 	 	 	 	 
Resultado esperado: Se valida que el sistema muestre un mensaje de error indicando que no se permite cargar archivos diferentes a PDF

Estado: PASS

Ev. UI: 
R6/UI/R6_Carga Doc.png
R6/UI/R6_Carga Imagen.png 
R6/UI/R6_Mensaje de errror.png

Ev. API: 
R6/API/R6_Postman_Carga archivo doc.png
R6\API\R6_Postman_Carga archivo imagen.png

Ev. BD: NA

Ev. Logs:NA

Comentarios: SN/C

R7
	
PDF >10MB
	
Validar límite tamaño
	
Login user1
	
big.pdf
	
Crear
	
Error 400
	 	 	 	 	 	 	 	 
Resultado esperado: Se valida que el sistema no permite cargar archivos con un peso mayor a los 10mb

Estado: PASS

Ev. UI: 
R7\UI\R7_Archivo mayor a 10mb.png
R7\UI\R7_Mensaje de error.png

Ev. API: 
R7\API\R7_Validación API.png

Ev. BD: 
R7\BD\R7_Base de datos_Registro no Creado.png

Ev. Logs:

Comentarios: SN/C

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

Se valida take simultaneo de manera correcta 

PASS



R12/UI/R12 tramite enviado 1.png

R12/Postman/.png 

R12/BD/bd 	

R12/Logs/Logs 
	 	 	 	 	 	 	 	 

R13
	
Aprobar + PDF resp
	
Validar aprobación
	
EN_REVISION
	
PDF resp
	
aprobar
	
APROBADO + RESPONSE_PDF


    Se valido la aprobación de manera correcta  

    PASS



     R13/UI/R13 Tramite aprobado.png

     R13/Postman/Documento prueba2.png	

     R13/BD/bd 	

     R13/Logs/Logs 	 	 	 	 

R14
	
Rechazo motivo
	
Validar rechazo
	
EN_REVISION
	
motivo vacío y luego texto
	
reject
	
400 y luego RECHAZADO


Se valida el flujo de manera correcta  por falta de texto, luego el rechazo con texto

PASS



R14/UI/R13 Tramite aprobado.png

R14/Postman/Campo obligatorio.png	-R14/Postman/rechazo.png

R14/BD/bd 	

R14/Logs/Logs 	 	 	 	 	 	 

R15
	
Descargar PDF
	
Validar descarga + audit
	
trámite con adjunto
	
attachment_id
	
download
	
200 + DOWNLOAD_PDF
	 	 	 	 	 	 	 	 
                                 
Se valida la descarga del documento de manera correcta 

PASS



R15/UI/R15UI Detalle.png

R15/Postman/R15 Postman1.png -- R15/Postman/R15 Postman2.png

R15/BD/bd 	

R15/Logs/Logs 