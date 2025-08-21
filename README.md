# from-validation

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gorgeous Form Validation</title>
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
  <style>

    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #f8f9fa, #dbe9f4);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 580px;
    }

    .form-container {
      background: #fff;
      padding: 25px 35px;
      /* box-shadow: 0 6px 18px rgba(0,0,0,0.1); */
      max-width: 400px;
      width: 100%;
    }

    
    h1 {
      color: #cf0000;
      text-align: center;
      padding-top: 25px;
    }

    label {
      font-weight: bold;
      margin-top: 10px;
      display: block;
    }

    input, select, button {
      padding: 8px;
      margin-top: 6px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 14px;
      transition: 0.3s;
      width: 100%;
      box-sizing: border-box;
    }

    .sub{width: 30px;}

    .gen{width: 30px;}

    input:focus, select:focus { border-color: #0077b6; }

    button {
      background: #05703e;
      color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      margin-top: 15px;
      transition: 0.3s;
    }

    button:hover {
      background: #005f8a;
      transform: scale(1.05);
    }

    .error {
      color: red;
      font-size: 12px;
      margin-top: 3px;
      display: none;
      transition: 0.3s;
    }

    .popup-box {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      text-align: left;
    }

    .popup-item {
      background: #f1f9ff;
      padding: 10px;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .popup-item b {
      display: block;
      color: #005f8a;
      margin-bottom: 4px;
    }

    input.valid {
      border-color: green;
      border-width: thick;
    }

    input.invalid {
      border-color: red;
      border-width: thick;
    }

  </style>
</head>

<body>
  <div class="form-container">
    <h1>Form Validation</h1>
    <form id="form">
      <label>Name:</label>
      <input type="text" id="name" required>
      <div id="nameError" class="error">Name must be at least 3 characters</div>

      <label>Password:</label>
      <input type="password" id="password" required>
      <div id="passError" class="error">Password must be at least 6 characters</div>

      <label>Age:</label>
      <input type="number" id="age" required>

      <label>Email:</label>
      <input type="email" id="email" required>
      <div id="emailError" class="error">Enter a valid email with @</div>

      <label>Phone:</label>
      <input type="text" id="phone" required>

      <label>Gender:</label>
      <input type="radio" name="gender" class="gen" value="Male"> Male
      <input type="radio" name="gender" class="gen" value="Female"> Female <br>

      <label>Choose Country:</label>
      <select id="country">
        <option value="Bangladesh">Bangladesh</option>
        <option value="India">India</option>
        <option value="USA">USA</option>
      </select>

      <label>Choose Subject:</label>
      <input type="checkbox" name="subject" class="sub" value="Graphic"> Designer 
      <input type="checkbox" name="subject" class="sub" value="Web Development"> Development
      <input type="checkbox" name="subject" class="sub" value="Network Engineer"> Engineering
      <br>
      <button type="submit">Submit</button>
    </form>
  </div>

  <script>
    class FormValidator {
      constructor(formId) {
        this.form = document.getElementById(formId);
        this.fields = {
          name: document.getElementById("name"),
          password: document.getElementById("password"),
          email: document.getElementById("email")
        };
        this.errors = {
          name: document.getElementById("nameError"),
          password: document.getElementById("passError"),
          email: document.getElementById("emailError")
        };
        this.addEventListeners();
      }

      addEventListeners() {
        // Live validation
        this.fields.name.addEventListener("input", () => this.validateName());
        this.fields.password.addEventListener("input", () => this.validatePassword());
        this.fields.email.addEventListener("input", () => this.validateEmail());

        // Form submit
        this.form.addEventListener("submit", (e) => {
          e.preventDefault();
          if (this.validateForm()) this.showPopup();
        });
      }

      validateName() {
        const name = this.fields.name.value.trim();
        if (name.length >= 3) {
          this.fields.name.classList.add("valid");
          this.fields.name.classList.remove("invalid");
          this.errors.name.style.display = "none";
          return true;
        } else {
          this.fields.name.classList.add("invalid");
          this.fields.name.classList.remove("valid");
          this.errors.name.style.display = "block";
          return false;
        }
      }

      validatePassword() {
        const password = this.fields.password.value.trim();
        if (password.length >= 6) {
          this.fields.password.classList.add("valid");
          this.fields.password.classList.remove("invalid");
          this.errors.password.style.display = "none";
          return true;
        } else {
          this.fields.password.classList.add("invalid");
          this.fields.password.classList.remove("valid");
          this.errors.password.style.display = "block";
          return false;
        }
      }

      validateEmail() {
        const email = this.fields.email.value.trim();
        if (email.includes("@")) {
          this.fields.email.classList.add("valid");
          this.fields.email.classList.remove("invalid");
          this.errors.email.style.display = "none";
          return true;
        } else {
          this.fields.email.classList.add("invalid");
          this.fields.email.classList.remove("valid");
          this.errors.email.style.display = "block";
          return false;
        }
      }

      validateForm() {
        const validName = this.validateName();
        const validPassword = this.validatePassword();
        const validEmail = this.validateEmail();
        return validName && validPassword && validEmail;
      }

      showPopup() {
        const name = this.fields.name.value.trim();
        const password = this.fields.password.value.trim();
        const age = document.getElementById("age").value;
        const email = this.fields.email.value.trim();
        const phone = document.getElementById("phone").value.trim();
        const gender = document.querySelector('input[name="gender"]:checked')?.value || "Not Selected";
        const country = document.getElementById("country").value;
        const subjects = Array.from(document.querySelectorAll('input[name="subject"]:checked'))
                          .map(s => s.value).join(", ") || "Not Selected";

        const maskedPassword = "●".repeat(password.length);

        Swal.fire({
          title: '<span style="background:linear-gradient(red);-webkit-background-clip:text;color:transparent;">Form Submitted!</span>',
          html: `
            <div class="popup-box">
              <div class="popup-item"><b>Name</b> ${name}</div>
              <div class="popup-item"><b>Password</b> ${maskedPassword}</div>
              <div class="popup-item"><b>Age</b> ${age}</div>
              <div class="popup-item"><b>Email</b> ${email}</div>
              <div class="popup-item"><b>Phone</b> ${phone}</div>
              <div class="popup-item"><b>Gender</b> ${gender}</div>
              <div class="popup-item"><b>Country</b> ${country}</div>
              <div class="popup-item"><b>Subject(s)</b> ${subjects}</div>
            </div>
          `,
          icon: "success",
          confirmButtonText: "OK",
          confirmButtonColor: "#0077b6",
          width: 600
        }).then(() => {
          this.form.reset();
          Object.values(this.fields).forEach(f => f.classList.remove("valid", "invalid"));
        });
      }
    }

    // Initialize validator
    new FormValidator("form");
  </script>
</body>
</html>
