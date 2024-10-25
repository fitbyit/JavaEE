## 6. Create a servlet that uses cookies to store and display the number of times a user has visited the servlet.

 ###  Create the Servlet named as `visit.java` and make url-parrent as `/`
 
<img src="https://github.com/user-attachments/assets/7c537c6b-877a-4f15-a1e3-55d5271a0450" alt="image" height="280" style="width:auto;">

<img src="https://github.com/user-attachments/assets/0e5c932c-1a94-4994-8e31-9f4af517838a" alt="image" height="280" style="width:auto;">

<img src="https://github.com/user-attachments/assets/dfe102c2-ba03-491f-9cfd-ad6a98bc210e" alt="image" height="280" style="width:auto;">

###  Write the below code inside `processRequest` Method
 
```java
import jakarta.servlet.http.Cookie;

protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
    response.setContentType("text/html");

    // Retrieve cookies
    Cookie[] cookies = request.getCookies();
    int visitCount = 0;
    boolean cookieFound = false;

    // Check for the visit count cookie
    if (cookies != null) {
        for (Cookie cookie : cookies) {
            if (cookie.getName().equals("visitCount")) {
                visitCount = Integer.parseInt(cookie.getValue());
                cookieFound = true;
                break;
            }
        }
    }

    // Increment visit count
    visitCount++;

    // Set/update the cookie
    Cookie visitCookie = new Cookie("visitCount", Integer.toString(visitCount));
    visitCookie.setMaxAge(60 * 60 * 24); // 1 day
    response.addCookie(visitCookie);

    // Write the response
    response.getWriter().println("<html><body>");
    response.getWriter().println("<h2>You have visited this page " + visitCount + " time(s).</h2>");
    response.getWriter().println("</body></html>");
}
```
### Output

<img src ="https://github.com/user-attachments/assets/f2cd0e0b-7627-4041-bb7b-599e03c2082f" height ="280" width="auto" alt="image" >
