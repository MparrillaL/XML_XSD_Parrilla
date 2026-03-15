# Actividad Evaluativa: Validacion de XML con XSD y Expresiones Regulares

## 1) Tecnologias utilizadas (criterio b)
- XML 1.0 para el documento de datos.
- XSD 1.0 para describir estructura, tipos y restricciones.
- Expresiones regulares dentro de `xs:pattern` para reglas de validacion.
- VS Code con extensiones de XML/XSD para validacion asistida.
- regex101.com para disenar y depurar los patrones.

## 2) Estructura y sintaxis analizada (criterio c)
- Elemento raiz: `usuarios`.
- Elemento repetible: `usuario`.
- Atributos de `usuario`: `id`, `rol`, `estado`.
- Campos obligatorios por usuario:
  - `nombreCompleto`
  - `email`
  - `telefono`
  - `codigoPostal`
  - `nombreUsuario`
  - `contrasena`
  - `fechaRegistro`

## 3) Descripcion del documento XML (criterios d, h)
Se ha creado el esquema `usuarios.xsd` con:
- Tipos complejos para la estructura (`Usuario`).
- Tipos simples para reglas de datos (`Email`, `TelefonoES`, etc.).
- Enumeraciones para `rol` y `estado`.
- Patrones regex para validar formato y sintaxis.

## 4) Reglas con regex y justificacion (criterios d, e)

### email
Patron aplicado en XSD:
[A-Za-z0-9!#$%&'*+/=?^_`{|}~-]+(\.[A-Za-z0-9!#$%&'*+/=?^_`{|}~-]+)*@[A-Za-z0-9]([A-Za-z0-9-]*[A-Za-z0-9])?(\.[A-Za-z0-9]([A-Za-z0-9-]*[A-Za-z0-9])?)+

Justificacion:
- Permite caracteres comunes del RFC en la parte local.
- Exige dominio con al menos un punto.
- Evita guiones en posiciones invalidas del dominio.

### telefono (Espana)
Patron aplicado:
(\+34|0034)?[ -]?[6789]\d([ -]?\d){7}

Justificacion:
- Admite prefijo internacional opcional `+34` o `0034`.
- Numeracion nacional de 9 cifras que inicia en 6, 7, 8 o 9.
- Acepta espacios o guiones como separadores ligeros.

### codigoPostal (Espana)
Patron aplicado:
(0[1-9]|[1-4][0-9]|5[0-2])\d{3}

Justificacion:
- Primer bloque de provincia entre 01 y 52.
- Longitud total de 5 digitos.
- Excluye codigos no asignados como 00xxx o 53xxx+.

### nombreUsuario
Patron aplicado:
[a-z][a-z0-9._-]{3,15}

Justificacion:
- Debe iniciar por letra minuscula.
- Longitud entre 4 y 16 caracteres.
- Solo permite minusculas, digitos, punto, guion y guion bajo.
- Regla coherente con convenciones tipicas de identificadores legibles.

### contrasena
Restricciones aplicadas:
- Longitud entre 8 y 64 caracteres.
- Solo se permiten letras, digitos y simbolos habituales seguros para credenciales.

Implementacion XSD:
- Un unico `xs:pattern` en `Contrasena`.

Patron aplicado en XSD:
[A-Za-z0-9@#$%._!?*+=-]{8,64}

Justificacion:
- Politica simplificada para mantener una expresion clara y facil de explicar en la actividad.
- En XSD 1.0, imponer con un solo patron simple la presencia obligatoria de mayuscula, minuscula, digito y simbolo en cualquier orden no es practico sin volver la expresion demasiado compleja.

## 5) Asociacion XML-XSD (criterio f)
En `usuarios.xml` se incluyo:
- `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`
- `xsi:noNamespaceSchemaLocation="usuarios.xsd"`

Con esto el XML queda enlazado al esquema para validacion.

## 6) Uso de herramientas especificas (criterio g)

### VS Code
1. Instalar extensiones XML/XSD (por ejemplo, XML de Red Hat).
2. Abrir `usuarios.xml` y `usuarios.xsd`.
3. Verificar que no aparezcan errores de validacion.
4. Probar un error intencional (por ejemplo, telefono invalido) y confirmar que VS Code lo reporta.

### regex101.com
1. Seleccionar modo compatible con expresiones regulares tipo PCRE para prototipo.
2. Probar casos validos e invalidos por cada campo.
3. Ajustar la expresion y trasladarla a `xs:pattern` (adaptando escapes cuando proceda).
4. Mostrar esta evidencia en la grabacion de pantalla solicitada.
