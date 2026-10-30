# DevSecOps Review

Verificar que un PR o rama cumple con los ítems SSDLC asignados al integrante.

## Pasos

1. Identificar qué integrante está haciendo el PR.
2. Consultar `Repos/src/transparencia-datos-cr/docs/DEVSECOPS_CHECKLIST.md`
   para ver sus ítems asignados.
3. Consultar `Repos/src/transparencia-datos-cr/openspec/changes/devsecops-pendientes/tasks.md`
   para ver las tareas específicas.
4. Verificar por cada ítem:
   - Existe el archivo o cambio descrito
   - Hay evidencia (screenshot, test, log de CI)
   - El CI pasa (lint, test, SAST, SCA)
5. Reportar: ítems cubiertos, ítems faltantes, sugerencias.

## Criterios de aprobación

- Mínimo 3 ítems completados por integrante
- Al menos 1 ítem de una etapa diferente a las demás
- CI verde en la rama
- Sin secretos expuestos (Gitleaks debe pasar)
