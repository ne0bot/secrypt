# Ejemplo de como descifrar un bloque con AES #

Este ejemplo muestra como cifrar, y luego volver a descifrar, un bloque de datos de 16 bytes (tamaño de bloque estandar).

Se utillizan las siguientes funciones:
  * `AESExpandKey`
  * `AESEncrypt`
  * `AESDecrypt`

# Código #

```pascal

var
Key: TAESKey;
ExpandedKey: TAESExpandedKey;
State: TAESState;
begin
Writeln;
// Usamos 32 'A' como clave
FillChar(Key,Sizeof(Key),'A');
// Preparamos la clave para ser usada
AESExpandKey(ExpandedKey,Key);
// Lenamos un bloque con 16 caracteres 'A'
FillChar(State,Sizeof(State),'A');
Write('Cifrando y descifrando ...');
// Ciframos el bloque
AESEncrypt(State,ExpandedKey);
// Desciframos el bloque
AESDecrypt(State,ExpandedKey);
// Mostramos el contenido del bloque
Writeln('Bloque = ' + Copy(PAnsiChar(@State),1,Sizeof(State)));
Writeln;
Writeln('Pulsa enter para salir ...');
Readln;
end.
```