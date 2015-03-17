# Recibir datos cifrados con PHP #
El siguiente ejemplo muestra como cifrar datos en PHP para luego ser descifrados en una aplicación hecha en pascal (Delphi, freepascal, etc ...), usando SeCrypt. El algoritmo de cifrado es AES  (Rijndael) con una longitud de clave de 256bits y un tamaño de bloque de 16 bytes, la contraseña es una cadena de texto, de cualquier longitud, a la que calcularemos su hash (SHA256) para ser usado como clave.

El código en PHP es el siguiente:
```php

<?php
error_reporting(0);
if ($cipher = mcrypt_module_open(MCRYPT_RIJNDAEL_128, '', MCRYPT_MODE_CBC, '')) {
// Calculamos el hash que usaremos como clave
$key = hash('sha256', 'Clave secreta', true);
// Inicializamos IV
$iv = "\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0";
$data = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n".
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n".
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n".
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n".
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n".
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz1234867890'."\n";
if (mcrypt_generic_init($cipher, $key, $iv) >= 0) {
// Ciframos los datos
$data = mcrypt_generic($cipher,$data);
// Los enviamos codificados en base64
echo base64_encode($data);
mcrypt_generic_deinit($cipher);
}
mcrypt_module_close($cipher);
}
```

Aquí puedes ver el resultado: http://delphi.jmrds.com/sites/delphi.jmrds.com/adjuntos/aes.php

El código en pascal es:
```pascal

program TestPHP;

{$APPTYPE CONSOLE}

uses
Windows,
SysUtils,
Classes,
UrlMon,
SeAES256 in 'SeAES256.pas',
SeBase64 in 'SeBase64.pas',
SeSHA256 in 'SeSHA256.pas',
SeStreams in 'SeStreams.pas';

var
Data: AnsiString;
Clave: AnsiString;
Key: TAESKey;
Stream: TStringStream;
BStream: TBase64Dec;
AStream: TAESDec;
begin
// Descargamos los datos del ejemplo
UrlDownloadToFile(nil,
'http://delphi.jmrds.com/sites/delphi.jmrds.com/adjuntos/aes.php',
PChar(ChangeFileExt(ParamStr(0),'.txt')),0,nil);
with TStringList.Create do
try
// Cargamos los datos en un string
LoadFromFile(ChangeFileExt(ParamStr(0),'.txt'));
Data:= Trim(Text);
Writeln('=== Texto cifrado ===');
Writeln(Data);
Writeln;
finally
Free;
end;
// Introducimos la clave
Clave:= 'Clave secreta';
// Usamos el Hash de la clave como Key
Key:= TAESKey(CalcSHA256(Clave));
Writeln('=== Key ===');
Writeln(SHA256ToStr(TSHA256HASH(Key)));
Writeln;
Stream:= TStringStream.Create(EmptyStr);
try
AStream:= TAESDec.Create(Stream,Key);
BStream:= TBase64Dec.Create(AStream);
try
BStream.WriteBuffer(PAnsiChar(Data)^,Length(Data));
finally
BStream.Free;
AStream.Free;
end;
Writeln('=== Texto descifrado ===');
Writeln(Stream.DataString);
Writeln;
finally
Stream.Free;
end;
Readln;
end.
```