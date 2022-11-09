## PART 3
Первостепенная и очевидная вещь, чтобы не было возможности дублей
в базе данных - сделать поле `external_id` уникальным.

```
ALTER TABLE `db`.`table`
ADD UNIQUE INDEX `external_id_UNIQUE` (`external_id` ASC) VISIBLE;
```

Также предлагаю изначально проверять наличие в базе данных таких 
же записей через метод `_getDealByExternalId`:

```
$checkedObject = $this->_getDealByExternalId($data['id']);
if (!empty($checkObject)) return false;

$this->_storeDeal(
    'Deal from webhook',
    $message,
    json_encode($fields),
);
```