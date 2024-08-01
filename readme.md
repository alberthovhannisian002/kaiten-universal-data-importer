# Data Import Specification

This document outlines the required fields and their descriptions for importing data from various task management tools into our system. Please ensure that the provided data matches the specified formats and includes all mandatory fields for a successful import.

## Table of Contents

1. [Introduction](#introduction)
2. [General Requirements](#general-requirements)
3. [User Data](#user-data)
4. [Boards Data](#boards-data)
5. [Columns Data](#columns-data)
6. [Cards Data](#cards-data)
7. [Comments Data](#comments-data)
8. [Card files Data](#card-files-data)
9. [Custom fields Data](#custom-fields-data)
10. [Meta data](#meta-data)

## Introduction

This specification defines the structure and required fields for importing data from task management tools like Asana, Jira, Trello, etc. The goal is to ensure that the imported data can be processed correctly and integrated into our system.

## General Requirements

- **File Format**: JSON
- **Field Types**: Ensure correct data types are used (string, integer, datetime, etc.)
- **Required Fields**: All required fields must be present and non-empty.
- **Email Validation**: Email fields must contain valid email addresses.

There are some required entities that is used to process the import - boards, columns, cards

Below is represented the required fields for entities

## Users Data

Description of importing process: Validates json data, if there are no validation issues, checks if the company is already existing for user, after that is checking if the user has access to some specific space, after that we are sending invite to user with default role of writer

### Fields

| Field Name  | Type             | Required | Description                               |
|-------------|------------------|----------|-------------------------------------------|
| `id`        | String \| Number | Yes      | Unique identifier for the user.           |
| `full_name` | String           | No       | Full name of the user.                    |
| `email`     | String           | Yes      | Email address of the user. Must be valid. |
| `username`  | String           | No       | Username.                                 |

### Description

- **id**: A unique identifier for the user, which is used to map and track the user within our system.
- **full_name**: The complete name of the user, used for display purposes.
- **email**: The user's email address, which must be a valid email format. This is used for communication and identification.
- **username**: Username, used for display purposes.

### Example JSON Structure


```json
[
  {
  "id": "123456",
  "full_name": "John Doe",
  "email": "john.doe@example.com",
  "username": "johndoe"
  }
]
```

## Boards data

### Fields

| Field Name  | Type             | Required | Description                           |
|-------------|------------------|----------|---------------------------------------|
| `id`        | String \| Number | Yes      | Unique identifier of the board.       |
| `title`     | String           | Yes      | Name of the board.  Max 128 char      |
| `author_id` | String           | No       | Unique identifier of author of board. |
| `created`   | Null or DateTime | No       | Date of creation of board.            |


### Description

- **id**: A unique identifier for the board, which is used to map and track the board within our system.
- **title**: The complete name of the board, used for display purposes.
- **author_id**: A unique identifier of author of board, used for display purposes.
- **created**: Null or Datetime of creation of board

### Example JSON Structure

```json
[
  {
    "id": "1207864633562249",
    "title": "Project01",
    "created": "2024-07-22T07:01:37.954Z",
    "author_id": "1207864767588674"
  }
]
```

## Columns data

### Fields

| Field Name   | Type             | Required | Description                           |
|--------------|------------------|----------|---------------------------------------|
| `id`         | String \| Number | Yes      | Unique identifier of column in board. |
| `title`      | String           | Yes      | Name of column. Max 128 chars.        |
| `board_id`   | String \| Number | Yes      | Unique identifier of board.           |
| `sort_order` | Number           | No       | Order sequence number.                |
| `type`       | Number           | No       | Sets up column type.                  |
| `created`    | Null or DateTime | No       | Date of creation of column            |

### Description

- **id**: Unique identifier of column in board.
- **title**: The complete name of the column, used for display purposes.
- **board_id**: A unique identifier of board, which is used to make relation between boards and columns.
- **sort_order**: Defines the order of columns inside space.
- **type**: Defines the actual type of column, available values are queued (value 1), in progress(value 2), done(value 3).
- **created**: Null or Datetime of creation of column

### Example JSON Structure

```json
 [
  {
      "id": "1207254524924717",
      "title": "To do",
      "created": "2024-05-07T06:34:24.413Z",
      "sort_order": 1,
      "type": 1,
      "board_id": "1207254524924716"
    },
    {
      "id": "1207254524924721",
      "title": "In progress",
      "created": "2024-05-07T06:34:24.413Z",
      "sort_order": 2,
      "type": 2,
      "board_id": "1207254524924716"
    }
]
```

## Cards data

### Fields

| Field Name            | Type                    | Required | Description                                            |
|-----------------------|-------------------------|----------|--------------------------------------------------------|
| `id`                  | String \| Number        | Yes      | Unique identifier of card.                             |
| `owner_id`            | String \| Number        | Yes      | Unique identifier of owner of card.                    |
| `responsible_id`      | String \| Number        | No       | Unique identifier of responsible of card.              |
| `column_id`           | String \| Number        | Yes      | Unique identifier of column in board.                  |
| `title`               | String                  | Yes      | Title of card. Max length 1024 chars                   |
| `description`         | String                  | No       | The description content of card                        |
| `description_type`    | String                  | No       | Defines the type of description.                       |
| `condition`           | Number                  | No       | Defines the current card status condition.             |
| `tags`                | CardTags[]              | No       | Defines the tags of card.                              |
| `history`             | CardHistory[]           | No       | Defines the card actions history.                      |
| `links`               | CardLinks[]             | No       | Defines the links attached to card.                    |
| `completed_by`        | String \| Number        | No       | ID of user who completed the card.                     |
| `properties`          | CardProperties[]        | No       | Array of custom properties of card.                    |
| `due_date`            | Null or CardDateObject  | No       | Due date of card.                                      |
| `planned_start`       | Null or CardDateObject  | No       | Planned start date of card.                            |
| `planned_end`         | Null or CardDateObject  | No       | Planned end date of card.                              |
| `created`             | Null or DateTime string | No       | Date of creation of card .                             |
| `checklists`          | CardChecklist[]         | No       | The checklists of card.                                |
| `blocked_by_card_ids` | Array                   | No       | IDs of cards which are blocking current card.          |
| `blocks_card_ids`     | Array                   | No       | IDs of cards which are bloked because of current card. |
| `parent_card_ids`     | Array                   | No       | IDs of parent cards.                                   |
| `child_card_ids`      | Array                   | No       | IDs of child cards.                                    |

### Description

- **id**: A unique identifier of card, which is used to map and track the card within our system.
- **title**: The complete title of card, used for display purposes.
- **owner_id**: Unique identifier of owner of card, used to create relations and display purposes.
- **responsible_id**: Unique identifier of responsible for card, used to create relations and display purposes
- **column_id**: Unique identifier of column in which the card is placed.
- **description**: The content description of card.
- **description_type**: The type of description, available values are markdown and html.
- **condition**: Number which identifies the current status condition of card, available values are - active(condition: 1), archived(condition: 2), deleted(condition: 3) .
- **tags**: Array of tags that are attached to card.
- **history**: Array of card actions history.
- **links**: Array of links that are attached to card.
- **completed_by**: ID of user who completed the card.
- **properties**: Array of custom properties available for current card.
- **due_date**: Due date of card.
- **planned_start**: Planned start date of card, used for display purposes, visible in Timeline section.
- **planned_end**: Planned end date of card, used for display purposes, visible in Timeline section.
- **blocked_by_card_ids**: Array of card ids which are blocking the current card. 
- **blocks_card_ids**: Array of card ids which are blocked because of current card.
- **parent_card_ids**: Array of parent card ids. 
- **child_card_ids**:  Array of child card ids.


### CardProperties fields

| Field Name | Type                                         | Required | Description                           |
|------------|----------------------------------------------|----------|---------------------------------------|
| `id`       | String \| Number                             | Yes      | Unique identifier of custom property. |
| `value`    | String \| Number \| Date \| DateTime \| ID[] | Yes      | Custom property values.               |

Custom property ID must exist or be included in the current import (custom fields data).
If type of the value is `select` | `multi_select` | `people` then the value is array of IDs.
Custom property value ID must exist or be included in the current import (custom fields data or users data).

### Example JSON Structure

```json
[
     {
        "id": "1207864637859364",
        "owner_id": "1207864767588674",
        "responsible_id": null,
        "column_id": "1207864633562250",
        "title": "Task03",
        "description": "<body></body>",
        "description_type": "html",
        "condition": 1,
        "tags": [],
        "history": [
            {
                "type": "card_due_date_change",
                "created": "2024-07-22T07:01:46.584Z",
                "author_id": "1207864767588674",
                "old_value": {
                    "value": "2024-07-26",
                    "time_present": false
                },
                "new_value": {
                    "value": "2024-07-26",
                    "time_present": false
                }
            }
        ],
       "checklists": [
         {
           "name": "Subtasks",
           "items": [
             {
               "text": "new one",
               "sort_order": 1,
               "checked": true,
               "created": "2024-05-13T15:36:49.384Z",
               "checked_at": "2024-05-27T12:20:21.274Z",
               "checked_by": "1207221341939584",
               "created_by": "1207221341939584",
               "due_date": {
                 "value": "2024-05-16",
                 "time_present": false
               },
               "responsible_id": "1207221341939584"
             },
             {
               "text": "second",
               "sort_order": 2,
               "checked": false,
               "created": "2024-05-13T15:36:52.931Z",
               "created_by": "1207221341939584",
               "responsible_id": "1207221341939584",
               "due_date": {
                 "value": "2024-05-29T16:00:00.000Z",
                 "time_present": true
               }
             }
           ]
         }
         ],
         "created": "2024-07-22T07:01:42.395Z",
        "links": [
            {
                "url": "https://app.asana.com/0/1207864633562249/1207864637859364"
            }
        ],
        "completed": false,
        "completed_by": null,
        "completed_at": null,
       "properties": [
         {
           "id": "1207888014064892",
           "value": "Text example"
         },
         {
           "id": "1207888014064899",
           "value": 123.456
         },
         {
           "id": "1207914037042113",
           "value": "2024-07-17"
         },
         {
           "id": "1207645766223465",
           "value": ["1207221263311709", "1207221341939584"]
         },
         {
           "id": "1207631614467241",
           "value": ["1207631614467242"]
         },
         {
           "id": "1207723749200577",
           "value": ["1207723749200601", "1207723749200612"]
         }
       ],
        "due_date": {
            "value": "2024-07-26",
            "time_present": false
        },
        "planned_start": {
            "value": "2024-07-24",
            "time_present": false
        },
        "planned_end": {
            "value": "2024-07-26",
            "time_present": false
        }
    }
]
```

### CardTags fields

| Field Name | Type             | Required | Description                     |
|------------|------------------|----------|---------------------------------|
| `id`       | String \| Number | Yes      | Unique identifier of card tag.  |
| `name`     | String           | Yes      | Name of card tag. Max 128 chars |

```json
{
  "id": "1207254524924728",
  "name": "some new"
}
```

### CardHistory fields

| Field Name  | Type             | Required | Description                                                                                                                        |
|-------------|------------------|----------|------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | String           | Yes      | Type of history action, available values - `card_move`, `card_due_date_change`, `card_tag_add`, `card_tag_remove`, `card_assign` . |
| `created`   | DateTime         | Yes      | DateTime of history action.                                                                                                        |
| `author_id` | String \| Number | Yes      | ID of author of action.                                                                                                            |
| `old_value` | Object           | No       | Object where is represented the old value that should be changed.                                                                  |
| `new_value` | Object           | No       | Object where is represented the new value.                                                                                         |
| `value`     | Object           | No       | If there is an old value you should send value object with new values that should be applied.                                      |

```json
{
      "type": "card_move",
      "created": "2024-05-14T06:00:21.323Z",
      "author_id": "1207221341939584",
      "old_value": {
        "column_id": "1207254524924722"
      },
      "new_value": {
        "column_id": "1207254524924717"
      }
}
```

### CardLinks fields

| Field Name    | Type                    | Required | Description                                                   |
|---------------|-------------------------|----------|---------------------------------------------------------------|
| `url`         | String \| Number        | Yes      | The URL of resource that should be displayed. Max 16384 chars |
| `description` | String                  | No       | String description of card link.                              |
| `created`     | DateTime string or Null | No       | DateTime of adding card link.                                 |

```json
{
    "url": "https://google.com",
    "description": "some description",
    "created": "2024-05-13T15:36:35.567Z"
}
```

### CardChecklist fields

| Field Name      | Type                | Required | Description                         |
|-----------------|---------------------|----------|-------------------------------------|
| `name`          | String              | No       | Name of checklist. Max 1024 chars.  |
| `items`         | ChecklistItem[]     | No       | Array of checklist items.           |
| `created`       | DateTime string     | No       | DateTime of creation checklist.     |
| `due_date`      | ChecklistDateObject | No       | Due date of checklist.              |
| `planned_start` | ChecklistDateObject | No       | Date of planned start of checklist. |
| `planned_end`   | ChecklistDateObject | No       | Date of planned end of checklist.   |


### ChecklistItem fields

| Field Name       | Type                | Required | Description                                       |
|------------------|---------------------|----------|---------------------------------------------------|
| `text`           | String              | Yes      | Text description of checklist item.               |
| `sort_order`     | Number              | No       | Order of checklist item in checklist.             |
| `checked`        | Boolean             | No       | If true checklist is marked as done.              |
| `created`        | DateTime string     | No       | DateTime of creation checklist item.              |
| `checked_at`     | DateTime string     | No       | DateTime when checklist item was checked.         |
| `checked_by`     | Number \| String    | No       | ID of user who checked the checklist item.        |
| `created_by`     | Number \| String    | No       | ID of user who created the checklist item.        |
| `due_date`       | ChecklistDateObject | No       | Due date of checklist item.                       |
| `responsible_id` | Number \| String    | No       | ID of user who is responsible for checklist item. |


### ChecklistDateObject

| Field Name     | Type             | Required | Description                                                            |
|----------------|------------------|----------|------------------------------------------------------------------------|
| `value`        | Date \| DateTime | No       | Date value .                                                           |
| `time_present` | Boolean          | No       | Boolean value that defines if `value` contains only date or time also. |

If the value includes time (DateTime) so `time_present` parameter should be set to true

## Comments data

### Fields

| Field Name    | Type             | Required | Description                          |
|---------------|------------------|----------|--------------------------------------|
| `id`          | String \| Number | Yes      | Unique identifier of comment.        |
| `card_id`     | String \| Number | Yes      | Unique identifier of card.           |
| `text`        | String           | Yes      | Content of comment.                  |
| `author_name` | String           | No       | Full name of comment author.         |
| `author_id`   | String \| Number | No       | Unique identifier of comment author. |
| `created`     | Null or Datetime | No       | Date of creation of comment          |

### Description

- **id**:  A unique identifier of comment, which is used to map and track the comment within our system.
- **card_id**: A unique identifier of card, under which the comment is written, which is used to map and track the comment within our system.
- **text**: Content of comment, used to display comment content.
- **author_name**: Name of the author who wrote the comment, used for display purposes
- **author_id**: A unique identifier of author for comment, used to map and track the comment, make relation to author, and display
- **created**: Date of creation the comment, or if empty by default will be used current date.

### Example JSON Structure

```json
[
    {
      "id": "1207254524924717",
      "text": "second",
      "created": "2024-05-13T14:18:18.805Z",
      "author_id": "1207221341939584",
      "card_id": "1207254524924719"
    },
    {
      "id": "1207254524924721",
      "text": "one more with file",
      "created": "2024-05-13T14:18:34.282Z",
      "author_id": "1207221341939584",
      "card_id": "1207254524924719"
    }
  ]
```

## Card files data

### Fields

| Field Name      | Type         | Required | Description                                                      |
|-----------------|--------------|----------|------------------------------------------------------------------|
| `id`            | String       | Yes      | Unique identifier for the card file.                             |
| `card_id`       | String       | Yes      | Unique identifier of card.                                       |
| `name`          | String       | Yes      | Name of card file.                                               |
| `author_id`     | String       | No       | Unique identifier of author of file.                             |
| `created`       | Null or Date | No       | Date of upload of card file                                      |
| `external`      | Boolean      | No       | Boolean value which specifying if the storage is external or not |
| `external_type` | String       | No`*`    | String which represents external storage type                    |
| `external_url`  | String       | No`*`    | URL of external storage file                                     |
| `size`          | Number       | No       | Size of card file                                                |

`*` - if `external` property is set to `true`, then `external_type` and `external_url` should be present also.

### Description

- **id**: Unique identifier of card file.
- **card_id**: Parent card ID, where the file is attached.
- **name**: Defines the name of card file.
- **author_id**: ID of author of the attached file.
- **created**: Date of uploading card file.
- **external**: Defines if the file is from external or internal storage.
- **external_type**: Defines external storage type, available options are: gdrive, dropbox.
- **external_url**: Defines url of external storage file.

### Example JSON Structure

```json
[
  {
    "id": "1207301518919127",
    "name": "Снимок экрана 2024-05-07 в 10.19.37.png",
    "size": 83562,
    "created": "2024-05-13T14:18:32.099Z",
    "card_id": "1207254524924719",
    "external": false
  },
  {
    "id": "1207301518919130",
    "name": "Снимок экрана 2024-04-25 в 17.44.27.png",
    "size": 505397,
    "created": "2024-05-13T14:18:48.648Z",
    "card_id": "1207254524924719",
    "external": false
  }
]
```

## Custom fields data

### Fields

| Field Name | Type                 | Required | Description                                                    |
|------------|----------------------|----------|----------------------------------------------------------------|
| `id`       | String \| Number     | Yes      | Unique identifier of field. Max length 1024 chars              |
| `type`     | String               | Yes      | Allowed types `string`,`number`,`date`,`select`,`multi_select` |
| `name`     | String               | Yes      | Name of field. Max length 128 chars                            |
| `options`  | CustomFieldOption[] | No       | Options of custom field                                        |


### Description

- **id**: Unique identifier of custom field.
- **type**: Defines the allowed types of custom field.
- **name**: Defines the name of custom field, used for display purposes.
- **options**: Defines the available options for selected custom field type.

### Example JSON Structure

```json
[
  {
    "id": "1207864637859355",
    "type": "select",
    "name": "Status",
    "options": [
      {
        "id": "1207864637859356",
        "value": "On track",
        "color": 9,
        "sort_order": 0
      },
      {
        "id": "1207864637859357",
        "value": "At risk",
        "color": 12,
        "sort_order": 1
      },
      {
        "id": "1207864637859358",
        "value": "Off track",
        "color": 1,
        "sort_order": 2
      }
    ]
  }
]
```

### CustomFieldOption fields

| Field Name   | Type                                 | Required | Description                                                      |
|--------------|--------------------------------------|----------|------------------------------------------------------------------|
| `id`         | String \| Number                     | Yes      | Unique identifier of custom field option. Max length 1024 chars. |
| `value`      | String \| Number \| Date \| DateTime | Yes      | Value of custom field option. Max length 128 chars.              |
| `color`      | Number                               | No       | Integer (1-17), based on color scheme.                           |
| `sort_order` | Number                               | No       | Float sorting value.                                             |


### CustomFieldOption Description

- **id**: Unique identifier of custom field option.
- **value**: Value of custom field option.
- **color**: An integer (1-17) that defines the selected color of custom property.
- **sort_order**: The numeric value which defines the sort order.

### Example JSON Structure

```json
[
  {
    "id": "1207864637859351",
    "value": "Low",
    "color": 8,
    "sort_order": 1.5
  }
]
```

### Color Scheme

| ID  | Name        |
|-----|-------------|
| 1   | Red         |
| 2   | Pink        |
| 3   | Purple      |
| 4   | Deep purple |
| 5   | Indigo      |
| 6   | Blue        |
| 7   | Light blue  |
| 8   | Cyan        |
| 9   | Teal        |
| 10  | Green       |
| 11  | Light green |
| 12  | Lime        |
| 13  | Orange      |
| 14  | Deep orange |
| 15  | Brown       |
| 16  | Blue grey   |
| 17  | Yellow      |


## Meta data

| Field Name           | Type   | Required | Description                        |
|----------------------|--------|----------|------------------------------------|
| `entities`           | Array  | Yes`*`   | Entities that should import        |
| `entities_paths_map` | Object | Yes      | Path to json files for each entity |

`*` - As mentioned at the top there are tree required entities - `boards`, `columns`, `cards`. The other entities aren't required.
Meta data file name is - `meta-data.json`, this is the main file which contains the all meta data information.

### Meta data Description

- **entities**: Array of entities that should be mapped.
- **entities_paths_map**: Paths to JSON files which should be the source of import.

### Example JSON Structure

```json
{
  "entities": [
    "users",
    "boards",
    "columns",
    "cards",
    "customFields",
    "comments",
    "files"
  ],
  "entities_paths_map": {
    "users": [
      "users_0.json"
    ],
    "boards": [
      "boards_0.json"
    ],
    "columns": [
      "columns_0.json"
    ],
    "cards": [
      "cards_0.json"
    ],
    "customFields": [
      "customFields_0.json"
    ],
    "comments": [
      "comments_0.json"
    ],
    "files": [
      "files_0.json"
    ]
  }
}
```
