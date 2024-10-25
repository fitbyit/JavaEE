##  7. Create a JSP page to demonstrate the use of Expression language.
### Create a simple from in `index.html` ass below
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Compare Values using EL</title>
</head>
<body>
    <h1>Compare Two Numbers</h1>
    <form action="result.jsp" method="post">
        <label for="a">Value A:</label>
        <input type="number" id="a" name="a" required>
        <br>
        <label for="b">Value B:</label>
        <input type="number" id="b" name="b" required>
        <br>
        <input type="submit" value="Compare">
    </form>
</body>
</html>
```

### Create `result.jsp` and write the code as below:
```jsp
<%@page contentType="text/html" pageEncoding="UTF-8" session="True" %>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>JSP Page</title>
    </head>
    <body>
        <h3>Use of EL in JSP</h3>
        <p> Number A : ${param.a} </p>
        <p> Number B : ${param.b} </p>
        <p> A+B : ${param.a + param.b} </p>
        <p> A mod B : ${param.a mod  param.b}</p>
        <p> A == B : ${param.a == param.b}</p>
        <p> A / B : ${param.a / param.b}</p>
        <p> A > B : ${param.a > param.b}</p>
    </body>
</html>
```

### Output:
![image](https://github.com/user-attachments/assets/0e0d8a99-dbcc-4490-a8c6-9762d4828fee)
![image](https://github.com/user-attachments/assets/8ef84116-b1f2-42b2-baa9-798ff4fb6dd1)

