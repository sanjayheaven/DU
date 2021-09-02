# Components

- **Less is Better**

# To do

## 1.x.x

- to realize the basic use of the more components & templates
- to improve documentation that show how to use

## 2.x.x

- try Vue3.x, maybe use another library

# Classification

## Basic

- button
- radioGroup
- checkboxGroup
- switch
- table
- input
- card
- select
- field
- pagination
- tag
- tooptip

# How to create/update a component

- **Document First**
- Confirm Properties (props,slots)
- Code

# Note

## Card

### Properties

| Name    | Type        | Desc |
| ------- | ----------- | ---- |
| title   | slot,String |      |
| extra   | slot        |      |
| header  | slot        |      |
| content | slot        |      |
| footer  | slot        |      |

## Input

[MDN-input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input)  
[MDN-textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)

### Properties

| Name          | Type     | Desc                             |
| ------------- | -------- | -------------------------------- |
| type          | String   | text,textarea,number,password    |
| value/v-model | String   |                                  |
| rows          | Number   | only when 'type' is textarea     |
| disabled      | Boonlean |                                  |
| readonly      | Boonlean |                                  |
| placeholder   | String   |                                  |
| autosize      | Boonlean | default:true (only for textarea) |

## RadioGroup

### Properties

| Name          | Type     | Desc                              |
| ------------- | -------- | --------------------------------- |
| type          | String   | can be radio(default) or 'button' |
| value/v-model | String   |                                   |
| options       | [Object] | {lable,value}                     |
| change        | Function |                                   |

## Button

### Properties

| Name     | Type     | Desc                    |
| -------- | -------- | ----------------------- |
| label    | String   |                         |
| disabled | Boonlean |                         |
| click    | Function |                         |
| type     | Function | primary(default),danger |

## Select

- native option' style can not be modified
- select will relized by ul&li

### Properties

| Name        | Type     | Desc          |
| ----------- | -------- | ------------- |
| searchable  | Boonlean |               |
| placeholder | String   |               |
| options     | [Object] | {lable,value} |
| change      | Function |               |

## Switch

### Properties

| Name          | Type     | Desc |
| ------------- | -------- | ---- |
| value/v-model | Boonlean |      |
| change        | Function |      |

## Table

### Properties

| Name      | Type     | Desc                      |
| --------- | -------- | ------------------------- |
| data      | [Object] |                           |
| columns   | [Object] | {lable,value:slot/String} |
| draggable | Boonlean |                           |

## Dialog

### Properties

| Name         | Type        | Desc           |
| ------------ | ----------- | -------------- |
| show/v-model | Boonlean    |                |
| title        | slot,String |                |
| showFooter   | Boonlean    | default：false |
| header       | slot        |                |
| footer       | slot        |                |
| content      | slot        |                |

## Slider

### Properties

| Name          | Type   | Desc           |
| ------------- | ------ | -------------- |
| value/v-model | Number | default：1-100 |

## Field

### Properties

| Name     | Type        | Desc          |
| -------- | ----------- | ------------- |
| title    | slot,String |               |
| required | Boonlean    | default false |

## Pagination

### Properties

| Name            | Type     | Desc          |
| --------------- | -------- | ------------- |
| current/v-model | Number   | default:1     |
| total           | Number   |               |
| pageSize        | Number   | default:10    |
| change          | Function | (current)=>{} |

## Tag

### Properties

| Name     | Type     | Desc          |
| -------- | -------- | ------------- |
| closable | Boonlean | default:false |
| close    | Function | (current)=>{} |

## Tooltip

### Properties

| Name      | Type   | Desc                                                                                                           |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------- |
| label     | String |                                                                                                                |
| placement | String | top(default) left right bottom topLeft topRight bottomLeft bottomRight leftTop leftBottom rightTop rightBottom |
