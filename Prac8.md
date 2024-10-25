## 8. Create a servlet application that functions as a basic calculator.

### Step 1: Create `index.html`
Create a file named `index.html` your project:
```html
<head>
    <title>Basic Calculator</title>
</head>
<body>
    <h1>Basic Calculator</h1>
    <form action="calculator" method="post">
        <label for="number1">Number 1:</label>
        <input type="text" id="number1" name="number1" required><br><br>
        <label for="number2">Number 2:</label>
        <input type="text" id="number2" name="number2" required><br><br>
        <label for="operation">Operation:</label>
        <select id="operation" name="operation" required>
            <option value="add">Add</option>
            <option value="subtract">Subtract</option>
            <option value="multiply">Multiply</option>
            <option value="divide">Divide</option>
        </select><br><br>
        <input type="submit" value="Calculate">
    </form>
</body>
</html>
```

### Create the Servlet `calculator.java`
write the below code inside `processRequest` Method

```java
protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        String number1Str = request.getParameter("number1");
        String number2Str = request.getParameter("number2");
        String operation = request.getParameter("operation");

        double result = 0;
        String errorMessage = "";

        if (number1Str != null && number2Str != null && operation != null) {
            try {
                double number1 = Double.parseDouble(number1Str);
                double number2 = Double.parseDouble(number2Str);

                switch (operation) {
                    case "add":
                        result = number1 + number2;
                        break;
                    case "subtract":
                        result = number1 - number2;
                        break;
                    case "multiply":
                        result = number1 * number2;
                        break;
                    case "divide":
                        if (number2 != 0) {
                            result = number1 / number2;
                        } else {
                            errorMessage = "Cannot divide by zero.";
                        }
                        break;
                    default:
                        errorMessage = "Invalid operation.";
                }
            } catch (NumberFormatException e) {
                errorMessage = "Invalid input. Please enter valid numbers.";
            }
        }

        out.println("<html><body>");
        out.println("<h1>Calculation Result</h1>");
        if (!errorMessage.isEmpty()) {
            out.println("<p style='color:red;'>" + errorMessage + "</p>");
        } else {
            out.println("<h2>Result: " + result + "</h2>");
        }
}
```
### Output:
<img src = "https://github.com/user-attachments/assets/6bc6da0e-8b9f-410c-865c-fc41045ee4da" heigth="200" width="auto">
<img src = "https://github.com/user-attachments/assets/46f33cf3-76cf-47ff-b6ab-8f9f76b84645" heigth="200" width="auto">


