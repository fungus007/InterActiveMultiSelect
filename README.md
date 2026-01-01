# InterActiveMultiSelect

A jQuery multiselect dropdown plugin I built for my projects. Supports checkboxes, radio buttons, search, and works great with Bootstrap modals.

![Demo](https://img.shields.io/badge/jQuery-Plugin-blue) ![License](https://img.shields.io/badge/license-MIT-green)

🔗 **[Live Demo](https://fungus007.github.io/InterActiveMultiSelect/)**

## Why I Made This

I needed a simple multiselect that:
- Shows selected items as tags (like select2 but lighter)
- Works inside Bootstrap modals without breaking
- Plays nice with ASP.NET MVC forms
- Doesn't need a ton of dependencies

So I built one.

## Quick Start

**1. Include the files**

```html
<!-- Local files -->
<link href="css/InterActiveMultiSelect.css" rel="stylesheet">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="js/InterActiveMultiSelect.js"></script>
```

**Or use CDN:**

```html
<link href="https://cdn.jsdelivr.net/gh/fungus007/InterActiveMultiSelect@v1.0.1/css/InterActiveMultiSelect.min.css" rel="stylesheet">
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/gh/fungus007/InterActiveMultiSelect@v1.0.1/js/InterActiveMultiSelect.min.js"></script>
```

**2. Create a select**

```html
<select id="mySelect" name="items" multiple>
  <option value="1">Option 1</option>
  <option value="2">Option 2</option>
  <option value="3">Option 3</option>
</select>
```

**3. Initialize**

```javascript
$('#mySelect').interActiveMultiSelect();
```

That's it.

## Options

```javascript
$('#mySelect').interActiveMultiSelect({
  mode: 'checkbox',           // 'checkbox' or 'radio'
  placeholder: 'Select...',
  search: true,               // adds search box
  searchPlaceholder: 'Type to search...',
  selectAllText: 'Select All',
  clearText: 'Clear'
});
```

| Option | Default | What it does |
|--------|---------|--------------|
| mode | 'checkbox' | Use 'radio' for single select |
| placeholder | 'Select' | Text shown when nothing selected |
| search | false | Adds a search/filter box |
| searchPlaceholder | 'Search...' | Placeholder for search input |

## With Search

```javascript
$('#employees').interActiveMultiSelect({
  search: true,
  placeholder: 'Pick employees'
});
```

## Radio Mode (Single Select)

```javascript
$('#country').interActiveMultiSelect({
  mode: 'radio',
  placeholder: 'Choose country'
});
```

## Pre-selected Values

Just add `selected` to your options:

```html
<select id="cats" multiple>
  <option value="1" selected>Already picked</option>
  <option value="2">Not picked</option>
  <option value="3" selected>Also picked</option>
</select>
```

Works great for edit forms.

## ASP.NET MVC

Standard Razor stuff:

```html
<select id="categories" name="CategoryIds" multiple>
  @foreach(var c in Model.Categories)
  {
    <option value="@c.Id" @(Model.Selected.Contains(c.Id) ? "selected" : "")>
      @c.Name
    </option>
  }
</select>

<script>
$(function(){
  $('#categories').interActiveMultiSelect();
});
</script>
```

Controller gets the values as `int[] CategoryIds` - nothing special needed.

## Inside Bootstrap Modals

Initialize when modal opens:

```javascript
$('#myModal').on('shown.bs.modal', function(){
  $('#modalSelect').interActiveMultiSelect();
});
```

## Customizing Colors

Override CSS variables:

```css
:root {
  --ias-tag-bg: #28a745;           /* tag background */
  --ias-tag-color: #fff;           /* tag text */
  --ias-focus-border: #28a745;     /* focus ring */
  --ias-item-selected-bg: #d4edda; /* selected row bg */
  --ias-checkbox-color: #28a745;   /* checkbox color */
}
```

Or scope to specific element:

```css
#mySelect + .ias-wrapper {
  --ias-tag-bg: #dc3545;
}
```

### All CSS Variables

```css
/* Button */
--ias-btn-bg: #fff;
--ias-btn-border: #ced4da;
--ias-btn-color: #212529;
--ias-btn-radius: 0.375rem;
--ias-btn-min-height: 38px;

/* Focus glow */
--ias-focus-border: #0d6efd;
--ias-focus-glow: rgba(13, 110, 253, 0.35);

/* Tags */
--ias-tag-bg: #0d6efd;
--ias-tag-color: #fff;
--ias-tag-radius: 0.25rem;

/* Dropdown */
--ias-dropdown-bg: #fff;
--ias-dropdown-border: #ced4da;
--ias-dropdown-shadow: 0 0.5rem 1rem rgba(0,0,0,0.15);

/* List items */
--ias-item-color: #212529;
--ias-item-hover-bg: #f8f9fa;
--ias-item-selected-bg: #cfe2ff;
--ias-item-selected-color: #084298;

/* Checkbox */
--ias-checkbox-color: #0d6efd;
--ias-checkbox-size: 1rem;

/* Other */
--ias-placeholder-color: #6c757d;
--ias-arrow-color: #6c757d;
--ias-select-all-color: #198754;
--ias-clear-color: #dc3545;
```

## Get Selected Values

```javascript
// array of values
var vals = $('#mySelect').val();

// listen for changes
$('#mySelect').on('change', function(){
  console.log($(this).val());
});
```

## Methods

```javascript
// destroy and restore original select
$('#mySelect').interActiveMultiSelect('destroy');

// rebuild (useful after adding options dynamically)
$('#mySelect').interActiveMultiSelect('refresh');
```

## Disabled Options

```html
<option value="2" disabled>Can't select this</option>
```

## Troubleshooting

### Dropdown gets cut off in modal

Your modal CSS probably has `overflow: hidden`. Fix:

```css
.modal .your-card-class {
  overflow: visible !important;
}
```

### Not working?

1. Make sure jQuery is loaded before the plugin
2. Check console for errors
3. Make sure select has `multiple` attribute for checkbox mode

## Files

```
├── css/
│   ├── InterActiveMultiSelect.css      (dev)
│   └── InterActiveMultiSelect.min.css  (prod, ~4kb)
├── js/
│   ├── InterActiveMultiSelect.js       (dev)
│   └── InterActiveMultiSelect.min.js   (prod, ~8kb)
└── index.html                          (demo)
```

## Browser Support

Chrome, Firefox, Safari, Edge. Should work in IE11 too but I haven't tested much.

## Changelog

### v1.0.1
- **Fixed:** Group headers now properly show/hide when using search with option groups
- **Fixed:** "Select All" and "Clear" buttons now only affect visible (filtered) items when search is active

### v1.0.0
- Initial release

## License

MIT - do whatever you want with it.

---

Made by **fungus007**
