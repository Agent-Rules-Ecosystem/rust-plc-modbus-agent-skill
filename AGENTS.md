---
name: rust-plc-modbus-agent-skill
description: Specialized skill for industrial PLC Ethernet Modbus TCP async communication in Rust.
---

# 🦀🔌 Rust PLC Modbus Skill Directive

## Bootstrap de la Habilidad

1. `.skill/rust-plc-modbus-agent-skill/core/commands.md` ← Comandos de dominio
2. `.skill/rust-plc-modbus-agent-skill/core/brain.md` ← Matriz de diagnóstico y reconexión Tokio
3. `.skill/rust-plc-modbus-agent-skill/SKILL.md` ← Directivas técnicas y `tokio-modbus`
4. `.skill/rust-plc-modbus-agent-skill/knowledge/modbus_tcp_async_tokio.md` ← Referencia del runtime Tokio

## Reglas Canónicas de la Skill

1. **Uso Estricto de Async/Await**: Toda interacción con sockets Ethernet Modbus debe ser asíncrona mediante `tokio_modbus::client::tcp`.
2. **Reconexión Asíncrona Transparente**: El cliente debe envolver los fallos de `TcpStream` en un loop con `tokio::time::sleep` sin bloquear otros hilos.
3. **Manejo Seguro de Errores con `Result`**: Omitir `unwrap()` o `expect()` en código de I/O de red. Retornar `Result<T, tokio_modbus::Error>`.
4. **Persistencia Activa**: Registrar los informes de `$rustplc:audit` en `overview/work/skill/rust-plc-modbus.md`.
