ID
	
Req / Regla de negocio
	
Escenario (entrada)
	
Resultado esperado
	
Tipo de prueba
	
Herramienta(s) del stack
	
Evidencia / salida a guardar


R1
	
Acceso con credenciales válidas
	
Login con usuario1 / Usuario123!
	
Ingresa a Home Usuario + sesión creada
	
Funcional
	
UI E2E (Playwright/Cypress), API (Postman)
	
Captura Home + cookie/sesión + log en audit_log


R2
	
Error con credenciales inválidas
	
Login con password incorrecto
	
Mensaje “Credenciales inválidas”, sin sesión
	
Funcional + Negativa
	
UI E2E / Postman
	
Captura del error + respuesta/registro de intento


R3
	
Bloqueo por intentos fallidos
	
5 logins fallidos seguidos al mismo usuario
	
Usuario pasa a LOCKED y ya no permite login
	
Seguridad
	
API (Postman/RestAssured) + DB (DBeaver/psql)
	
Evidencia de bloqueo (users.status=LOCKED) + audit_log USER_LOCKED


R4
	
RBAC: Usuario no puede ver trámites ajenos
	
usuario1 intenta abrir /tramites/{id} de otro
	
403 “No autorizado”
	
Seguridad/Autorización
	
API (Postman) + UI
	
Evidencia 403 + captura


R5
	
Crear trámite con PDF obligatorio
	
Usuario llena form + adjunta PDF válido
	
Se crea folio, estado ENVIADO, adjunto guardado
	
Funcional + Integración
	
UI E2E + DB (PostgreSQL)
	
Folio + registro en tramites/attachments + status_history


R6
	
Validación de adjunto: solo PDF
	
Usuario intenta subir .docx/.png
	
Rechaza upload con mensaje
	
Funcional + Negativa
	
UI E2E + API
	
Captura mensaje + HTTP 400


R7
	
Validación de tamaño máximo de PDF
	
Usuario sube PDF > 10MB (límite default)
	
Rechaza upload (no crea adjunto)
	
Negativa
	
API (Postman) + DB
	
HTTP 400 + evidencia en DB “no attachment”


R8
	
Bandeja Usuario: listar solo propios
	
Usuario entra a /tramites
	
Lista trámites del usuario, orden desc por fecha
	
Funcional
	
UI E2E
	
Captura bandeja + conteo esperado


R9
	
Bandeja Usuario: filtro por estado
	
Filtrar status=APROBADO
	
Solo muestra aprobados del usuario
	
Funcional
	
UI E2E
	
Captura de filtro + verificación de filas

El usuario denominado deaj1 pudo ver los archivos filtrados por aceptado/rechazado

PASS



R9/UI9/R9_Bandeja de entrada deaj.png
R9/UI/R9_Peticiones enviadas usuario.png

R9/POSTMAN/R9_Status aprobado y rechazado.png
R9/POSTMAN/R9_Status aprobado.png
R9/POSTMAN/R9_Status rechazado.png

R9/LOGS/R9_Logs.png

R9/DB/R9_Archivos adjuntos.png
R9/DB/R9_Peticiones encontradas.png
R9/DB/R9_Status aprobados en la BD.png
R9/DB/R9_Status rechazados en la BD.png

Se realizaron las 4 pruebas y todas concluyen con éxito


R10
	
DEAJ visualiza bandeja global
	
deaj1 entra a /deaj/tramites
	
Ve todos los trámites (cualquier usuario)
	
Funcional
	
UI E2E
	
Captura bandeja DEAJ

El usuario denominado Deaj1 pudo observar todos las peticiones enviadas

PASSS



R10/UI/R10_Bandeja de entrada deaj.png
R10/UI/R10_Tramites aprobados.png
R10/ui/R10_Tramites rechazados.png

R10/POSTAM/R10_Bandeja de entrada.png
R10/POSTMAN/R10_Login.png

R10/DB/R10_Filtro aprobado.png
R10/DB/R10_Filtro rechazado.png
R10/DB/R10_Listado global.png

Se realizaron las 3 pruebas y todas concluyeron con éxito


R11
	
DEAJ “Toma” trámite (cambia estado)
	
DEAJ presiona Tomar sobre trámite ENVIADO
	
Estado pasa a EN_REVISION y asigna assigned_to
	
Funcional + Integración
	
UI + DB
	
Captura + tramites.status + status_history

El usuario deaj1 tomó una petición y esta paso al status EN_REVISION

PASS



R11/UI/R11_Bandeja en revision.png
R11/UI/R11_Bandeja enviado.png

R11/POSTAM/R1!_Error.png

R11/DB/11_Acciones de una peticion.png
R11/DB/R11_Integridad.png
R11/DB/R11_Listado enviados.png
R11/DB/R11_Status history.png
R11/DB/R11_Tramite en revision.png

Falló en postman a la hora de mostrar los resultados

R12
	
Concurrencia: solo un DEAJ puede tomar
	
(Simular) 2 DEAJ intentan “Tomar” el mismo trámite
	
Uno ok, el otro recibe 409
	
Integración/Concurrencia
	
API (Postman/RestAssured)
	
Evidencia 409 + evidencia de assigned_to único


R13
	
DEAJ aprueba con PDF respuesta obligatorio
	
DEAJ aprueba + llena texto + adjunta PDF
	
Estado APROBADO + crea responses + adjunto RESPONSE_PDF
	
Funcional + Integración
	
UI E2E + DB
	
Captura detalle + evidencia en responses/attachments


R14
	
DEAJ rechaza con motivo obligatorio
	
DEAJ rechaza sin motivo / con motivo
	
Sin motivo: bloquea/400; con motivo: RECHAZADO + guarda motivo
	
Funcional + Negativa
	
UI + API + DB
	
Captura validación + DB responses.reject_reason


R15
	
Descarga de PDF con auditoría
	
Usuario descarga su PDF desde detalle
	
Descarga OK + registra DOWNLOAD_PDF en auditoría
	
Funcional + Auditoría
	
UI + DB
	
Archivo descargado + registro en audit_log