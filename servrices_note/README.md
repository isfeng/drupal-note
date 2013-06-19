Drupal services note
====================

Module reference
----------------
* https://drupal.org/project/services
* https://gist.github.com/kylebrowning/affc9864487bb1b9c918


How to customize services api
-----------------------------

1. implement hook\_services\_resources()
2. implement access callback function defined in hook\_services\_resources()
3. implement resource callback function defined in hook\_services\_resources()


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


services主要提供4種類型API定義
------------------------------
1.	operations
2.	actions
3.	targeted_actions
4.	relationships


operations
--------------
operations提供基本CRUD  
url pattern: 

- create:    POST    /{endpoint}/{resource}
- retrieve:  GET     /{endpoint}/{resource}/{resource_id}
- update:    PUT     /{endpoint}/{resource}/{resource_id}
- delete:    DELETE  /{endpoint}/{resource}/{resource_id}
- index:     GET     /{endpoint}/{resource}

api ex:  

- create a group:           POST           /api/group
- retrieve a group:         GET             /api/group/1
- update a group:          PUT             /api/group/2
- delete a group:            Delete        /api/group/3
- retrieve a group list:  GET             /api/group

actions
-----------
actions是執行在resource type上，而非特定resource  
url pattern: 

- POST   /{endpoint}/{resource}/{actions}

api ex:

- -	backup group data:      POST  /api/group/backup


targeted_actions
--------------------
targeted_actions是對單一指定的resource執行動作  
url pattern: 

- POST   /{endpoint}/{resource}/{resource_id}/{targeted_actions}

api ex:

- backup data of group 3:  POST    /api/group/3/backup


relationships
-----------------
relationships是取得與某個resource相關聯的資料  
url pattern: 

- GET     /{endpoint}/{resource}/{resource_id}/{relationships}

api ex:

- Retrive group students:  GET  /api/group/3/students
- Retrive group room teacher:  GET  /api/group/3/teacher



基於services模組的web services設計方式大概就是

1. 決定提供什麽resource type
2. 決定提供哪些resource operations
3. 決定提供哪些resource actions
4. 決定提供哪些resource targeted_actions
5. 決定提供哪些resource relationships



