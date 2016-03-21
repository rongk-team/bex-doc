 
## storages
1. tasks - *stores tasks of deliverying messages*
2. pending tasks queue - *a queue which holds pending tasks of delivery messages*
3. sub tasks - *a task would be divided into servral sub tasks.*
4. pending message queue - *each user has his onw message queue*

### Entities

#### Push Message Request

* **request_id** - ID
* **tag** - targets sending messages to
* **message_body** - a user-defined message body
* **version_number** - protocal version
* **from_type** - user/system/app
* **from_id** - sender's id
* **create_time** - date time
* **update_time** - date time

#### Push Task
* **task_id** - ID
* **request_id** - the ID of request which it is belonged to
* **stauts** - PENDING / PROCESSING / COMPLETED / CANCELLED
* **create_time** - date time
* **update_time** - date time

#### Push Sub Task
* **subtask_id** - ID
* **task_id** - the ID of task which it is belonged to
* **task_info** - stores information of this task. it might be a URL to a list of user IDs
* **stauts** - PENDING / PROCESSING / COMPLETED / CANCELLED
* **create_time** - date time
* **update_time** - date time

#### Message

* **message_id** - ID
* **request_id** - the ID of request which it is belonged to
* **status** - PENDING / SENT / DELIVERIED
* **version_number** - protocal version
* **create_time** - date time
* **update_time** - date time
