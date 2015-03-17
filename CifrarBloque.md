# Ejemplo de como cifrar un bloque con AES #

Este ejemplo muestra como cifrar un bloque de datos de 16 bytes (tamaño de bloque estandar).

Se utillizan las siguientes funciones:
  * `AESCopyKey`
  * `AESExpandKey`
  * `AESEncrypt`

# Código #

```pascal

var
Key: AnsiString;
PlainText: AnsiString;
AESKey: TAESKey;
ExpandedKey: TAESExpandedKey;
State: TAESState;
begin
// Clave de 32 bytes de longitud
Key:=
#$60#$3d#$eb#$10#$15#$ca#$71#$be#$2b#$73#$ae#$f0#$85#$7d#$77#$81 +
#$1f#$35#$2c#$07#$3b#$61#$08#$d7#$2d#$98#$10#$a3#$09#$14#$df#$f4;
// Texto plano de 16 bytes de longitud
PlainText:=
#$6b#$c1#$be#$e2#$2e#$40#$9f#$96#$e9#$3d#$7e#$11#$73#$93#$17#$2a;
// Copiamos la clave en una variable del tipo TAESKey
// Debemos estar seguros de que la clave tiene 32 bytes de longitud
AESCopyKey(AESKey,PAnsiChar(Key));
// Preparamos la clave para ser utilizada
AESExpandKey(ExpandedKey,AESKey);
// Copiamos el texto que queremos cifrar en una variable del tipo TAESState (16 bytes)
move(PAnsiChar(PlainText)^,State,Sizeof(State));
// Ciframos el bloque
AESEncrypt(State,ExpandedKey);
// Ahora la variable State contiene los datos cifrados
end;
```