Drupal services note
====================


How to customize services api
-----------------------------

* implement hook\_services\_resources()
* implement access callback function defined in hook\_services\_resources()
* implement resource callback function defined in hook\_services\_resources()


How to define services
----------------------

Return An associative array which defines available resources in hook_services_resources.

The associative array which defines services has five possible top
level keys. The operations array has five possible keys representing
the CRUD operations.

- operations              -- CRUD functions
  - create                -- POST
  - retrieve              -- GET
  - update                -- PUT
  - delete                -- DELETE
  - index
- actions                 -- Action直接執行在Resource Type, 非執行在指定的單一Resource
- targeted_actions        -- Targeted actions執行在指定的單一Resource
- relationships           -- 取得與指定Resouce有某種關係的相關資料

參考services.services.api.php

