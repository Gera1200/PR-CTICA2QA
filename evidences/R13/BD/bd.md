1. SELECT id, folio, status, assigned_to, updated_at
FROM tramites
WHERE id=1;

1 TRM-20260218-9F95F8	APROBADO	2	2026-02-18 11:09:20.640 -0600

2. SELECT id, tramite_id, responded_by, decision, response_text, reject_reason, created_at
FROM responses
WHERE tramite_id=1;

1	1	2	APPROVE	se aprobó correctamente		2026-02-18 11:09:20.640 -0600

3. SELECT id, tramite_id, type, filename, size_bytes, created_at
FROM attachments
WHERE tramite_id=1
ORDER BY created_at;

1	1	REQUEST_PDF	CHECKLIST_GALINDO RAMOS JESUS EDUARDO.pdf	71471	2026-02-18 11:04:10.653 -0600
2	1	RESPONSE_PDF	CHECKLIST_GALINDO RAMOS JESUS EDUARDO.pdf	71471	2026-02-18 11:09:20.640 -0600

4.SELECT id, from_status, to_status, changed_by, comment, changed_at
FROM status_history
WHERE tramite_id=1
ORDER BY changed_at DESC
LIMIT 5;

3	EN_REVISION	APROBADO	2	Aprobado por DEAJ	2026-02-18 11:09:20.640 -0600
2	ENVIADO	EN_REVISION	2	Trámite tomado por DEAJ	2026-02-18 11:05:04.641 -0600
1		ENVIADO	1	Creación de trámite	2026-02-18 11:04:10.653 -0600
