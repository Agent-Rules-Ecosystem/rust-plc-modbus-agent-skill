# Concurrencia Async Tokio con Modbus TCP en Rust

---

## ⚡ Manejo de Conexiones Tokio con Reconexión Automática

```rust
use std::net::SocketAddr;
use std::time::Duration;
use tokio::time::sleep;
use tokio_modbus::prelude::*;

pub async fn run_plc_worker(addr: SocketAddr) {
    loop {
        match tcp::connect(addr).await {
            Ok(mut ctx) => {
                println!("Conectado a PLC en {}", addr);
                if let Err(e) = poll_plc(&mut ctx).await {
                    eprintln!("Error en comunicación PLC: {:?}", e);
                }
            }
            Err(e) => {
                eprintln!("Fallo de conexión TCP con PLC ({}): {:?}", addr, e);
            }
        }
        sleep(Duration::from_secs(3)).await;
    }
}

async fn poll_plc(ctx: &mut Context) -> Result<(), tokio_modbus::Error> {
    let regs = ctx.read_holding_registers(0, 10).await??;
    println!("Registros PLC: {:?}", regs);
    Ok(())
}
```
