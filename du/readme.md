# Components

- **Less is Better**
- **Document First**

# To do

- Slider
- Date
- Layout

## 1.x.x

- to realize the basic use of the more components & templates
- to improve documentation that show how to use

## 2.x.x

- try Vue3.x / React, maybe use another Repo,

# 1.x.x Classification

## Basic

- Button

### Button

| Name     | Type     | Desc                    |
| -------- | -------- | ----------------------- |
| label    | String   |                         |
| disabled | Boonlean |                         |
| click    | Function |                         |
| type     | Function | primary(default),danger |

## Display

- Card
- Dialog
- Pagination
- Progress
- Table
- Tabs
- Tag
- Tooltip

### Card

| Name    | Type        | Desc |
| ------- | ----------- | ---- |
| title   | Slot,String |      |
| extra   | Slot        |      |
| header  | Slot        |      |
| content | Slot        |      |
| footer  | Slot        |      |

### Dialog

| Name         | Type        | Desc           |
| ------------ | ----------- | -------------- |
| show/v-model | Boonlean    |                |
| title        | Slot,String |                |
| showFooter   | Boonlean    | default：false |
| header       | Slot        |                |
| footer       | Slot        |                |
| content      | Slot        |                |

### Pagination

| Name            | Type     | Desc          |
| --------------- | -------- | ------------- |
| current/v-model | Number   | default:1     |
| total           | Number   |               |
| pageSize        | Number   | default:10    |
| change          | Function | (current)=>{} |

### Progress

| Name          | Type   | Desc           |
| ------------- | ------ | -------------- |
| value/v-model | Number | range in 1-100 |

### Table

| Name      | Type     | Desc                      |
| --------- | -------- | ------------------------- |
| data      | [Object] |                           |
| columns   | [Object] | {lable,value:Slot/String} |
| draggable | Boonlean |                           |

### Tabs

| Name    | Type     | Desc          |
| ------- | -------- | ------------- |
| options | [Object] | {lable,value} |

### Tag

| Name     | Type     | Desc          |
| -------- | -------- | ------------- |
| closable | Boonlean | default:false |
| close    | Function | (current)=>{} |

### Tooltip

| Name      | Type   | Desc                                                                                                           |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------- |
| label     | String |                                                                                                                |
| placement | String | top(default) left right bottom topLeft topRight bottomLeft bottomRight leftTop leftBottom rightTop rightBottom |

## Form

- Cascader
- CheckboxGroup
- Field(form-item)
- Form
- Input
- RadioGroup
- Select
- Slider
- Switch

### Cascader

| Name        | Type     | Desc          |
| ----------- | -------- | ------------- |
| placeholder | String   |               |
| options     | [Object] | {lable,value} |
| change      | Function |               |

### CheckboxGroup

| Name        | Type     | Desc          |
| ----------- | -------- | ------------- |
| placeholder | String   |               |
| options     | [Object] | {lable,value} |
| change      | Function |               |

### Field

| Name          | Type        | Desc                  |
| ------------- | ----------- | --------------------- |
| value/v-model | String      | default show as Input |
| title         | Slot,String |                       |
| required      | Boonlean    | default false         |

### Input

| Name          | Type     | Desc                             |
| ------------- | -------- | -------------------------------- |
| type          | String   | text,textarea,number,password    |
| value/v-model | String   |                                  |
| rows          | Number   | only when 'type' is textarea     |
| disabled      | Boonlean |                                  |
| readonly      | Boonlean |                                  |
| placeholder   | String   |                                  |
| autosize      | Boonlean | default:true (only for textarea) |

### RadioGroup

| Name          | Type     | Desc                              |
| ------------- | -------- | --------------------------------- |
| type          | String   | can be radio(default) or 'button' |
| value/v-model | String   |                                   |
| options       | [Object] | {lable,value}                     |
| change        | Function |                                   |

### Select

- native option' style can not be modified
- select will relized by ul&li

| Name        | Type     | Desc          |
| ----------- | -------- | ------------- |
| searchable  | Boonlean |               |
| placeholder | String   |               |
| options     | [Object] | {lable,value} |
| change      | Function |               |

### Slider

| Name          | Type   | Desc           |
| ------------- | ------ | -------------- |
| value/v-model | Number | default：1-100 |

### Switch

| Name          | Type     | Desc |
| ------------- | -------- | ---- |
| value/v-model | Boonlean |      |

## Layout

### Notification

- Alert
- Message
- Confirm
