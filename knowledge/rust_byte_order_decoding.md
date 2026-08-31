# Decodificación de Endianness y Float32 en Rust

---

## 🔢 Parsing con Crate `byteorder`

```rust
use byteorder::{BigEndian, ByteOrder};

pub fn parse_float32(reg1: u16, reg2: u16) -> f32 {
    let mut bytes = [0u8; 4];
    BigEndian::write_u16(&mut bytes[0..2], reg1);
    BigEndian::write_u16(&mut bytes[2..4], reg2);
    BigEndian::read_f32(&bytes)
}

pub fn parse_int32_swapped(reg1: u16, reg2: u16) -> i32 {
    let mut bytes = [0u8; 4];
    BigEndian::write_u16(&mut bytes[0..2], reg2); // Word swap
    BigEndian::write_u16(&mut bytes[2..4], reg1);
    BigEndian::read_i32(&bytes)
}
```
