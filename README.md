# Jcbin
JongChan's binary serialization format. Pronounce as `jay-see-bin`.
It targets speed, backward compatibility, ease to implement.

## Wire format
Jcbin's serialization unit is message. The serialized message is array of message fields.
Each field consists of 4 bytes header and variable length payload.
Every multi-byte data is interpreted with little endian when you are reading it as integer.

### Field structure
`aa aa bb cc (dd dd dd dd) ee ee ee (ff)`

- `a`: field number
- `b`: field version
- `c`: field length
- `d`: extended field length (if `c` is zero)
- `e`: payload
- `f`: padding to align 4 bytes

### How to calculate payload length

If `c`(field length) is zero, the field length is `d`(extended field length).\
Else, the field length is `c * 4`.
