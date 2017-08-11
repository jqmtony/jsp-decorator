## jsp-decorator

For Apache Maven users, please add following to your pom.xml.

```
<!-- servlet-api 和jsp-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.0</version>
    <scope>provided</scope>
</dependency>
<!-- jstl标签 -->
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>
```

## Getting started

jstl.jsp

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn"%>
<%@ taglib prefix="decorator" uri="http://claudiushauptmann.com/jsp-decorator/" %>
<c:set value="${pageContext.request.contextPath }" var="contextPath"/>
```

template.jsp

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8" %>
<%@ include file="jstl.jsp"%>
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="keywords" content=""/>
    <meta name="description" content=""/>
    <link rel="shortcut icon"  href="favicon.ico"/>
    <link rel="stylesheet" type="text/css" href="${contextPath}/static/css/common.css"/>
    <script type="text/javascript" src="${contextPath}/static/js/common.js"></script>
    <decorator:placeholder name='include'/>
    <title><decorator:placeholder name='title'/>common title</title>
</head>
<script>
    $(function () {
        //common javascript code
    });
</script>
<body>
<div id="head" class="head">
    <!--common head code-->
</div>
<decorator:placeholder name='top'/>
<decorator:placeholder name='content'/>
<decorator:placeholder name='bottom'/>
<div id="footer" class="footer">
    <!--common footer code-->
</div>
</body>
<decorator:placeholder name='script'/>
</html>
```

index.jsp

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8" %>
<%@ include file="jstl.jsp"%>
<decorator:decorate filename='template.jsp'>
    <decorator:content placeholder='include'>
        <!--other include code-->
    </decorator:content>
    <decorator:content placeholder='title'>
        <!--title code-->
    </decorator:content>
    <decorator:content placeholder='top'>
        <!--top code-->
    </decorator:content>
    <decorator:content placeholder='content'>
        <!--content code-->
    </decorator:content>
    <decorator:content placeholder='bottom'>
        <!--bottom code-->
    </decorator:content>
    <decorator:content placeholder='script'>
        <script type="text/javascript">
            //javascript code
        </script>
    </decorator:content>
</decorator:decorate>
```
