
# jQuery Validation Rules with Input Masking

Small demo showing how to combine `jQuery Validation` with `Inputmask` (vanilla & jQuery builds) to validate user input and ensure masked fields are complete before submission.

This repository contains a single static demo (`index.html`) that demonstrates common validation rules (required fields, email, password confirmation, file restrictions) together with input masks for phone number, date, and SSN.

## Features

- Uses `jQuery Validation` (validate + additional-methods) for form validation.
- Uses `Inputmask` (jQuery binding) to provide masked inputs and a custom validator method that checks mask completeness.
- Example validations included:
	- Required fields
	- Email format
	- Password and confirm password
	- Masked phone, birth date (`dd/mm/yyyy`), SSN
	- File inputs with extension, per-file size and total size limits, and max files count

## Files

- `index.html` - The demo page with the registration form and inline scripts initializing input masks and jQuery Validation.
- `masking/jquery.inputmask.min.js` - Inputmask jQuery plugin used by the demo.
- `masking/inputmask.min.js` - (included in the repo but commented out in `index.html`) standalone Inputmask build.

## Usage

Open `index.html` in a browser (no server required) and interact with the registration form. The page includes CDN links for Bootstrap, jQuery and jQuery Validation; the Inputmask files are loaded from the local `masking/` folder.

How it works (high level):

1. Input masks are applied with `$(':input').inputmask()` which activates any `data-inputmask` attributes on the inputs.
2. A custom validation method `masked` is registered using `$.validator.addMethod(...)` which returns true if the field is optional or the Inputmask reports the field as complete via `inputmask('isComplete')`.
3. `$.validator.classRuleSettings.masked = { masked: true }` ensures elements with class `masked` are validated automatically.
4. The form is initialized with `$('#registrationForm').validate()` and uses some default settings (debug mode on, custom wrapper and error class).

## Example inputs shown in the demo

- Phone: `(999) 999-9999` mask
- Birth Date: alias `datetime` with `inputFormat: 'dd/mm/yyyy'`
- SSN: `999-99-9999` mask
- Profile picture: accepts `jpg,png`, max 1MB
- Portfolio: multiple images, max 3 files, combined size max 3MB

## Custom validation notes

- The demo registers a `masked` rule which is used to ensure masked fields are fully entered before considering them valid.
- File inputs in the demo include `data-rule-extension`, `data-rule-maxfiles`, `data-rule-maxsize`, and `data-rule-maxsizetotal` attributes so the included jQuery Validation Additional Methods can pick them up (these attributes follow the convention used by the additional methods plugin).

## How to re-use in your project

1. Include jQuery, `jquery.validate.min.js` and `additional-methods.min.js`.
2. Include `jquery.inputmask.min.js` (or the standalone build) and call `$(':input').inputmask()` after the DOM is ready.
3. Add `class="masked"` to inputs you want to validate for mask completeness and ensure they have `data-inputmask` attributes describing the mask.
4. Register the `masked` rule exactly as in `index.html` or copy the snippet into your scripts so `$.validator` knows how to treat masked inputs.

## Development / Extending

- Turn off `debug: true` in the `jQuery.validator.setDefaults` to allow the form to submit after passing validation.
- If you prefer the standalone Inputmask build, uncomment the `masking/inputmask.min.js` include and remove the jQuery binding file.
- Consider adding explicit server-side validation for any submitted files and sensitive inputs (SSN, birth date) — masks and client-side validation are only for UX and convenience.

## License

This repository has no license specified. Add a `LICENSE` file if you want to apply an open source license.

## Acknowledgements

- jQuery Validation plugin - https://jqueryvalidation.org/
- Inputmask - https://github.com/RobinHerbots/Inputmask
