# User Registration Servlet

This project demonstrates a servlet that accepts user registration details (Username, Password, Email, Country) from an HTML form and stores these details in a database using JDBC.

## Project Structure

- `registration.html`: HTML form for user registration.
- `RegisterServlet.java`: Java servlet to handle registration.

## HTML Body Code

Create a file named `registration.html` with the following body content:

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
        
        <input type="submit" value="Register">
    </form>
</body>
```

## Create Databse `dbprac` and  Table as `users`
- Create Database
  
![image](https://github.com/user-attachments/assets/57a96b4a-d882-4438-b447-bc5873970ca7)

- Create Table

![image](https://github.com/user-attachments/assets/b07f43d0-dd64-492f-bf0e-2c59fdb1d5f2)


## Add the MySql J Connector.jar file in project
- Adding Jar in Database Services

![Jar GIF](https://raw.githubusercontent.com/fitbyit/JavaEE/main/img/jar.gif)

- Adding Jar in Project Library
  
![Jar GIF](https://raw.githubusercontent.com/fitbyit/JavaEE/main/img/jar2.gif)


## `doPost` Method Code

Create a file named `RegisterServlet.java` and include the following `processRequest` method:


```java
import java.sql.*

 protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    String email = request.getParameter("email");
    String country = request.getParameter("country");

    response.setContentType("text/html");
    PrintWriter out = response.getWriter();

    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/dbprac", "root", "");
        String sql = "INSERT INTO users (username, password, email, country) VALUES (?, ?, ?, ?)";
        PreparedStatement pstmt = conn.prepareStatement(sql);
        pstmt.setString(1, username);
        pstmt.setString(2, password);
        pstmt.setString(3, email);
        pstmt.setString(4, country);

        int rowsInserted = pstmt.executeUpdate();
        if (rowsInserted > 0) {
            out.println("<h1>Registration Successful!</h1>");
        } else {
            out.println("<h1>Registration Failed.</h1>");
        }
        pstmt.close();
        conn.close();
    } catch (Exception e) {
        out.println("<h1>Error: " + e.getMessage() + "</h1>");
    } finally {
        out.close();
    }
}
```

### Output:
![Outpu GIF](https://raw.githubusercontent.com/fitbyit/JavaEE/main/img/outputdb.gif)


