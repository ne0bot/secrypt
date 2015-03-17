# Estructura #

## `SeAES256.pas` ##
  * `AESExpandKey`
    * Prepara la clave para ser utilizada
    * ```pascal
procedure AESExpandKey(var ExpandedKey: TAESExpandedKey; Key: TAESKey);```
    * Ejemplos: [CifrarBloque](CifrarBloque.md), [DescifrarBloque](DescifrarBloque.md)
  * `AESEncrypt`
    * Cifra un bloque de 16 bytes
    * ```pascal
procedure AESEncrypt(var State: TAESState; ExpandedKey: TAESExpandedKey);```
    * Ejemplos: [CifrarBloque](CifrarBloque.md), [DescifrarBloque](DescifrarBloque.md)
  * `AESDecrypt`
    * Descifra un bloque de 16 bytes
    * ```pascal
procedure AESDecrypt(var State: TAESState; ExpandedKey: TAESExpandedKey);```
    * Ejemplos: [DescifrarBloque](DescifrarBloque.md)
  * `AESXORState`
    * Realiza la operación XOR sobre dos bloques
    * ```pascal
procedure AESXORState(var S1: TAESState; S2: TAESState);```
  * `AESSwapKey`
    * Intercambia el orden de los bytes de la clave
    * ```pascal
procedure AESSwapKey(var Key: TAESKey);```
  * `AESCopyKey`
    * Copia el contenido de una porción de memoria para se utilizada como clave
    * ```pascal
procedure AESCopyKey(var Key: TAESKey; Buffer: Pointer);```
    * Ejemplos: [CifrarBloque](CifrarBloque.md)

## `SeBase64.pas` ##
  * `BinToStr`
    * Convierte un conjunto de datos binarios en una cadena de texto (base64)
    * ```pascal
function BinToStr(Data: PByteArray; Len: Integer): AnsiString;```
    * Ejemplos: [UnicodeBase64](UnicodeBase64.md)
  * `StrToBin`
    * Convierte una cadena de texto (base64) en un conjunto de datos binarios
    * ```pascal
function StrToBin(Str: AnsiString; var Len: Integer; Dirty: Boolean): PByteArray; overload;```
    * ```pascal
function StrToBin(Str: AnsiString; var Len: Integer): PByteArray; overload;```
    * Ejemplos: [UnicodeBase64](UnicodeBase64.md)
  * `Base64CleanStr`
    * Limpia una cadena de texto de todos los caracteres que no pertenecen a base64
    * ```pascal
function Base64CleanStr(Str: PAnsiChar; Count: Integer): Integer;```

## `SeSha256.pas` ##
  * `CalcSHA256`
    * Calcula el hash SHA256 de un conjunto de datos binarios, o de una cadena de texto
    * ```pascal
function CalcSHA256(Msg: AnsiString): TSHA256HASH; overload;```
    * ```pascal
function CalcSHA256(Stream: TStream): TSHA256HASH; overload;```
  * `SHA256ToStr`
    * Presenta el hash en formato hexadecimal para que pueda ser leído
    * ```pascal
function SHA256ToStr(Hash: TSHA256HASH): String;```

## `SeMD5.pas` ##
  * `CalcMD5`
    * Calcula el hash MD5 de un conjunto de datos binarios, o de una cadena de texto
    * ```pascal
function CalcMD5(Msg: AnsiString): TMD5HASH; overload;```
    * ```pascal
function CalcMD5(Stream: TStream): TMD5HASH; overload;```
  * `MD5ToStr`
    * Presenta el hash en formato hexadecimal para que pueda ser leído
    * ```pascal
function MD5ToStr(Hash: TMD5HASH): String;```

## `SeStreams.pas` ##
  * `TAESEnc`
    * Stream para cifrar datos usando AES256 con el metdodo CBC (Cipher-block chaining)
  * `TAESDec`
    * Stream para descifrar datos usando AES256 con el metdodo CBC (Cipher-block chaining)
  * `TBase64Enc`
    * Stream para codificar en base64 un conjunto de datos binarios
  * `TBase64Dec`
    * Stream para descodificar un conjunto de datos codificados en base64
  * `StrToStream`
    * Decodifica un conjunto de datos codificados en base64 y los guarda en un stream

## `SeEasyAES.pas` ##
  * `EasyGenKey`
    * Genera una clave de cifrado de 256 bits a partir de un texto
    * ```pascal
procedure EasyGenKey(var Key: TAESKey; Password: WideString);```
  * `EasyAESEnc`
    * Cifra utilizando AES 256 CBC con un un IV aleatorio.
    * ```pascal
procedure EasyAESEnc(Src, Dst: TStream; Password: WideString);```
    * ```pascal
function EasyAESEnc(Str, Password: WideString): WideString;```
    * ```pascal
procedure EasyAESEnc(SrcFile, DstFile, Password: WideString);```
  * `EasyAESDec`
    * Cifra utilizando AES 256 CBC con un un IV aleatorio.
    * ```pascal
procedure EasyAESDec(Src, Dst: TStream; Password: WideString);```
    * ```pascal
function EasyAESDec(Str, Password: WideString): WideString;```
    * ```pascal
procedure EasyAESDec(SrcFile, DstFile, Password: WideString);```