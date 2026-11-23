# Contrato Edge -> Cloud (Cloud final)

Todo es sintético. El Cloud no decide en tiempo real: guarda, agrupa incidentes, etiqueta, reentrena y valida.

## Mensajes que el Cloud acepta (MQTT, QoS 1)
| Topic | Contenido | ACK |
|---|---|---|
| `wildfiresense/edge/alerts` | Alertas (sin cambios) | `cloud/ack` `{"event_id"}` |
| `wildfiresense/cloud/analysis` | Resumen por zona (ver abajo). El formato antiguo sin `zone` sigue válido | `cloud/ack` `{"event_id"}` |
| `wildfiresense/edge/evidence` | Lecturas crudas de los nodos de un incidente (10 min antes y después) | `cloud/ack` `{"event_id": "<batch_id>"}` |
| `wildfiresense/edge/status`, `edge/ping` | Sin cambios | `cloud/pong` |

### Resumen por zona (`cloud/analysis`)
Zona = bloque 4x4 de la rejilla 32x32: `z_{y//4}_{x//4}` con `idx = N-1`, `x = idx % 32`, `y = idx // 32`.
```json
{"event_id":"...","generated_at":"...","computed_by":"edge",
 "zone":"z_3_3","from_ts":1784124000000,"to_ts":1784124060000,
 "n":120,"mean_pm25":12.4,"max_pm25":48.0,"max_node_id":"node_0496"}
```
Con `computed_by:"cloud"` se envía `samples: [{"node_id":..,"pm25":..}]` (1..512) y el Cloud calcula.

### Evidencia (`edge/evidence`)
```json
{"batch_id":"unico","run_id":"...","readings":[
 {"id":496,"ts":1784124000000,"seq":12,"boot_id":"a3f1c2d4","kind":"periodic",
  "values":{"PM2.5":9.4,"PM10":17.8,"temperature":24.1,"humidity":58.3}}]}
```
- `id`: entero o `node_0496`. `ts`: ms o ISO. Máximo 1 MiB y 5000 lecturas por mensaje.
- Deduplicación por `(run_id, node, boot_id, seq)`; reenviar un lote es seguro.

## API HTTP
`GET /api/stats|alerts|incidents|readings|nodes|zones|models` · `POST /api/labels|truth|retrain|models/promote|models/rollback`.
- `incidents` incluye `timeline` (orden y segundos de alarma por nodo), `duration_s`, `peak_pm25` y `label`.

## Etiquetas y reentrenamiento
- Fuentes de etiqueta: verdad del escenario (`POST /api/truth`) o corrección manual (`POST /api/labels`). Nunca la salida del Edge. La manual prevalece.
- A las N etiquetas nuevas (por defecto 10, `RETRAIN_TRIGGER_LABELS`) se exporta el JSONL revisado, se ejecuta `lab.train --extra` y `lab.model_gate`.
- Solo un candidato aprobado se puede promover. `rollback` restaura el modelo anterior.
- El Edge debe recargar `models/forest.json` tras promover o volver atrás.
- Además del gate sintético, el candidato debe pasar los 9 escenarios de `data/scenarios` (`lab/scenario_gate.py`): no puede fallar ninguno que el modelo desplegado supere.
- Verificado de punta a punta: entrenamiento real con 42 039 filas exportadas por el Cloud en 29 s; el candidato fue rechazado por el gate (macro-F1, exactitud y retardo) y el modelo activo no cambió.
