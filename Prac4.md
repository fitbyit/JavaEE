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
<html>
<head>
    <title>Update Details</title>
</head>
<body>
    
    <h2>Modify User Details</h2>
    <%
        String username = (String) session.getAttribute("username");
        if (username == null) {
            response.sendRedirect("login.jsp");
            return;
        }
        
        Connection conn = null;
        PreparedStatement stmt = null;
        ResultSet rs = null;

        String email = "";
        String name = "";

        try{
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbprac", "root", "");
            String sql = "SELECT * FROM userinfo WHERE username=?";
            stmt = conn.prepareStatement(sql);
            stmt.setString(1, username);
            rs = stmt.executeQuery();

            if (rs.next()) {
                email = rs.getString("email");
                name = rs.getString("full_name");
            }
        } catch (Exception e) {
            out.println("<h1> Error " + e.getMessage() + "</h1>");
        }
    %>
    
    <form method="post">
        Email: <input type="email" name="email" value="<%= email %>" required /><br />
        Name: <input type="text" name="name" value="<%= name %>" required /><br />
        <input type="submit" value="Update" />
    </form>
    
    <form method="post" action="logout.jsp">
        <input type="submit" value="Logout" />
    </form>

    <%
        String newEmail = request.getParameter("email");
        String newName = request.getParameter("name");

        if (newEmail != null && newName != null) {
            try {
                String sql = "UPDATE userinfo SET email=?, full_name=? WHERE username=?";
                stmt = conn.prepareStatement(sql);
                stmt.setString(1, newEmail);
                stmt.setString(2, newName);
                stmt.setString(3, username);
                stmt.executeUpdate();
                response.sendRedirect("updateSuccess.jsp");
            } catch (Exception e) {
                out.println("<h1> Error " + e.getMessage() + "</h1>");
            }
        }
    %>
</body>
</html>
```
### 3. Create UpdateSucess Page `(updateSuccess.jsp)`
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<html>
<head>
    <title>Update Successful</title>
</head>
<body>
    <h1>Your details have been updated successfully!</h1>
    <a href="modify.jsp">Go back</a>
</body>
</html>
```

### 5. Create a Logout Page  `logout.jsp`
```jsp
<%@ page language="java" session="true" %>
<%
    session.invalidate(); // Invalidate the session
    response.sendRedirect("login.jsp"); 
%>
```


