### 5. Create a servlet that accepts at least six user registration details and displays them on another page after submission.

1. **Create the HTML File**: Create a file named `registration.html` and paste the HTML body code into it.

```html
<body>
    <h2>User Registration</h2>
    <form action="RegisterServlet" method="post">
        <label for="username">Username:</label><br>
        <input type="text" id="username" name="username" required><br><br>

        <label for="password">Password:</label><br>
        <input type="password" id="password" name="password" required><br><br>

        <label for="email">Email:</label><br>
        <input type="email" id="email" name="email" required><br><br>

        <label for="country">Country:</label><br>
        <input type="text" id="country" name="country" required><br><br>

        <label for="age">Age:</label><br>
        <input type="number" id="age" name="age" required><br><br>

        <label for="gender">Gender:</label><br>
        <select id="gender" name="gender" required>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
        </select><br><br>

        <input type="submit" value="Register">
    </form>
</body>
```

2. **Create the Servlet**: Create a file named `RegisterServlet.java` with the `processRequest` method code into it.

```java
protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    String email = request.getParameter("email");
    String country = request.getParameter("country");
    String age = request.getParameter("age");
    String gender = request.getParameter("gender");

    response.setContentType("text/html");
    PrintWriter out = response.getWriter();

    out.println("<html><body>");
    out.println("<h2>User Registration Details</h2>");
    out.println("<p>Username: " + username + "</p>");
    out.println("<p>Password: " + password + "</p>");
    out.println("<p>Email: " + email + "</p>");
    out.println("<p>Country: " + country + "</p>");
    out.println("<p>Age: " + age + "</p>");
    out.println("<p>Gender: " + gender + "</p>");
    out.println("</body></html>");
    
    out.close();
}
```
