# Simple Login Servlet
Q.1 Write a servlet that accepts a username and password from an HTML form. 
    If the credentials are correct (e.g., username: "admin", password: "password"), display "Hello <username>". 
    Otherwise, display "Login failed".

## Project Structure

- `login.html`: HTML form for user input.
- `LoginServlet.java`: Java servlet handling the login logic.

## HTML Form Code

Create a file named `login.html` with the following code inside body:

```html
    <h2>Login</h2>
    <form action="LoginServlet" method="post">
        <label for="username">Username:</label><br>
        <input type="text" id="username" name="username" required><br><br>
        <label for="password">Password:</label><br>
        <input type="password" id="password" name="password" required><br><br>
        <input type="submit" value="Login">
    </form>
```

## Servlet Code

Create a file named `LoginServlet.java` with the following code inside processRequest Method:

```java
String username = request.getParameter("username");
String password = request.getParameter("password");
response.setContentType("text/html");
PrintWriter out = response.getWriter();
if ("admin".equals(username) && "password".equals(password)) {
    out.println("<h1>Hello " + username + "</h1>");
}
else {
  out.println("<html><body style='background-color: red; color: white;'>");
  out.println("<h1>Login failed</h1>");
  out.println("</body></html>");
}
```

### Ouput
![image](https://github.com/user-attachments/assets/73f529f8-f899-47d0-b678-4bbe089704ef)
![image](https://github.com/user-attachments/assets/472ae60a-c89c-4fad-8620-306f16b3f409)
![image](https://github.com/user-attachments/assets/86a83bb4-2a90-44a0-b3e6-77186a9fa594)




