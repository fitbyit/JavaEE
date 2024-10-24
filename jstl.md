# 1. Core Tag JSTL
### Usage

```jsp
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/core" %>
```


 | **Tag**         | **Attributes**                                                   | **Description**                                      |
|------------------|-----------------------------------------------------------------|------------------------------------------------------|
| `<c:out>`        | `value`                                                         | Outputs the value.                                   |
|                  | `default`                                                       | Default value if `value` is null.                   |
|                  |                                                                 |                                                      |
| `<c:set>`        | `var`                                                           | Name of the variable to set.                         |
|                  | `value`                                                         | Value to assign to the variable.                     |
|                  | `scope`                                                         | Scope of the variable (page, request, session, application). |
|                  |                                                                 |                                                      |
| `<c:if>`         | `test`                                                          | Boolean expression to evaluate.                      |
|                  |                                                                 |                                                      |
| `<c:choose>`     | (No attributes)                                                 | Contains `<c:when>` and `<c:otherwise>` for conditional logic. |
|                  |                                                                 |                                                      |
| `<c:when>`       | `test`                                                          | Boolean expression for this case.                    |
|                  |                                                                 |                                                      |
| `<c:otherwise>`  | (No attributes)                                                 | Executes if no preceding `<c:when>` conditions are met. |
|                  |                                                                 |                                                      |
| `<c:forEach>`    | `items`                                                         | Collection or array to iterate over.                 |
|                  | `var`                                                           | Variable for each item in the collection.           |
|                  | `begin`                                                         | Starting index (optional).                           |
|                  | `end`                                                           | Ending index (optional).                             |
|                  | `step`                                                          | Increment for each iteration (optional).            |
|                  |                                                                 |                                                      |
| `<c:import>`     | `url`                                                          | URL to import content from.                          |
|                  | `var`                                                           | Name of the variable to store imported content (optional). |
|                  |                                                                 |                                                      |
| `<c:redirect>`   | `url`                                                          | URL to redirect to (typically not part of JSTL core). |
|                  |                                                                 |                                                      |
| `<c:remove>`     | `var`                                                           | Name of the variable to remove.                      |
|                  | `scope`                                                         | Scope of the variable (optional).                    |


**Example of**  `c:set` and `c:out`
```html
<p>
    <c:set var="channelName" value="Miss Xing" scope="page" ></c:set>
    <c:out value="${channelName}"></c:out> <br/>
    <c:out value="${channelName1}" default="Default Value"></c:out> <br/>
    <c:out value="${channelName2}">Here is another way to set Default Value</c:out> <br/>
</p>
<p>
    Escape XML demo: <br/>
    <c:set var="paragraph" value="<p>This is Escape XML demo</p>"></c:set>
    <c:out value="${paragraph}"></c:out>
    <c:out value="${paragraph}" escapeXml="false"></c:out>
</p>
```

**Example of**  `c:if`
```java
<c:set var="age" value="70" />
<c:if test="${age > 65}">
    <p>Retired: Age > 65</p>
</c:if>

<c:if test="${! (age <= 65)}">
    <p>Retired: Age > 65</p>
</c:if>
```

**Example of**  `c:choose`
```jsp
<c:set var="salary" value="1"></c:set>

<c:choose>
    <c:when test="${salary > 9000}">
        <p>Paid High</p>
    </c:when>
    <c:when test="${salary <= 9000 && salary > 1}">
        <p>Paid Normal</p>
    </c:when>
    <c:otherwise>
        <p>No comment</p>
    </c:otherwise>
</c:choose>
```

**Example of**  `c:ForEach` and `c:forTokens`
```jsp
<c:forEach var = "i" begin = "1" end = "5">
  Item <c:out value = "${i}"/><p>
</c:forEach>

<c:forTokens items = "Zara,nuha,roshy" delims = "," var = "name">
  User: <c:out value = "${name}"/><p>
</c:forTokens>
```


# 2. Formatting Tag JSTL
### Usage

```jsp
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/fmt" %>
```


| **Tag**         | **Attributes**                                                   | **Description**                                      |
|------------------|-----------------------------------------------------------------|------------------------------------------------------|
| `<fmt:message>`  | `key`                                                          | Key for the message in a resource bundle.           |
|                  | `bundle`                                                       | Name of the resource bundle (optional).              |
|                  | `var`                                                          | Name of the variable to store the message (optional). |
|                  |                                                                 |                                                      |
| `<fmt:formatNumber>` | `value`                                                     | The number to format.                                |
|                  | `pattern`                                                      | The pattern to format the number.                    |
|                  | `var`                                                          | Name of the variable to store the formatted number (optional). |
|                  |                                                                 |                                                      |
| `<fmt:formatDate>` | `value`                                                      | The date to format.                                  |
|                  | `pattern`                                                      | The pattern to format the date.                      |
|                  | `var`                                                          | Name of the variable to store the formatted date (optional). |
|                  |                                                                 |                                                      |
| `<fmt:parseDate>`  | `value`                                                     | The date string to parse.                            |
|                  | `pattern`                                                      | The pattern used for parsing the date.               |
|                  | `var`                                                          | Name of the variable to store the parsed date (optional). |
|                  |                                                                 |                                                      |
| `<fmt:formatTime>` | `value`                                                     | The time to format.                                  |
|                  | `pattern`                                                      | The pattern to format the time.                      |
|                  | `var`                                                          | Name of the variable to store the formatted time (optional). |
|                  |                                                                 |                                                      |
| `<fmt:setLocale>` | `value`                                                      | The locale to set (e.g., en_US, fr_FR).             |
|                  |                                                                 |                                                      |
| `<fmt:bundle>`    | `baseName`                                                  | Base name of the resource bundle.                    |
|                  | `var`                                                          | Name of the variable to store the bundle (optional). |


**Example**

```jsp
<%@ page import="java.time.LocalDateTime" %>
<%@ page import="java.util.Date" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<html>
<head>
    <title>JSTL Formatting Tag Library Demo</title>
</head>
<body>
<c:set var="amount" value="5728.9869"></c:set>
<fmt:parseNumber value="${amount}" integerOnly="true"/> <br/>
<fmt:parseNumber value="${amount}" type="number"></fmt:parseNumber> <br/>

<fmt:formatNumber value="${amount}" type="currency"/> <br/>
<fmt:setLocale value="zh_CN"></fmt:setLocale>
<fmt:formatNumber value="${amount}" type="currency"/> <br/>

<c:set var="today" value="16-10-2020"/>
<fmt:parseDate value="${today}" pattern="dd-MM-yyyy"/><br/>

<fmt:setLocale value="en_US"></fmt:setLocale>
<%--<c:set var="now" value="<%=LocalDateTime.now()%>"/>--%>
<c:set var="now" value="<%= new Date()%>"/>
<fmt:formatDate value="${now}" type="time" /><br/>
</body>
</html>
```



# 3. JSTL SQL Tag Attributes

### Usage

```jsp
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/sql" %>
```

## `<sql:query>`

| **Attribute**   | **Description**                                      |
|------------------|------------------------------------------------------|
| `dataSource`     | The data source to use for the query.                |
| `var`            | The name of the variable to store the result set.     |
| `scope`          | The scope of the variable (optional, defaults to page). |
| `timeout`        | Timeout in seconds for the query execution (optional). |
| `fetchSize`      | The number of rows to fetch (optional).               |
| `maxRows`        | Maximum number of rows to return (optional).          |
| `type`           | Type of the result set (optional).                    |

---

## `<sql:update>`

| **Attribute**   | **Description**                                      |
|------------------|------------------------------------------------------|
| `dataSource`     | The data source to use for the update.               |
| `var`            | The name of the variable to store the update count (optional). |
| `scope`          | The scope of the variable (optional, defaults to page). |
| `timeout`        | Timeout in seconds for the update execution (optional). |

---

## `<sql:insert>`

| **Attribute**   | **Description**                                      |
|------------------|------------------------------------------------------|
| `dataSource`     | The data source to use for the insert operation.     |
| `var`            | The name of the variable to store the insert count (optional). |
| `scope`          | The scope of the variable (optional, defaults to page). |
| `timeout`        | Timeout in seconds for the insert execution (optional). |

---

## `<sql:delete>`

| **Attribute**   | **Description**                                      |
|------------------|------------------------------------------------------|
| `dataSource`     | The data source to use for the delete operation.     |
| `var`            | The name of the variable to store the delete count (optional). |
| `scope`          | The scope of the variable (optional, defaults to page). |
| `timeout`        | Timeout in seconds for the delete execution (optional). |

---

## `<sql:param>`

| **Attribute**   | **Description**                                      |
|------------------|------------------------------------------------------|
| `name`           | The name of the parameter to set.                    |
| `value`          | The value of the parameter.                          |
| `type`           | The SQL type of the parameter (optional).            |


**Example:** Set DataSource
```jsp
    <c:catch var="sqlError">
    <sql:setDataSource var="ds"
                       driver="com.mysql.cj.jdbc.Driver"
                       url="jdbc:mysql://localhost:3306/dbprac"
                       user="root" password=""/>
</c:catch>
    <c:if test="${not empty sqlError}">
    <h2>Error Occurred:</h2>
    <p>${sqlError}</p>
</c:if>
```

**Example:**  `sql:query`
```jsp
<sql:query dataSource="${ds}" var="rs"> 
SELECT * FROM users; 
</sql:query> 
<c:forEach var="student" items="${rs.rows}">
  ${student.username} ${student.email}<br> 
</c:forEach> 
```

**Example:**  `sql:update`
```jsp
<sql:update dataSource="${ds}" var="rs"> 
    UPDATE users SET username=? WHERE password=?; 
    <sql:param>TestUser</sql:param>
    <sql:param>huhuh</sql:param>
</sql:update>
<c:if test="${rs==1}"> 
    Updated Successfully!
</c:if>
```

**Example:**  `dateParam`
```jsp    
<sql:dateParam value="<%=new Date() %>"/>
```

**Example:**  `sql:transaction`
```jsp 
<sql:transaction dataSource="${ds}">
    <sql:update var="rs">
        INSERT INTO student_details VALUES(?,?);
        <sql:param>105</sql:param>
        <sql:param>Jyoti</sql:param> 
    </sql:update> 
    <sql:update var="rs">
        DELETE FROM student_details WHERE student_id=?;
        <sql:param>101</sql:param>
    </sql:update>
</sql:transaction>
```


# # 3. JSTL Functions Tag 

### Usage

```jsp
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
```

In JSTL (JavaServer Pages Standard Tag Library), the `<fn:>` tag is part of the Function Library, providing various functions to manipulate data.

| Function              | Description                                       | Example Usage                                |
|-----------------------|---------------------------------------------------|----------------------------------------------|
| `fn:concat`           | Concatenates two or more strings.                 | `<c:out value="${fn:concat('Hello, ', name)}"/>` |
| `fn:length`           | Returns the length of a string or collection.     | `<c:out value="${fn:length(list)}"/>`      |
| `fn:substring`        | Returns a substring of a string.                   | `<c:out value="${fn:substring(name, 0, 3)}"/>` |
| `fn:toUpperCase`     | Converts a string to upper case.                   | `<c:out value="${fn:toUpperCase(name)}"/>` |
| `fn:toLowerCase`     | Converts a string to lower case.                   | `<c:out value="${fn:toLowerCase(name)}"/>` |
| `fn:trim`            | Removes leading and trailing whitespace from a string. | `<c:out value="${fn:trim(name)}"/>`      |
| `fn:contains`         | Checks if a string contains a specified sequence.  | `<c:if test="${fn:contains(description, 'test')}">...</c:if>` |
| `fn:startsWith`       | Checks if a string starts with a specified prefix. | `<c:if test="${fn:startsWith(name, 'A')}">...</c:if>` |
| `fn:endsWith`         | Checks if a string ends with a specified suffix.   | `<c:if test="${fn:endsWith(name, 'son')}">...</c:if>` |
| `fn:replace`          | Replaces occurrences of a substring within a string. | `<c:out value="${fn:replace(text, 'old', 'new')}"/>` |





