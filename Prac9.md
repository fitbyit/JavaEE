## 9.Develop a servlet that demonstrates session creation and destruction.

### Create `index.html` and write as below

```index.html
<html>
    <head>
        <title>Session</title>
    </head>
    <body>
        <h1>Session Practical</h1>
    <form action="welcome" method="get">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required>
        <input type="submit" value="Submit">
    </form>
    </body>
</html>
```


### Now Create a Servlet `welcome.java` and write code inside `processRequest` Method
```java
protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        try (PrintWriter out = response.getWriter()) {
            String username = request.getParameter("username");
            HttpSession session = request.getSession();
            session.setMaxInactiveInterval(30);
            Boolean isNewUser = (Boolean) session.getAttribute("isNewUser");
            if (isNewUser == null) {
                session.setAttribute("isNewUser", false);
                session.setAttribute("username", username);
                out.println("<h1>Welcome, " + username + "! This is your first visit.</h1>");
            } else {
                String previousUsername = (String) session.getAttribute("username");
                if(previousUsername==null){
                   session.invalidate();
                   response.sendRedirect("index.html");
                }
                out.println("<h1>Welcome back, " + previousUsername + "!</h1>");
                out.println("<h2> Session ID: " + session.getId() + "</h2>");
                out.println("<h3>Nice to see you again!!</h3>");
            }
        out.println("<a href='Page2'>Next Page</a><br>");
        out.println("<a href='index.html'>Login Page</a><br>");
        out.println("<a href='Logout'>Logout</a>");
        }
}
```

### Create a new Servelet `Page2.java` to Display Session Details.
```java
HttpSession session = request.getSession(false);
        if(session == null){
         response.sendRedirect("index.html");
        }
        response.setContentType("text/html;charset=UTF-8");
        try (PrintWriter out = response.getWriter()) {
            String username = (String) session.getAttribute("username");
            out.println("<h2>Session Information</h2>");
            out.println("<p>Session ID: " + session.getId() + "</p>");
            out.println("<p>Username: " + username + "</p>");
            out.println("<p>Creation Time: " + new Date(session.getCreationTime()) + "</p>");
            out.println("<p>Last Access Time: " + new Date(session.getLastAccessedTime()) + "</p>");
            out.println("<p>Max Inactive Interval: " + session.getMaxInactiveInterval() + "</p>");
            out.println("<a href='welcome'>Go to Welcome Page</a><br>");
            out.println("<a href='Logout'>Logout</a><br>");
        }
    }
```

### Create a Servlet `Logout.java` to Destory Session

```java
protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        HttpSession session = request.getSession(false); // Do not create a new session
        if (session != null) {
            session.invalidate(); // Invalidate the session
        }
        response.sendRedirect("index.html");
}
```

### Output
![image](https://github.com/user-attachments/assets/65530a45-f6ce-47d9-a429-f754ab12682a)
![image](https://github.com/user-attachments/assets/87afc817-009e-46ce-924f-e76ea650a97f)
![image](https://github.com/user-attachments/assets/4c030152-9d8c-4e88-9d3c-ff4da1fd5b9b)
![image](https://github.com/user-attachments/assets/6630f465-dac1-4a20-86df-d41a7c7df4ff)
