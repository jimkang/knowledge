# HTML

# How to get the boolean value of a `<input type="checkbox">` representing whether or not it is currently checked

It's the `checked` property, not `value`. e.g. `document.getElementById('send-image-raw-checkbox').checked`

# Select controls

- Get the currently selected option value with `.value`.
- Set the default option by adding a `selected` attribute (with no value) to an `<option>` element.
