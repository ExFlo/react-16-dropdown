react-16-dropdown
=================

A zero-dependency, lightweight and fully customizable dropdown (not select) for React. You can find examples [here](https://ankit-m.github.io/react-16-dropdown/)

# Installation

```shell
npm install --save react-16-dropdown
```

# Basic usage

```javascript
import Dropdown from 'react-16-dropdown';

const options = [{
  label: 'Prestige 🎩',
  value: 'prestige',
}, {
  label: 'Inception 😴',
  value: 'inception',
}];

<Dropdown
  align='left'
  className='custom-classname'
  closeOnEscape={true}
  options={options}
  triggerLabel='Movies 🍿'
  onClick={val => console.log(val)}
/>
```

# Supported props

You can pass the following props to the `Dropdown` component -

|Name|Default|Allowed values|Description|
|----|------|------|---|
|align|left|left, right|Decides the alignment of the menu w.r.t trigger|
|autoFocus|`false`|`Boolean`|Should the trigger be focused by default|
|className|''|`String`|Adds the given class to the wrapper element|
|closeOnClickOutside|`true`|`Boolean`|Should the dropdown menu close on clicking outside the menu|
|closeOnEscape|`true`|`Boolean`|Should the dropdown menu close on pressing Escape|
|closeOnOptionClick|`true`|`Boolean`|Should the dropdown close when option is clicked|
|disabled|`false`|`Boolean`|Disable the trigger|
|id|`undefined`|`String`|HTML attribute id for the wrapper component|
|focused|`undefined`|`String`|Default focused component in controlled mode|
|menuComponent|`Menu`⁽¹⁾ ⁽²⁾|`ReactElement`|Component to replace the default menu|
|menuPortalTarget|`body`|`String`|Selector for the portal to be attached as a child to|
|menuRenderer|`MenuRenderer`⁽¹⁾|`ReactElement`|Component to render the menu|
|menuSectionRenderer|`MenuRenderer`⁽¹⁾|`ReactElement`|Component to render menu sections|
|onClick*|`undefined`|`Function`|Handler for option click event|
|onClose|`undefined`|`Function`|Function to be called when menu closes|
|onOpen|`undefined`|`Function`|Function to be called when menu opens|
|onMenuKeyDown|`undefined`|`Function`|Function to be called when keydown event is triggered on the menu or bubbled up from option|
|onTriggerClick|`undefined`|`Function`|Function to be called when the trigger element is clicked|
|onTriggerKeyDown|`undefined`|`Function`|Function to be called when a key is pressed on the trigger|
|open|`undefined`|`Boolean`|Prop to control open/closed state of the menu|
|optionComponent|`Option`⁽¹⁾ ⁽²⁾|`ReactElement`|Component to replace the default option|
|optionRenderer|`OptionRenderer`⁽¹⁾|`ReactElement`|Component to render option|
|options*|`undefined`|`Array`|An array of objects|
|portalClassName|''|`String`|Adds the given class to portal component|
|sections|`undefined`|`Array`|Sections array for menu with sections|
|triggerComponent|`Trigger`⁽¹⁾ ⁽²⁾|`ReactElement`|Component to replace the default trigger|
|triggerLabel|Open menu|`String`|Text for the default trigger button|
|triggerRenderer|`TriggerRenderer`⁽¹⁾|`ReactElement`|Component to render the trigger|


The `options` prop is an array of objects. Each object can have the following keys -

|Key|Value|Description|
|----|------|---|
|value*|`String`|Unique identifier for each option|
|label*|<`String`|`ReactElement`>|Display label for the option|
|className|`String`|Custom class name for the option|


In case you are using sections you need to pass the `sections` prop, which is an array of objects. Each object can have the following keys -

|Key|Value|Description|
|----|------|---|
|id*|`String`|Unique identifier for each section|
|options*|`Array`|Array of options under this section|
|title|<`String`|`ReactElement`>|Title for the section|
|className|`String`|Custom class name for section|

⁽¹⁾ Default internal component

⁽²⁾ If you replace the component (instead of using renderers), you will have to pass down all the handlers, refs and other props down to your components.

\* Required props

# Customization

You can customize any part of the dropdown to suit your needs. In most cases, modifying existing classes/adding your own classes should do the trick. For advanced use cases, you can use custom render components. If you want to take over individual components of the dropdown, you can replace the `menu`, `option` or `trigger` default components.

Using renderers -
```javascript
<Dropdown
  options={colorOptions}
  triggerRenderer={() => <button className='btn btn-dark ml-2'>Option renderer</button>}
  optionRenderer={props => <div className={`option option--${props.value}`}>{props.label}</div>}
  onClick={e => console.log(e)}
/>
```

Using components -
```javascript
function CustomButtonComponent(props) {
  return (
    <a
      className='btn btn-outline-info'
      ref={props.triggerRef}
      onClick={props.onClick}
      onKeyDown={props.onKeyDown}
    >
      Custom link component
    </a>
  );
}

<Dropdown
  options={options}
  triggerComponent={CustomButtonComponent}
  onClick={e => console.log(e)}
/>
```

# Controlled Component

You can also use the dropdown as a controlled component if you pass the `open` prop.

```javascript
<Dropdown
  open={true}
  options={options}
  onTriggerClick={() => { /* do something */ }}
  onClick={e => console.log(e)}
/>
```

# Sections

Dropdown sections with titles are also supported. Although, you can only have one level of sections. Instead of the `options` array, you need to pass the `sections`, which is an  array of sections containing options. You need to pass a unique `id` for each section.

```javascript
const sections = [{
  title: 'Movies',
  id: 'movies',
  options: movieOptions,
}, {
  title: 'Fruits',
  id: 'fruits',
  options: fruitOptions,
}];

<Dropdown
  closeOnEscape
  sections={sections}
  triggerLabel='Sections'
  onClick={e => console.log(e)}
/>
```
