# Script de Diagnóstico — Rust Modbus TCP Harness

```bash
# Verificar puerto 502 de PLC objetivo
nc -zvw3 192.168.1.50 502

# Ejecutar test de integración Rust
cargo test --test plc_integration_test -- --nocapture
```
