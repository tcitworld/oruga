---
title: Select
---

# Select

> Select an item in a dropdown list. Use with Field to access all functionalities

---

<a href="https://github.com/oruga-ui/oruga/edit/develop/packages/docs/../oruga/src/components/select/examples/Select.md" class="docgen-edit-link">edit on github</a>

## Examples

### Base

::: demo

```html
<template>
  <section>
    <o-field label="Simple">
      <o-select placeholder="Select a name">
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Grouped">
      <o-select placeholder="Select a character" icon="user">
        <optgroup label="Black Sails">
          <option value="flint">Flint</option>
          <option value="silver">Silver</option>
          <option value="vane">Vane</option>
          <option value="billy">Billy</option>
          <option value="jack">Jack</option>
        </optgroup>

        <optgroup label="Breaking Bad">
          <option value="heisenberg">Heisenberg</option>
          <option value="jesse">Jesse</option>
          <option value="saul">Saul</option>
          <option value="mike">Mike</option>
        </optgroup>

        <optgroup label="Game of Thrones">
          <option value="tyrion-lannister">Tyrion Lannister</option>
          <option value="jamie-lannister">Jamie Lannister</option>
          <option value="daenerys-targaryen">Daenerys Targaryen</option>
          <option value="jon-snow">Jon Snow</option>
        </optgroup>
      </o-select>
    </o-field>

    <o-field label="Error" variant="danger" message="Something went wrong with this field">
      <o-select placeholder="Select a character">
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Rounded">
      <o-select placeholder="Select a character" rounded>
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Disabled">
      <o-select placeholder="Select a character" disabled>
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Disabled option">
      <o-select placeholder="Select a character">
        <option value="flint">Flint</option>
        <option value="silver" disabled>Silver</option>
      </o-select>
    </o-field>

    <o-field label="Expanded">
      <o-select placeholder="Select a character" expanded>
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Size 'large'">
      <o-select placeholder="Large" size="large">
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </o-select>
    </o-field>

    <o-field label="Multiple">
      <o-select multiple native-size="8" v-model="selectedOptions">
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
        <option value="vane">Vane</option>
        <option value="billy">Billy</option>
        <option value="jack">Jack</option>
        <option value="heisenberg">Heisenberg</option>
        <option value="jesse">Jesse</option>
        <option value="saul">Saul</option>
        <option value="mike">Mike</option>
      </o-select>
    </o-field>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        selectedOptions: []
      }
    }
  }
</script>
```

:::

## Props

| Prop name          | Description                                                 | Type                                   | Values                                            | Default                                                  |
| ------------------ | ----------------------------------------------------------- | -------------------------------------- | ------------------------------------------------- | -------------------------------------------------------- |
| expanded           | Makes input full width when inside a grouped or addon field | boolean                                | -                                                 |                                                          |
| rounded            | Makes the element rounded                                   | boolean                                | -                                                 |                                                          |
| icon               | Icon name to be added                                       | string                                 | -                                                 |                                                          |
| iconPack           | Icon pack to use                                            | string                                 | `mdi`, `fa`, `fas and any other custom icon pack` |                                                          |
| autocomplete       | Native options to use in HTML5 validation                   | string                                 | -                                                 |                                                          |
| maxlength          | Same as native maxlength, plus character counter            | number\|string                         | -                                                 |                                                          |
| useHtml5Validation | Enable html 5 native validation                             | boolean                                | -                                                 | Config -> <code> "useHtml5Validation": true</code>       |
| statusIcon         | Show status icon using field and variant prop               | boolean                                | -                                                 | Config -> <code> "statusIcon": true</code>               |
| validationMessage  | The message which is shown when a validation error occurs   | string                                 | -                                                 |                                                          |
| v-model            |                                                             | string\|number\|boolean\|object\|array | -                                                 | null                                                     |
| size               | Vertical size of input, optional                            | string                                 | `small`, `medium`, `large`                        |                                                          |
| iconRight          | Icon name to be added on the right side                     | string                                 | -                                                 | Config -> <code> 'select.iconRight': 'caret-down'</code> |
| placeholder        | Text when nothing is selected                               | string                                 | -                                                 |                                                          |
| multiple           |                                                             | boolean                                | -                                                 |                                                          |
| nativeSize         | Same as native size                                         | string\|number                         | -                                                 |                                                          |

## Class props

| Prop name        | Description | Type   | Values | Default |
| ---------------- | ----------- | ------ | ------ | ------- |
| rootClass        |             | string | -      |         |
| iconsLeftClass   |             | string | -      |         |
| iconsRightClass  |             | string | -      |         |
| roundedClass     |             | string | -      |         |
| multipleClass    |             | string | -      |         |
| emptyClass       |             | string | -      |         |
| expandedClass    |             | string | -      |         |
| iconLeftClass    |             | string | -      |         |
| iconRightClass   |             | string | -      |         |
| sizeClass        |             | string | -      |         |
| variantClass     |             | string | -      |         |
| placeholderClass |             | string | -      |         |

## Events

| Event name | Type      | Description |
| ---------- | --------- | ----------- |
| blur       | undefined |
| focus      | undefined |

## Slots

| Name    | Description | Bindings |
| ------- | ----------- | -------- |
| default |             |          |

## Style

| CSS Variable                         | SASS Variable                  | Default                                               |
| ------------------------------------ | ------------------------------ | ----------------------------------------------------- |
| --oruga-select-background-color      | \$select-background-color      | #fff                                                  |
| --oruga-select-border-color          | \$select-border-color          | \$grey-lighter                                        |
| --oruga-select-border-width          | \$select-border-width          | 1px                                                   |
| --oruga-select-border-style          | \$select-border-style          | solid                                                 |
| --oruga-select-border-radius         | \$select-border-radius         | \$base-border-radius                                  |
| --oruga-select-rounded-border-radius | \$select-rounded-border-radius | \$base-rounded-border-radius                          |
| --oruga-select-box-shadow            | \$select-box-shadow            | none                                                  |
| --oruga-select-color                 | \$select-color                 | #363636                                               |
| --oruga-select-icon-zindex           | \$select-icon-zindex           | 4                                                     |
| --oruga-select-font-size             | \$select-font-size             | \$base-font-size                                      |
| --oruga-select-height                | \$select-height                | \$control-height                                      |
| --oruga-select-line-height           | \$select-line-height           | \$base-line-height                                    |
| --oruga-select-margin                | \$select-margin                | 0                                                     |
| --oruga-select-max-width             | \$select-max-width             | 100%                                                  |
| --oruga-select-width                 | \$select-width                 | 100%                                                  |
| --oruga-select-placeholder-opacity   | \$select-placeholder-opacity   | \$base-disabled-opacity                               |
| --oruga-select-padding               | \$select-padding               | $control-padding-vertical $control-padding-horizontal |
