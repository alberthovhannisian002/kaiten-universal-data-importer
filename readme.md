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
| `created`   | Null or DateTime | No       | Date of creation of board             |


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
| `title`      | String           | Yes      | Name of column.                       |
| `board_id`   | String \| Number | Yes      | Unique identifier of board.           |
| `sort_order` | Number           | No       | Order sequence number                 |
| `type`       | Number           | No       | Sets up column type                   |
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

| Field Name         | Type             | Required | Description                               |
|--------------------|------------------|----------|-------------------------------------------|
| `id`               | String \| Number | Yes      | Unique identifier of card.                |
| `owner_id`         | String \| Number | Yes      | Unique identifier of owner of card.       |
| `responsible_id`   | String \| Number | No       | Unique identifier of responsible of card. |
| `column_id`        | String \| Number | Yes      | Unique identifier of column in board.     |
| `title`            | String           | Yes      | Title of card.  Max length 1024 chars     |
| `description`      | String           | Yes      | The description content of card           |
| `description_type` | String           | No       | Defines the type of description.          |
| `condition`        | Number           | No       | ?.                                        |
| `tags`             | CardTags[]       | No       | Defines the tags of card.                 |
| `history`          | CardHistory[]    | No       | Defines the card actions history.         |
| `links`            | CardLinks[]      | No       | .                                         |
| `completed`        |                  | No       | .                                         |
| `completed_by`     |                  | No       | .                                         |
| `properties`       |                  | No       | .                                         |
| `due_date`         | Null or Date     | No       | Due date of card.                         |
| `planned_start`    | Null or Date     | No       | Planned start date of card.               |
| `planned_end`      | Null or Date     | No       | Planned end date of card.                 |
| `created`          | Null or Date     | No       | Date of creation of card .                |
| `checklist`        | CardChecklist[]  | No       | The checklists of card.                   |

### Description

- **id**: A unique identifier of card, which is used to map and track the card within our system.
- **title**: The complete title of card, used for display purposes.
- **owner_id**: Unique identifier of owner of card, used to create relations and display purposes.
- **responsible_id**: Unique identifier of responsible of card, used to create relations and display purposes
- **column_id**: Unique identifier of column in which the card is placed.
- **description**: The content description of card.
- **description_type**: The type of description, available values are markdown and html.
- **condition**: .
- **tags**: .
- **history**: .
- **links**: .
- **completed**: .
- **completed_by**: .
- **properties**: .
- **due_date**: Due date of card.
- **planned_start**: Planned start date of card.
- **planned_end**: Planned end date of card.

### Example JSON Structure

```json
[
    {
        "id": "1207864637859360",
        "owner_id": "1207864767588674",
        "responsible_id": "1207864767588674",
        "column_id": "1207864633562250",
        "title": "Task01",
        "description": "<body></body>",
        "description_type": "html",
        "condition": 1,
        "tags": [],
        "history": [
            {
                "type": "card_assign",
                "created": "2024-07-22T07:01:41.368Z",
                "author_id": "1207864767588674",
                "value": {
                    "user_id": "1207864767588674"
                }
            },
            {
                "type": "card_due_date_change",
                "created": "2024-07-22T07:01:46.107Z",
                "author_id": "1207864767588674",
                "old_value": {
                    "value": "2024-07-24",
                    "time_present": false
                },
                "new_value": {
                    "value": "2024-07-24",
                    "time_present": false
                }
            }
        ],
        "created": "2024-07-22T07:01:41.009Z",
        "links": [
            {
                "url": "https://app.asana.com/0/1207864633562249/1207864637859360"
            }
        ],
        "completed": false,
        "completed_by": null,
        "completed_at": null,
        "properties": [
            {
                "id": "1207864637859350",
                "value": {
                    "id": "1207864637859351",
                    "value": "Low",
                    "color": 8
                }
            },
            {
                "id": "1207864637859355",
                "value": {
                    "id": "1207864637859357",
                    "value": "At risk",
                    "color": 12
                }
            },
            {
                "id": "1207864637859405",
                "value": [
                    {
                        "id": "1207864778999507",
                        "value": "k333dg+3@gmail.com"
                    },
                    {
                        "id": "1207864780759883",
                        "value": "k333dg+4@gmail.com"
                    }
                ]
            },
            {
                "id": "1207864637859408",
                "value": [
                    {
                        "id": "1207864637859409",
                        "value": "Yellow",
                        "color": 12
                    },
                    {
                        "id": "1207864637859410",
                        "value": "Blue",
                        "color": 6
                    }
                ]
            }
        ],
        "due_date": {
            "value": "2024-07-24",
            "time_present": false
        },
        "planned_start": {
            "value": "2024-07-22",
            "time_present": false
        },
        "planned_end": {
            "value": "2024-07-24",
            "time_present": false
        }
    },
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
                "id": "1207864637859350",
                "value": {
                    "id": "1207864637859353",
                    "value": "High",
                    "color": 3
                }
            },
            {
                "id": "1207864637859355",
                "value": {
                    "id": "1207864637859358",
                    "value": "Off track",
                    "color": 1
                }
            },
            {
                "id": "1207864637859405",
                "value": [
                    {
                        "id": "1207864780910183",
                        "value": "k333dg+5@gmail.com"
                    },
                    {
                        "id": "1207864780759883",
                        "value": "k333dg+4@gmail.com"
                    }
                ]
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

| Field Name | Type             | Required | Description                    |
|------------|------------------|----------|--------------------------------|
| `id`       | String \| Number | Yes      | Unique identifier of card tag. |
| `name`     | String           | Yes      | Name of card tag.              |

```json
{
  "id": "1207254524924728",
  "name": "some new"
}
```

### CardHistory fields

| Field Name  | Type             | Required | Description                    |
|-------------|------------------|----------|--------------------------------|
| `type`      | String \| Number | Yes      | Unique identifier of card tag. |
| `created`   | String           | Yes      | Name of card tag.              |
| `author_id` | String           | Yes      | Name of card tag.              |
| `old_value` | String           | Yes      | Name of card tag.              |
| `new_value` | String           | Yes      | Name of card tag.              |


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

| Field Name    | Type             | Required | Description                    |
|---------------|------------------|----------|--------------------------------|
| `url`         | String \| Number | Yes      | Unique identifier of card tag. |
| `description` | String           | Yes      | Name of card tag.              |
| `created`     | String           | Yes      | Name of card tag.              |

```json
{
    "url": "https://google.com",
    "description": "some description",
    "created": "2024-05-13T15:36:35.567Z"
}
```

### CardChecklist fields

| Field Name      | Type            | Required | Description                    |
|-----------------|-----------------|----------|--------------------------------|
| `name`          | String          |          | Unique identifier of card tag. |
| `items`         | ChecklistItem[] |          | Name of card tag.              |
| `created`       | String          |          | Name of card tag.              |
| `due_date`      | String          |          | Name of card tag.              |
| `planned_start` | String          |          | Name of card tag.              |
| `planned_end`   | String          |          | Name of card tag.              |


### ChecklistItem fields

| Field Name       | Type            | Required | Description                    |
|------------------|-----------------|----------|--------------------------------|
| `text`           | String          |          | Unique identifier of card tag. |
| `sort_order`     | ChecklistItem[] |          | Name of card tag.              |
| `checked`        | String          |          | Name of card tag.              |
| `created`        | String          |          | Name of card tag.              |
| `checked_at`     | String          |          | Name of card tag.              |
| `checked_by`     | String          |          | Name of card tag.              |
| `created_by`     | String          |          | Name of card tag.              |
| `due_date`       | String          |          | Name of card tag.              |
| `responsible_id` | String          |          | Name of card tag.              |


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

| Field Name      | Type         | Required | Description                                                       |
|-----------------|--------------|----------|-------------------------------------------------------------------|
| `id`            | String       | Yes      | Unique identifier for the card file.                              |
| `card_id`       | String       | Yes      | Unique identifier of card.                                        |
| `name`          | String       | Yes      | Name of card file.                                                |
| `author_id`     | String       | No       | Unique identifier of author of file.                              |
| `created`       | Null or Date | No       | Date of upload of card file                                       |
| `external`      | Boolean      | No       | Boolean value which specifiying if the storage is external or not |
| `external_type` | String       | No       | String which represents external storage type                     |
| `external_url`  | String       | No       | URL of external storage file                                      |
| `size`          | Number       | No       | Size of card file ?                                               |
| `download_url`  | String       | No       | URL of external storage file       ?                              |
| `path`          | String       | No       | URL of external storage file      ?                               |


### Description

- **id**: Unique identifier of card file.
- **card_id**: Parent card ID, where the file is attached.
- **name**: Defines the name of card file.
- **author_id**: ID of author of the attached file.
- **created**: Date of uploading card file.
- **external**: Defines if the file is from external or internal storage.
- **external_type**: Defines external storage type, available options are: gdrive, dropbox, asana.
- **external_url**: Defines url of external storage file.

### Example JSON Structure

```json
[
  {
    "id": "1207301518919127",
    "download_url": "https://asana-user-private-us-east-1.s3.amazonaws.com/assets/1207221263311720/1207301518919126/4d351afbfc3b4539fc33c5c120f808c1?X-Amz-Security-Token=IQoJb3JpZ2luX2VjECYaCXVzLWVhc3QtMSJHMEUCIQDa9bZH8HUO9dMed1lozL%2Bdqva2fCJ5FZ4DdUPL7xo9NgIgTIfrgO5s06RUWvW5Ibd0lGWfgQq6PP4OHuoS8XnrDa8qugUIj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw0MDM0ODM0NDY4NDAiDLcOaylqz5vEColJGyqOBcllPJ6xmztFdcG3UDf8QIGpHK%2BHBYtrYNMT6BsD0TfxDmIqyj0f%2FXHdq0BIWcTp7UNqY4YspbM4UiOtG98e2PK0kIZCLZ6%2B4jh4oqO%2FOGdNDfti5BA%2FcaK0iOr3yt9THcWfYYyLTlbMlJGscO7iBjn63Dzf848uaFN3z72e%2BuDirYQ7WJ20KGANzQo7CaHvtyyxoGDBc5VC6Z6QoFo1qcEmKQI5Ml%2FwySwvQfVupbPHBgnFrKhSwNyw5Ci7QDLYUtwdd1i4GnFZjpLAzsGGtpF%2FyCcjsxUVCCsaiSvSU%2FDo0uPSOke7o%2FBsOZkzub3sYb%2FTNIfpVF7fiovojXmAtAjT4JnuKd3zDbGlFw9zIQy6u6B5%2Bycp8Dlf1arizYydqOEKayQROEHSZnhlUU2TxYI7dOF397dvr2hIdKOhP5MaMhSn%2FeEvcink%2BKfyrB6EaGsetxBKxFj%2BM9dlWs3YHHO9t2yC5Hoo96VvvacngoIBGc2Qtb0svG4rCfw19ZaI3ajDEf1ReodgMDsbNCklnzLFrz8rNXzanQYkuP%2F7VF%2FmSBm0%2ByDeNFS57SyeJ3m3e%2BhPDBKrVQ2Zbxwcc3mj%2F2ZgF35eWuOmVopwl4CPRfGXkzh%2FV%2F5LMuav0ylgByYlqa7Zld2HD7bOkpEmbNlHWE2oOIV8rzibGT05RWD3nX0Q%2ByORdKKJ6598i2mDlm37DVPeCNK0USNii3vadrjJ2Hl9zSpSrTZZmyOiIS7xReGmIuJQqVaOh%2Bs1O1qAB%2F%2FjixM1GL5hQAbIdmOyD4iPz2Ox8ADm6LK%2FQSDhijkdSH2xMcC0TICcmzLqoUHLrCqzgeHXaY%2FhHA9SJTG9uhvGnxr90m0FTifTn6mHJ6orETCo142yBjqxAbFp2cr9%2BOHUsRSLARDDuW7gPB8ELHcl6IOVwRduxT%2BBKghc5rEBWLcLZjFD3%2FwdVS7gpJKN2eK5fjyLxeVeb9%2BLECh3nbM%2BrXHIVhV9MoH9M2ofzH4YCMhpsRwTA1BcNhnep10rRbjIiLur8cJ1um%2F2GhQ3fzQKSZhctmMBsoLRpHAbBgHAwInSPKZpdNzd3cLDxAChpXMSbayI57EcLpZoYB43Kx9fvZtlq8EfhI0TBQ%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240514T143645Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=ASIAV34L4ZY4PIGJ7FFE%2F20240514%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=b57496a52ee688555a6f8ea8706596b56576c43d33ffb7ac73c3ceeb16b590fb#_=_",
    "name": "Снимок экрана 2024-05-07 в 10.19.37.png",
    "size": 83562,
    "created": "2024-05-13T14:18:32.099Z",
    "card_id": "1207254524924719",
    "external": false,
    "path": "https://asana-user-private-us-east-1.s3.amazonaws.com/assets/1207221263311720/1207301518919126/4d351afbfc3b4539fc33c5c120f808c1?X-Amz-Security-Token=IQoJb3JpZ2luX2VjECYaCXVzLWVhc3QtMSJHMEUCIQDa9bZH8HUO9dMed1lozL%2Bdqva2fCJ5FZ4DdUPL7xo9NgIgTIfrgO5s06RUWvW5Ibd0lGWfgQq6PP4OHuoS8XnrDa8qugUIj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw0MDM0ODM0NDY4NDAiDLcOaylqz5vEColJGyqOBcllPJ6xmztFdcG3UDf8QIGpHK%2BHBYtrYNMT6BsD0TfxDmIqyj0f%2FXHdq0BIWcTp7UNqY4YspbM4UiOtG98e2PK0kIZCLZ6%2B4jh4oqO%2FOGdNDfti5BA%2FcaK0iOr3yt9THcWfYYyLTlbMlJGscO7iBjn63Dzf848uaFN3z72e%2BuDirYQ7WJ20KGANzQo7CaHvtyyxoGDBc5VC6Z6QoFo1qcEmKQI5Ml%2FwySwvQfVupbPHBgnFrKhSwNyw5Ci7QDLYUtwdd1i4GnFZjpLAzsGGtpF%2FyCcjsxUVCCsaiSvSU%2FDo0uPSOke7o%2FBsOZkzub3sYb%2FTNIfpVF7fiovojXmAtAjT4JnuKd3zDbGlFw9zIQy6u6B5%2Bycp8Dlf1arizYydqOEKayQROEHSZnhlUU2TxYI7dOF397dvr2hIdKOhP5MaMhSn%2FeEvcink%2BKfyrB6EaGsetxBKxFj%2BM9dlWs3YHHO9t2yC5Hoo96VvvacngoIBGc2Qtb0svG4rCfw19ZaI3ajDEf1ReodgMDsbNCklnzLFrz8rNXzanQYkuP%2F7VF%2FmSBm0%2ByDeNFS57SyeJ3m3e%2BhPDBKrVQ2Zbxwcc3mj%2F2ZgF35eWuOmVopwl4CPRfGXkzh%2FV%2F5LMuav0ylgByYlqa7Zld2HD7bOkpEmbNlHWE2oOIV8rzibGT05RWD3nX0Q%2ByORdKKJ6598i2mDlm37DVPeCNK0USNii3vadrjJ2Hl9zSpSrTZZmyOiIS7xReGmIuJQqVaOh%2Bs1O1qAB%2F%2FjixM1GL5hQAbIdmOyD4iPz2Ox8ADm6LK%2FQSDhijkdSH2xMcC0TICcmzLqoUHLrCqzgeHXaY%2FhHA9SJTG9uhvGnxr90m0FTifTn6mHJ6orETCo142yBjqxAbFp2cr9%2BOHUsRSLARDDuW7gPB8ELHcl6IOVwRduxT%2BBKghc5rEBWLcLZjFD3%2FwdVS7gpJKN2eK5fjyLxeVeb9%2BLECh3nbM%2BrXHIVhV9MoH9M2ofzH4YCMhpsRwTA1BcNhnep10rRbjIiLur8cJ1um%2F2GhQ3fzQKSZhctmMBsoLRpHAbBgHAwInSPKZpdNzd3cLDxAChpXMSbayI57EcLpZoYB43Kx9fvZtlq8EfhI0TBQ%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240514T143645Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=ASIAV34L4ZY4PIGJ7FFE%2F20240514%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=b57496a52ee688555a6f8ea8706596b56576c43d33ffb7ac73c3ceeb16b590fb#_=_"
  },
  {
    "id": "1207301518919130",
    "download_url": "https://asana-user-private-us-east-1.s3.amazonaws.com/assets/1207221263311720/1207301518919129/c59e00896b730439edabb9614c5e2926?X-Amz-Security-Token=IQoJb3JpZ2luX2VjECYaCXVzLWVhc3QtMSJHMEUCIQDa9bZH8HUO9dMed1lozL%2Bdqva2fCJ5FZ4DdUPL7xo9NgIgTIfrgO5s06RUWvW5Ibd0lGWfgQq6PP4OHuoS8XnrDa8qugUIj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw0MDM0ODM0NDY4NDAiDLcOaylqz5vEColJGyqOBcllPJ6xmztFdcG3UDf8QIGpHK%2BHBYtrYNMT6BsD0TfxDmIqyj0f%2FXHdq0BIWcTp7UNqY4YspbM4UiOtG98e2PK0kIZCLZ6%2B4jh4oqO%2FOGdNDfti5BA%2FcaK0iOr3yt9THcWfYYyLTlbMlJGscO7iBjn63Dzf848uaFN3z72e%2BuDirYQ7WJ20KGANzQo7CaHvtyyxoGDBc5VC6Z6QoFo1qcEmKQI5Ml%2FwySwvQfVupbPHBgnFrKhSwNyw5Ci7QDLYUtwdd1i4GnFZjpLAzsGGtpF%2FyCcjsxUVCCsaiSvSU%2FDo0uPSOke7o%2FBsOZkzub3sYb%2FTNIfpVF7fiovojXmAtAjT4JnuKd3zDbGlFw9zIQy6u6B5%2Bycp8Dlf1arizYydqOEKayQROEHSZnhlUU2TxYI7dOF397dvr2hIdKOhP5MaMhSn%2FeEvcink%2BKfyrB6EaGsetxBKxFj%2BM9dlWs3YHHO9t2yC5Hoo96VvvacngoIBGc2Qtb0svG4rCfw19ZaI3ajDEf1ReodgMDsbNCklnzLFrz8rNXzanQYkuP%2F7VF%2FmSBm0%2ByDeNFS57SyeJ3m3e%2BhPDBKrVQ2Zbxwcc3mj%2F2ZgF35eWuOmVopwl4CPRfGXkzh%2FV%2F5LMuav0ylgByYlqa7Zld2HD7bOkpEmbNlHWE2oOIV8rzibGT05RWD3nX0Q%2ByORdKKJ6598i2mDlm37DVPeCNK0USNii3vadrjJ2Hl9zSpSrTZZmyOiIS7xReGmIuJQqVaOh%2Bs1O1qAB%2F%2FjixM1GL5hQAbIdmOyD4iPz2Ox8ADm6LK%2FQSDhijkdSH2xMcC0TICcmzLqoUHLrCqzgeHXaY%2FhHA9SJTG9uhvGnxr90m0FTifTn6mHJ6orETCo142yBjqxAbFp2cr9%2BOHUsRSLARDDuW7gPB8ELHcl6IOVwRduxT%2BBKghc5rEBWLcLZjFD3%2FwdVS7gpJKN2eK5fjyLxeVeb9%2BLECh3nbM%2BrXHIVhV9MoH9M2ofzH4YCMhpsRwTA1BcNhnep10rRbjIiLur8cJ1um%2F2GhQ3fzQKSZhctmMBsoLRpHAbBgHAwInSPKZpdNzd3cLDxAChpXMSbayI57EcLpZoYB43Kx9fvZtlq8EfhI0TBQ%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240514T143645Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=ASIAV34L4ZY4PIGJ7FFE%2F20240514%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4f2ed1667c3a9fcbb516c8b7ce1cc0fd7dd0d730e3e21337abcf2df49ef3ec2d#_=_",
    "name": "Снимок экрана 2024-04-25 в 17.44.27.png",
    "size": 505397,
    "created": "2024-05-13T14:18:48.648Z",
    "card_id": "1207254524924719",
    "external": false,
    "path": "https://asana-user-private-us-east-1.s3.amazonaws.com/assets/1207221263311720/1207301518919129/c59e00896b730439edabb9614c5e2926?X-Amz-Security-Token=IQoJb3JpZ2luX2VjECYaCXVzLWVhc3QtMSJHMEUCIQDa9bZH8HUO9dMed1lozL%2Bdqva2fCJ5FZ4DdUPL7xo9NgIgTIfrgO5s06RUWvW5Ibd0lGWfgQq6PP4OHuoS8XnrDa8qugUIj%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw0MDM0ODM0NDY4NDAiDLcOaylqz5vEColJGyqOBcllPJ6xmztFdcG3UDf8QIGpHK%2BHBYtrYNMT6BsD0TfxDmIqyj0f%2FXHdq0BIWcTp7UNqY4YspbM4UiOtG98e2PK0kIZCLZ6%2B4jh4oqO%2FOGdNDfti5BA%2FcaK0iOr3yt9THcWfYYyLTlbMlJGscO7iBjn63Dzf848uaFN3z72e%2BuDirYQ7WJ20KGANzQo7CaHvtyyxoGDBc5VC6Z6QoFo1qcEmKQI5Ml%2FwySwvQfVupbPHBgnFrKhSwNyw5Ci7QDLYUtwdd1i4GnFZjpLAzsGGtpF%2FyCcjsxUVCCsaiSvSU%2FDo0uPSOke7o%2FBsOZkzub3sYb%2FTNIfpVF7fiovojXmAtAjT4JnuKd3zDbGlFw9zIQy6u6B5%2Bycp8Dlf1arizYydqOEKayQROEHSZnhlUU2TxYI7dOF397dvr2hIdKOhP5MaMhSn%2FeEvcink%2BKfyrB6EaGsetxBKxFj%2BM9dlWs3YHHO9t2yC5Hoo96VvvacngoIBGc2Qtb0svG4rCfw19ZaI3ajDEf1ReodgMDsbNCklnzLFrz8rNXzanQYkuP%2F7VF%2FmSBm0%2ByDeNFS57SyeJ3m3e%2BhPDBKrVQ2Zbxwcc3mj%2F2ZgF35eWuOmVopwl4CPRfGXkzh%2FV%2F5LMuav0ylgByYlqa7Zld2HD7bOkpEmbNlHWE2oOIV8rzibGT05RWD3nX0Q%2ByORdKKJ6598i2mDlm37DVPeCNK0USNii3vadrjJ2Hl9zSpSrTZZmyOiIS7xReGmIuJQqVaOh%2Bs1O1qAB%2F%2FjixM1GL5hQAbIdmOyD4iPz2Ox8ADm6LK%2FQSDhijkdSH2xMcC0TICcmzLqoUHLrCqzgeHXaY%2FhHA9SJTG9uhvGnxr90m0FTifTn6mHJ6orETCo142yBjqxAbFp2cr9%2BOHUsRSLARDDuW7gPB8ELHcl6IOVwRduxT%2BBKghc5rEBWLcLZjFD3%2FwdVS7gpJKN2eK5fjyLxeVeb9%2BLECh3nbM%2BrXHIVhV9MoH9M2ofzH4YCMhpsRwTA1BcNhnep10rRbjIiLur8cJ1um%2F2GhQ3fzQKSZhctmMBsoLRpHAbBgHAwInSPKZpdNzd3cLDxAChpXMSbayI57EcLpZoYB43Kx9fvZtlq8EfhI0TBQ%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240514T143645Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Credential=ASIAV34L4ZY4PIGJ7FFE%2F20240514%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4f2ed1667c3a9fcbb516c8b7ce1cc0fd7dd0d730e3e21337abcf2df49ef3ec2d#_=_"
  }
]
```

## Custom fields data

### Fields

| Field Name | Type                 | Required | Description                                                    |
|------------|----------------------|----------|----------------------------------------------------------------|
| `id`       | String \| Number     | Yes      | Unique identifier of field. Max length 1024 chars              |
| `type`     | String               | Yes      | Allowed types 'string','number','date','select','multi_select' |
| `name`     | String               | Yes      | Name of field. Max length 128 chars                            |
| `options`  | CustomFieldsObject[] | No       | Options of custom field                                        |


### Description

- **id**: Unique identifier of custom field.
- **type**: Defines the type of custom field, allowed types are string, number, date, select, multi_select.
- **name**: Defines the name of custom field, used for display purposes.
- **options**: Defines the available options for selected custom field type

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

### CustomFieldsObject fields

| Field Name   | Type             | Required | Description                              |
|--------------|------------------|----------|------------------------------------------|
| `id`         | String \| Number | -        | Unique identifier of custom field option |
| `value`      | String           | -        | Value of custom field option             |
| `color`      | String           | -        |                                          |
| `sort_order` | Number           | -        |                                          |


### CustomFieldsObject Description

- **id**: Unique identifier of custom field option
- **value**: Value of custom field option
- **color**: .
- **sort_order**: .

### Example JSON Structure

```json
[
  {
    "id": "1207864637859351",
    "value": "Low",
    "color": 8,
    "sort_order": 0
  }
]
```