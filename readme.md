# Data Import Specification

This document outlines the required fields and their descriptions for importing data from various task management tools into our system. Please ensure that the provided data matches the specified formats and includes all mandatory fields for a successful import.

## Table of Contents

1. [Introduction](#introduction)
2. [General Requirements](#general-requirements)
3. [User Data](#user-data)
4. [Boards Data](#boards-data)
5. [Cards Data](#cards-data)
6. [Comments Data](#comments-data)
7. [Card files Data](#card-files-data)
8. [Error Handling](#error-handling)

## Introduction

This specification defines the structure and required fields for importing data from task management tools like Asana, Jira, Trello, etc. The goal is to ensure that the imported data can be processed correctly and integrated into our system.

## General Requirements

- **File Format**: JSON
- **Field Types**: Ensure correct data types are used (string, integer, datetime, etc.)
- **Required Fields**: All required fields must be present and non-empty.
- **Email Validation**: Email fields must contain valid email addresses.

There are some required entities that is used to process the import - boards, columns, cards

Below is represented the required fields for entities

## User Data

Description of importing process: Validates json data, if there are no validation issues, checks if the company is already existing for user, after that is checking if the user has access to some specific space, after that we are sending invite to user with default role of writer

### Fields

| Field Name  | Type   | Required | Description                               |
|-------------|--------|----------|-------------------------------------------|
| `id`        | String | Yes      | Unique identifier for the user.           |
| `full_name` | String | No       | Full name of the user.                    |
| `email`     | String | Yes      | Email address of the user. Must be valid. |
| `username`  | String | No       | Username.                                 |

### Description

- **id**: A unique identifier for the user, which is used to map and track the user within our system.
- **full_name**: The complete name of the user, used for display purposes.
- **email**: The user's email address, which must be a valid email format. This is used for communication and identification.
- **username**: Username, used for display purposes.

### Example JSON Structure

```json
{
  "id": "123456",
  "full_name": "John Doe",
  "email": "john.doe@example.com",
  "username": "johndoe"
}
```

## Boards data

### Fields

| Field Name          | Type   | Required | Description                            |
|---------------------|--------|----------|----------------------------------------|
| `id`                | String | Yes      | Unique identifier of the board.        |
| `title`             | String | Yes      | Name of the board.  Maxlength 128 char |
| `author_id`         | String | No       | Unique identifier of author of board.  |
| `column.id`         | String | Yes      | Unique identifier of column in board.  |
| `column.title`      | String | Yes      | Name of column.                        |
| `column.board_id`   | String | Yes      | Unique identifier of board.            |
| `column.sort_order` | Number | No       | .                                      |
| `column.type`       | String | No       | .   queue, done , in progress ??       |

### Description

- **id**: A unique identifier for the board, which is used to map and track the board within our system.
- **title**: The complete name of the board, used for display purposes.
- **author_id**: A unique identifier of author of board, used for display purposes.
- **column.id**: Unique identifier of column in board.
- **column.title**: The complete name of the column, used for display purposes.
- **column.board_id**: A unique identifier of board, which is used to make relation between boards and columns.
- **column.sort_order**: .
- **column.type**: Defines the actual type of column, available values are queued, in progress, done.

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

## Cards

### Fields

| Field Name         | Type         | Required | Description                               |
|--------------------|--------------|----------|-------------------------------------------|
| `id`               | String       | Yes      | Unique identifier of card.                |
| `owner_id`         | String       | Yes      | Unique identifier of owner of card.       |
| `responsible_id`   | String       | No       | Unique identifier of responsible of card. |
| `column_id`        | String       | Yes      | Unique identifier of column in board.     |
| `title`            | String       | Yes      | Name of column.  Max length 1024 chars    |
| `description`      | String       | Yes      | The description content of card           |
| `description_type` | String       | No       | Defines the type of description.          |
| `condition`        |              | No       | .                                         |
| `tags`             |              | No       | tag_name max length 128 chars ??.         |
| `history`          |              | No       | .                                         |
| `links`            |              | No       | .                                         |
| `completed`        |              | No       | .                                         |
| `completed_by`     |              | No       | .                                         |
| `properties`       |              | No       | .                                         |
| `due_date`         | Null or Date | No       | Due date of card.                         |
| `planned_start`    | Null or Date | No       | Planned start date of card.               |
| `planned_end`      | Null or Date | No       | Planned end date of card.                 |
| `created`          | Null or Date | No       | Date of creation of card .                |

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

## Comments

### Fields

| Field Name    | Type         | Required | Description                          |
|---------------|--------------|----------|--------------------------------------|
| `id`          | String       | Yes      | Unique identifier of comment.        |
| `card_id`     | String       | Yes      | Unique identifier of card.           |
| `text`        | String       | Yes      | Content of comment.                  |
| `author_name` | String       | No       | Full name of comment author.         |
| `author_id`   | String       | No       | Unique identifier of comment author. |
| `created`     | Null or Date | No       | Date od creation of comment          |

### Description

- **id**:  A unique identifier of comment, which is used to map and track the comment within our system.
- **card_id**: A unique identifier of card, under which the comment is written, which is used to map and track the comment within our system.
- **text**: Content of comment, used to display comment content.
- **author_name**: Name of the author who wrote the comment, used for display purposes
- **author_id**: A unique identifier of author for comment, used to map and track the comment, make relation to author, and display
- **created**: Date of creation the comment, or if empty by default will be used current date.

## Card files

### Fields

| Field Name      | Type         | Required | Description                          |
|-----------------|--------------|----------|--------------------------------------|
| `id`            | String       | Yes      | Unique identifier for the card file. |
| `card_id`       | String       | Yes      | Unique identifier of card.           |
| `name`          | String       | Yes      | Name of card file.                   |
| `author_id`     | String       | No       | Unique identifier of author of file. |
| `created`       | Null or Date | No       | Date of upload of card file          |
| `external`      |              | No       |                                      |
| `external_type` |              | No       | gdrive', 'dropbox', 'asana'??        |
| `external_url`  | String       | No       |                                      |


### Description

- **id**: .
- **card_id**: .
- **name**: .

## Custom fields

### Fields

| Field Name | Type   | Required | Description                               |
|------------|--------|----------|-------------------------------------------|
| `id`       | String | Yes      | Unique identifier of field. Max length 1024 |
| `type`     | String | Yes      | Allowed types 'string','number','date','select','multi_select'                            |
| `name`     | String | Yes      | Name of field.                            |

### Description

- **id**: .
- **type**: .
- **name**: .
