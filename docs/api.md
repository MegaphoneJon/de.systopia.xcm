# API

The Extended Contact manager (XCM) provides a CiviCRM API action `getorcreate`
for the `Contact` entity.

There is no distinct parameter specification. The action takes any contact-
related parameters and relates them to one of these CiviCRM entities:

- *Contact*
- *Address*
- *Email*
- *Phone*
- *Website*

You may also submit custom field values with a key formatted as
<nobr>`<custom_group_name>.<custom_field_name>`</nobr>, which XCM will try to
resolve to the internal notation `custom_<custom_field_id>`.

The API action will return the CiviCRM ID of the contact record only.

## Example

Assume a matching rule being configured containing one or multiple of

- first name
- last name
- e-mail address

Let's say this person is not in your database:

```php
<?php
$result = civicrm_api3('Contact', 'getorcreate', array(
  'first_name' => "John",
  'last_name' => "Doe",
  'email' => "john.doe@example.org",
  ));

// $result['id'] = 1234
```

They are now. Do the same thing again:

```php
<?php
$result = civicrm_api3('Contact', 'getorcreate', array(
  'first_name' => "John",
  'last_name' => "Doe",
  'email' => "john.doe@example.org",
  ));

// $result['id'] = 1234
```

They were found and no duplicate contact was created.
