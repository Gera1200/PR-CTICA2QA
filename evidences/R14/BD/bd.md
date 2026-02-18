1. SELECT t.id, t.folio, t.subject, t.status, t.assigned_to
FROM tramites t
LEFT JOIN responses r ON r.tramite_id = t.id
WHERE t.status='EN_REVISION' AND r.id IS NULL
ORDER BY t.created_at DESC
LIMIT 5;

2	TRM-20260218-37BBB1	Solicitud2	EN_REVISION	2


2. SELECT id, status
FROM tramites
WHERE id=2;

2	EN_REVISION

3. SELECT id, status
FROM tramites
WHERE id=2;

2	RECHAZADO