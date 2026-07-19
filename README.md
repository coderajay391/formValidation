# Form Validation (Signup)

## Overview

This small frontend project demonstrates client-side form validation for a **Signup** form.
It validates the **Full Name**, **Email**, and **Password** fields in real-time (on submit) using plain JavaScript, and provides visual feedback using icons.

> Note: The UI expects Font Awesome classes (`fa-xmark`, `fa-check`) on an `<i class="fa-solid"></i>` element next to each input.

## Preview
<image src="./assets/formValidation.png"></image>

## Demo
[Demo](assets/formValidation.mp4)

## Features

- **Full Name validation**
  - Required
  - Must be in the format: _FirstName LastName_ (single space)
- **Email validation**
  - Required
  - Validates email pattern (e.g., `example@gmail.com`)
- **Password validation**
  - Required
  - Enforces a strong password pattern using a regular expression
- **User feedback**
  - Shows error messages in dedicated `<span>` elements
  - Toggles icon classes:
    - `fa-xmark` when invalid
    - `fa-check` when valid

## Project Structure

```
frontend/spireX/formValidation/
  index.html        # Signup form markup
  javascript.js     # Validation logic
  style.css         # Styling (layout, colors, background)
  assets/
    ironman.jpg     # Background image used by CSS
  READEME.md        # This documentation
```

## How it works

### 1) Submit handling

- `javascript.js` grabs the submit button (`#submitBtn`).
- On click, it prevents the default form submission.
- It runs all validators:
  - `validateName()`
  - `validateEmail()`
  - `validatePassword()`
- If **all** validations return `true`, it displays:
  - `alert("Form Submitted Successfully")`

### 2) Validation rules

#### `validateName()`

Checks the value of `#name`:

- If empty → sets `#nameError` to **"Name is required"** and adds `fa-xmark`.
- If it does not match the regex → sets **"Write full Name"** and adds `fa-xmark`.
- If valid → clears the error and adds `fa-check`.

Regex used:

- `^[A-Za-z]*\s{1}[A-Za-z]*$`

#### `validateEmail()`

Checks the value of `#email`:

- If empty → sets `#emailError` to **"Email is required"** and adds `fa-xmark`.
- If invalid pattern → sets **"Enter Valid Email"** and adds `fa-xmark`.
- If valid → clears the error and adds `fa-check`.

Regex used:

- `^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$`

#### `validatePassword()`

Checks the value of `#password`:

- If empty → sets `#passError` to **"Password is required"** and adds `fa-xmark`.
- If it does not match the strong-password regex → sets an explanatory message and adds `fa-xmark`.
- If valid → clears the error and adds `fa-check`.

Regex used:

- `^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[^a-zA-Z0-9])(?!.*\s).{8,30}$`

This enforces:

- at least **1 digit**
- at least **1 lowercase letter**
- at least **1 uppercase letter**
- at least **1 special character**
- **no spaces**
- length between **8 and 30** characters

## Setup / Run

This project is static.

1. Open: `frontend/spireX/formValidation/index.html` in a browser.
2. Fill the form fields.
3. Click **Create Account**.

## Files explained

- **`index.html`**
  - Contains the form inputs:
    - `#name`, `#email`, `#password`
  - Contains error containers:
    - `#nameError`, `#emailError`, `#passError`
  - Each input has a sibling icon element:
    - `<i class="fa-solid"></i>`

- **`javascript.js`**
  - Adds the submit click handler.
  - Implements the three validation functions.
  - Updates error text and toggles icon classes.

- **`style.css`**
  - Applies a centered card layout.
  - Uses `assets/ironman.jpg` as the page background.
  - Styles input fields and feedback text.

## Notes

- **Font Awesome dependency**: The icons rely on Font Awesome being loaded in `index.html` (or otherwise available).
- **Assets dependency**: The background image path in CSS must exist:
  - `frontend/spireX/formValidation/assets/ironman.jpg`

## Troubleshooting

- **Icons don’t appear**
  - Ensure Font Awesome is included in `index.html`.
  - Check that `fa-xmark` and `fa-check` are available in the loaded Font Awesome version.

- **Background image missing**
  - Verify `assets/ironman.jpg` exists.
  - Confirm relative path is correct from `index.html`.

- **Validation never shows success**
  - Check whether your browser blocks JavaScript (should not normally).
  - Verify input IDs match those referenced in `javascript.js`.
