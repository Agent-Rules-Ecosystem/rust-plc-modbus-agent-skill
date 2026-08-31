# Motor de Decisiones — rust-plc-modbus-agent-skill

| Situación | Diagnóstico | Acción recomendada |
|---|---|---|
| Fallo en `tcp::connect` | Socket cerrado o IP inalcanzable | Reintentar en loop con `tokio::time::sleep(Duration::from_secs(2))` |
| Error `Exception Code` de Modbus | Dirección o función no soportada | Verificar si la dirección en el PLC es base 0 o base 1 |
| Incompatibilidad de tipos | Conversión manual fallida | Usar `byteorder::BigEndian::read_f32` sobre el slice leido |
| Bloqueo del runtime | Código síncrono en async fn | Asegurar que toda llamada I/O se haga con `.await` |
