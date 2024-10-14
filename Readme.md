# DB Blog

## Cambios Realizados

### 1.Añadido el campo 'publication_date'

Se agregó una nueva propiedad a la clase:

```php
public $publication_date;
```
Se actualizó la definición de la clase para incluir publication_date en la estructura de la base de datos:

```php
'publication_date' => array('type' => self::TYPE_DATE, 'validate' => 'isDate'),
```

### 2. Modificada consulta SQL en 'getPost'

Se actualizó la consulta en el método getPost para filtrar los artículos según la fecha de publicación:

```php
WHERE p.active = 1 AND p.link_rewrite = '$rewrite'
    AND (p.publication_date IS NULL OR p.publication_date <= '$today')
```
Esta modificación nos permite asegurarnos que solo se recuperen los artículos que están activos y cuya fecha de publicación sea nula o ya haya pasado.

### 3. Formato de Fecha en el Método getPost

Se actualizó el formato de la fecha de publicación en el array $post:

```php
$post['publication_date'] = date_format(date_create($result['publication_date']), 'd/m/Y');
```

