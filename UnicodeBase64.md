# Ejemplo de como cifrar una cadena de texto en base64 #

Este ejemplo muestra como cifrar una cadena de texto, de caracteres unicode, en base64. Ademas también muestra como descifrarla.

Se utilizan las siguientes funciones:
  * `BinToStr`
  * `StrToBin`

# Código #

```pascal

var
l: Integer;
Str: WideString;
P: PWideChar;
begin
Str:= '这样还经营';
MessageBoxW(0,PWideChar('Texto original: ' + Str),'Test',
MB_OK or MB_SETFOREGROUND or MB_TASKMODAL);
Str:= BinToStr(PByteArray(PWideChar(Str)),Length(Str)*Sizeof(WideChar));
MessageBoxW(0,PWideChar('Texto codificado: ' + Str),'Test',
MB_OK or MB_SETFOREGROUND or MB_TASKMODAL);
P:= PWideChar(StrToBin(Str,l));
try
Str:= Copy(P,1,l div Sizeof(WideChar));
finally
FreeMem(P);
end;
MessageBoxW(0,PWideChar('Texto reconstruido: ' + Str),'Test',
MB_OK or MB_SETFOREGROUND or MB_TASKMODAL);
end;
```