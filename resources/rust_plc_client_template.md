# Plantilla de Código — Cliente PLC Modbus TCP en Rust

```rust
use std::net::SocketAddr;
use tokio_modbus::prelude::*;

pub struct PlcClient {
    ctx: Context,
}

impl PlcClient {
    pub async fn connect(addr: SocketAddr) -> Result<Self, tokio_modbus::Error> {
        let ctx = tcp::connect(addr).await?;
        Ok(Self { ctx })
    }

    pub async fn read_u32(&mut self, addr: u16) -> Result<u32, tokio_modbus::Error> {
        let data = self.ctx.read_holding_registers(addr, 2).await??;
        let val = ((data[0] as u32) << 16) | (data[1] as u32);
        Ok(val)
    }
}
```
