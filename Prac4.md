### 1. **Create a Database:** Create a `table` to store user registration details.
- Create Database
  
![image](https://github.com/user-attachments/assets/57a96b4a-d882-4438-b447-bc5873970ca7)

- Create Table

![image](https://github.com/user-attachments/assets/c4530b91-12c8-40e2-be51-455b103a8235)


## Add the MySql J Connector.jar file in project
- Adding Jar in Database Services

![Jar GIF](https://raw.githubusercontent.com/fitbyit/JavaEE/main/img/jar.gif)

- Adding Jar in Project Library
  
![Jar GIF](https://raw.githubusercontent.com/fitbyit/JavaEE/main/img/jar2.gif)

### 2. Create the Login Jsp Page `(login.jsp)` with code as below.
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.sql.*" %>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <form action="login.jsp" method="post">
        Username: <input type="text" name="username"><br>
        Password: <input type="password" name="password"><br>
        <input type="submit" value="Login">
    </form>

    <%
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        if (username != null && password != null) {
            Connection conn = null;
            PreparedStatement stmt = null;
            ResultSet rs = null;

            try {
                Class.forName("com.mysql.cj.jdbc.Driver");
                conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbprac", "root", "");
                stmt = conn.prepareStatement("SELECT * FROM userinfo WHERE username = ? AND password = ?");
                stmt.setString(1, username);
                stmt.setString(2, password); 
                rs = stmt.executeQuery();

                if (rs.next()) {
                    session.setAttribute("username", username);
                    response.sendRedirect("modify.jsp");
                } else {
                    out.println("<p>Invalid username or password</p>");
                }
            } catch (Exception e) {
                out.println("<h1>Error: " + e.getMessage() + "</h1>");
            } 
        }
    %>
</body>
</html>
```

> Here we had stored username in HttpSession if Username and Password Matches from Database

### 3. Create Modify Registration Details Page `(modify.jsp)`
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.sql.*" %>
<%@ page session="true" %>
<!DOCTYPE html>
<html>
<head>
    <title>Modify Registration Details</title>
</head>
<body>
    <h2>Modify Registration Details</h2>

    <%
        String username = (String) session.getAttribute("username");
        if (username == null) {
            response.sendRedirect("login.jsp");
            return;
        }

        Connection conn = null;
        PreparedStatement stmt = null;
        ResultSet rs = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbprac", "root", "");
            stmt = conn.prepareStatement("SELECT * FROM users WHERE username = ?");
            stmt.setString(1, username);
            rs = stmt.executeQuery();

            if (rs.next()) {
                String email = rs.getString("email");
                String fullName = rs.getString("full_name");
    %>
                <form method="post">
                    Email: <input type="text" name="email" value="<%= email %>"><br>
                    Full Name: <input type="text" name="fullName" value="<%= fullName %>"><br>
                    <input type="submit" value="Update">
                </form>
    <%
            }

            if (request.getMethod().equalsIgnoreCase("post")) {
                String newEmail = request.getParameter("email");
                String newFullName = request.getParameter("fullName");

                stmt = conn.prepareStatement("UPDATE users SET email = ?, full_name = ? WHERE username = ?");
                stmt.setString(1, newEmail);
                stmt.setString(2, newFullName);
                stmt.setString(3, username);
                stmt.executeUpdate();
                out.println("<p>Details updated successfully!</p>");
            }
        } catch (Exception e) {
            out.println("<h1>Error: " + e.getMessage() + "</h1>");
        } finally {
            rs.close();
            conn.close():
          }
    %>
</body>
</html>
```
