# Documentation

This document explains the implementation details of the **Form Validation (Signup)** project.

## Files

- `index.html`
- `style.css`
- `javascript.js`

## `index.html`

### Structure

- Contains a centered signup card.
- Each field has:
  - a label
  - an `<input>`
  - an icon container: `<i class="fa-solid"></i>`
  - an error `<span>` with a fixed id

### Important element IDs (used by JavaScript)

- `name` → input for full name
- `email` → input for email
- `password` → input for password
- `submitBtn` → submit button

### Important error elements (used by JavaScript)

- `nameError`
- `emailError`
- `passError`

## `javascript.js`

### Event flow

1. Reads DOM elements:
   - `submitBtn`, `nameError`, `emailError`, `passError`
2. Attaches a click listener:
   - `submitBtn.addEventListener("click", (e) => { ... })`
3. On click:
   - `e.preventDefault()` prevents page reload
   - Runs validations in order:
     - `validateName()`
     - `validateEmail()`
     - `validatePassword()`
   - If all are `true`, shows an alert.

### Validation helpers

Each validator follows the same pattern:

- Read the input value
- If invalid:
  - set the related error span text
  - add `fa-xmark` to the icon element (via `previousElementSibling`)
  - return `false`
- If valid:
  - clear the error text
  - add `fa-check`
  - return `true`

## Validation rules (regex)

### Name

- Must contain alphabetic text separated by exactly one space:
  - `^[A-Za-z]*\s{1}[A-Za-z]*$`

### Email

- Uses a common regex pattern for basic email format validation:
  - `^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$`

### Password

- Strong password requirements enforced by:
  - `^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[^a-zA-Z0-9])(?!.*\s).{8,30}$`

## `style.css`

### Layout

- Background image:
  - `background: url('assets/ironman.jpg') no-repeat;`
- Centered card using `position: relative`, `top: 50%`, `left: 50%`, and `transform: translate(-50%, -50%)`

### Feedback styling

- The icon (`i`) is positioned absolutely inside the `<p>` wrapper.
- Error spans are styled via:
  - `font-size: 18px; font-weight: 600; color: #90ee90;`

## Notes / Dependencies

- **Font Awesome**: The `<i class="fa-solid"></i>` element expects Font Awesome to be loaded.
- **assets/ironman.jpg**: Required by the CSS background.

## Known limitations

- Validation occurs only on submit-button click.
- Password strength message contains a small typo in UI text ("Lowecase").
