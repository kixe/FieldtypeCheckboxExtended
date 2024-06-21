# ProcessWire Fieldtype Checkbox Extended

This Fieldtype stores a single checkbox value as integer (0 or 1). The ON (checked) value is 1 and OFF (unchecked) value is 0

In contrast to the core field type, both the checked and the unchecked value are saved in the DB. In addition, the checked status can also be set as default in the field settings.

The difficulty in saving the unselected checkbox as a value in the DB is that an unselected checkbox does not exist at all in the transmitted form data. To avoid this problem, a hidden input field with a value was added via hook and the sum of both fields was used to determine whether the checkbox was selected or not.

The solution is based on the following trick:

HTML

```
<input type="checkbox" name="checkboxname[]" value="1" />
<input type="hidden" name="checkboxname[]" value="2" />
```

PHP

```
$value = array_sum($_POST['checkboxname']) == 2? 0 : 1;
```