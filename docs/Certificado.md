# `\CfdiUtils\Certificado`

Esta clase obtiene la información de un archivo de tipo certificado.

Una vez cargado el certificado permite obtener:
- RFC
- Nombre
- Número de serie
- Válido desde y hasta
- Llave pública
- Nombre del archivo cargado

Adicionalmente cuenta con los métodos:
- `belongsTo(string $pemKeyFile, string $passPhrase = ''): bool`
  Permite verificar si una llave privada corresponde a este certificado
- `verify(string $data, string $signature, int $algorithm = OPENSSL_ALGO_SHA256): bool`
  Permite verificar si una firma dada corresponde a los datos, como por ejemplo,
  si el sello corresponde con  la cadena de origen

## Relación con `\CfdiUtils\CfdiCertificado`

La clase `\CfdiUtils\Certificado` funciona con un archivo almacenado.
Para extraer un certificado de un cfdi se ofrece la clase `\CfdiUtils\CfdiCertificado`.

## Acerca de los formatos de archivo

El certificado (el archivo extensión CER) puede ser leído directamente.

La llave privada (el archivo extensión KEY) debe ser convertido a tipo PEM para ser correctamente interpretado
por esta clase (en realidad por PHP).

## Comandos útiles de openssl

```shell
# obtener información del certificado:
openssl x509 -nameopt utf8,sep_multiline,lname -inform DER -noout -dates -serial -subject -fingerprint -pubkey -in CSD01_AAA010101AAA.cer

# Convertir la llave privada a un archivo PEM sin contraseña:
openssl pkcs8 -inform DER -in CSD01_AAA010101AAA.key -out CSD01_AAA010101AAA.key.pem

# Establecer la contraseña a un archivo PEM:
openssl rsa -in CSD01_AAA010101AAA.key.pem -des3 -out CSD01_AAA010101AAA_password.key.pem

# convertir el certificado a formato PEM:
openssl x509 -inform DER -outform PEM -in CSD01_AAA010101AAA.cer -pubkey -out CSD01_AAA010101AAA.cer.pem
```
