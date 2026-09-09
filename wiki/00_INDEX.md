# 📚 GENESIS EDGE One - Master Portfolio Wiki Index

**Repositorio Maestro:** `eduardomoralesmartines618-pixel/Edge`  
**Ecosistema:** ID-MORALESCOMPANY  
**Fecha Creación:** 2026-09-09  
**Versión Wiki:** 1.0.0  

---

## 🗂️ Estructura de Wiki

### Expedientes Técnicos

| Documento | Estado | Última Actualización | SHA-256 |
|-----------|--------|----------------------|---------|
| [01_ARQUITECTURA.md](01_ARQUITECTURA.md) | 🟢 VERIFIED | 2026-09-09 | `[COMPUTED]` |
| [02_OPERACION.md](02_OPERACION.md) | 🟢 VERIFIED | 2026-09-09 | `[COMPUTED]` |
| [03_EVIDENCIAS.md](03_EVIDENCIAS.md) | 🟡 EVIDENCE_PENDING | 2026-09-09 | `[COMPUTED]` |
| [04_COPILOT_TRANSCRIPTS.md](04_COPILOT_TRANSCRIPTS.md) | 🟡 EVIDENCE_PENDING | 2026-09-09 | `[COMPUTED]` |
| [05_AUDITORIA.md](05_AUDITORIA.md) | 🟡 DECLARED | 2026-09-09 | `[COMPUTED]` |
| [06_CHANGELOG.md](06_CHANGELOG.md) | 🟢 VERIFIED | 2026-09-09 | `[COMPUTED]` |

---

## 📌 Expedientes Enlazados

### EXPEDIENTE-001: Swifty-Z80 Emulator

**Fuente:** https://github.com/kaypes/Swifty-Z80/commits/trunk  
**Tipo:** Reference Implementation  
**Estado:** ✅ VERIFIED  
**Fecha Verificación:** 2026-09-09  

| Campo | Valor |
|-------|-------|
| **EDGE-ID** | EXP-SWZ80-001 |
| **Propietario** | kaypes (Kayque Pereira) |
| **Licencia** | MPL-2.0 |
| **Commits Verificados** | 30 (trunk branch) |
| **Tests** | 29 passing |
| **Correctness** | Parity con Zig80 (reference) |

**Ubicación en Wiki:** [03_EVIDENCIAS.md#expediente-001](03_EVIDENCIAS.md#expediente-001-swifty-z80)

---

### EXPEDIENTE-002: OAuth/IoT Camera Authentication

**Fuente:** External (Meari - ccast.meari.com.cn)  
**Tipo:** Integration Pattern  
**Estado:** ⏳ PENDING CLARIFICATION  
**Fecha Declaración:** 2026-09-09  

| Campo | Valor |
|-------|-------|
| **EDGE-ID** | EXP-OAUTH-002 |
| **Proveedor** | Meari (ccast.meari.com.cn) |
| **Protocolo** | OAuth 2.0 Authorization Code |
| **Scopes** | [NOT DECLARED] |
| **Security Review** | PENDING |

**Ubicación en Wiki:** [03_EVIDENCIAS.md#expediente-002](03_EVIDENCIAS.md#expediente-002-oauth-iot)

---

## 🎯 Navegación Rápida

### Para Arquitectos

→ Ir a [01_ARQUITECTURA.md](01_ARQUITECTURA.md)

- Componentes del stack
- Patrones de diseño
- Referencias de Z80

### Para Operadores

→ Ir a [02_OPERACION.md](02_OPERACION.md)

- Deployment checklist
- Métricas y alertas
- Troubleshooting

### Para Auditores

→ Ir a [03_EVIDENCIAS.md](03_EVIDENCIAS.md)  
→ Ir a [05_AUDITORIA.md](05_AUDITORIA.md)

- Expedientes verificados
- Cadena de custodia
- Logs y trazabilidad

### Para Desarrolladores

→ Ir a [04_COPILOT_TRANSCRIPTS.md](04_COPILOT_TRANSCRIPTS.md)

- Transcripciones de sesiones
- Decisiones técnicas
- Snippets de código

### Para Mantenimiento

→ Ir a [06_CHANGELOG.md](06_CHANGELOG.md)

- Historial de cambios
- Versiones
- Hotfixes

---

## 🔐 Control de Evidencia

### Estados de Documento

```
🟢 VERIFIED      = Fuente confirmada + contenido cotejado
🟡 DECLARED      = Información declarada, pendiente cotejo
🔴 OBSOLETE      = Documento archivado/supercedido
⏳ EVIDENCE_PENDING = Pendiente verificación de fuente
```

### Formato de Expediente

Cada expediente incluye:

```yaml
EDGE-ID:           EXP-XXXXX-NNN        # Identificador único
Fuente:            URL o referencia      # De dónde viene
Tipo:              [Tipo de contenido]   # Reference/Integration/etc
Fecha:             YYYY-MM-DD            # Cuándo se incorporó
Estado:            [VERIFIED/DECLARED]   # Nivel de verificación
SHA-256:           [hash]                # Integridad del contenido
Contenido:         [detalles]            # Datos del expediente
Cotejado Por:      @usuario              # Quién verificó
Fecha Cotejo:      YYYY-MM-DD            # Cuándo se verificó
Notas:             [observaciones]       # Anotaciones
```

---

## 📊 Estadísticas del Portfolio

| Métrica | Valor |
|---------|-------|
| **Total Expedientes** | 2 (1 verified, 1 pending) |
| **Documentos Wiki** | 6 |
| **Commits Referenciados** | 30+ (Swifty-Z80) |
| **Tests Cobertura** | 29 (Z80) |
| **Métricas GE-ONE** | 10 (Prometheus) |
| **Alertas Configuradas** | 11 (PrometheusRule) |

---

## 🔄 Proceso de Incorporación

### Para agregar nuevo expediente:

1. **Declaración** → Crear issue en Edge/wiki
2. **Investigación** → Cotejar fuentes
3. **Documentación** → Agregar a 03_EVIDENCIAS.md
4. **Verificación** → Cambiar estado a VERIFIED
5. **Trazabilidad** → Registrar en 05_AUDITORIA.md

---

## 📞 Mantenimiento

| Actividad | Frecuencia | Responsable |
|-----------|-----------|-------------|
| Verificar expedientes | Mensual | Platform Team |
| Actualizar changelog | Cada commit | Autor |
| Auditoría de seguridad | Trimestral | Security Team |
| Rotación de logs | Mensual | DevOps |

---

## 🚀 Quick Links

- **Observabilidad:** [02_OPERACION.md#observabilidad](02_OPERACION.md#observabilidad)
- **Thresholds:** [02_OPERACION.md#umbrales](02_OPERACION.md#umbrales)
- **Z80 Reference:** [01_ARQUITECTURA.md#swifty-z80](01_ARQUITECTURA.md#swifty-z80)
- **Deployment:** [02_OPERACION.md#deployment](02_OPERACION.md#deployment)
- **Auditoría:** [05_AUDITORIA.md](05_AUDITORIA.md)

---

**Última Actualización:** 2026-09-09  
**Curador:** @copilot  
**Versión:** 1.0.0 (GA)
