# JSP Implicit Objects Demonstration

This project demonstrates the use of various implicit objects available in JSP, including `request`, `response`, `session`, and `application`.

## Project Structure

- `index.jsp`: The main JSP page that utilizes implicit objects.

## JSP Code

Create a file named `index.jsp` with the following code inside body:

```jsp
    <h2>JSP Implicit Objects Demonstration</h2>

    <h3>Request Object</h3>
    <p>This request method is: <%= request.getMethod() %></p>

    <h3>Response Object</h3>
    <p>Response content type: <%= response.getContentType() %></p>

    <h3>Session Object</h3>
    <%
        String sessionId = session.getId();
        session.setAttribute("user", "John Doe");
    %>
    <p>Session ID: <%= sessionId %></p>
    <p>User in session: <%= session.getAttribute("user") %></p>

    <h3>Application Object</h3>
    <%
        application.setAttribute("appName", "JSP Demo Application");
    %>
    <p>Application Name: <%= application.getAttribute("appName") %></p>

    <h3>Additional Information</h3>
    <p>Server Info: <%= application.getServerInfo() %></p>
    <p>Servlet Context Path: <%= application.getContextPath() %></p>
```
