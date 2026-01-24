# Tomcat

Tomcat = **HTTP Server + Servlet Container**

## Tomcat's Dual Role (Broken Down)

```
Tomcat Architecture:
┌─────────────────────┐
│     Tomcat          │
│  (Full Web Server)  │
├─────────────────────┤
│ Coyote (HTTP)       │ ← HTTP Server (handles HTTP/1.1, HTTPS)
│                     │   - Listens on port 8080
│                     │   - Parses HTTP requests
│                     │   - Serves static files (HTML/CSS/JS)
└─────────────────────┤
│ Catalina            │ ← Servlet Container
│                     │   - Manages Java servlets
│                     │   - Executes JSP pages
│                     │   - Handles servlet lifecycle
└─────────────────────┘
```

## How It Works Together

**1. HTTP Request Arrives (Coyote - HTTP Server)**

```
Browser → GET /api/users → port 8080
       ↓
   Coyote Connector receives HTTP request
       ↓
   Checks: Static file or Dynamic servlet?
```

**2. Static Content (HTTP Server handles directly)**

```
GET /styles.css → Coyote serves file directly ✅
GET /logo.png   → Coyote serves image directly ✅
```

**3. Dynamic Content (Routes to Servlet Container)**

```
GET /api/users → Coyote → Catalina → YourServlet.service() ✅
```

## Spring Boot Default Setup

```yaml
# application.yml (Tomcat embedded)
server:
  port: 8080
  tomcat:
    max-threads: 200
    min-spare-threads: 10
```

**Spring Boot auto-configures:**

```
TomcatEmbeddedServletContainerFactory
├── Coyote HTTP Connector (port 8080)
├── Catalina Servlet Engine
├── Context for your Spring MVC controllers
└── Servlet mappings (@GetMapping → servlet)
```

## Proof: Standalone HTTP Server

```bash
# Run Spring Boot → Full web server!
mvn spring-boot:run
# Visit http://localhost:8080 → Serves static + dynamic content
```

## Comparison Table

| Component               | Tomcat      | Nginx    | Node.js                |
| ----------------------- | ----------- | -------- | ---------------------- |
| **HTTP Server**         | ✅ Coyote   | ✅ Full  | ✅ http.createServer() |
| **Servlet Container**   | ✅ Catalina | ❌ No    | ❌ No                  |
| **Static Files**        | ✅ Yes      | ✅ Yes   | ✅ Yes                 |
| **Java Servlets**       | ✅ Yes      | ❌ No    | ❌ No                  |
| **Spring Boot Default** | ✅ Embedded | ❌ Proxy | ❌ Alternative         |

## Visual Request Flow

```
Browser ── HTTP ──► [Coyote HTTP Connector] ── static? ──► Static File ✅
                  │
                  └── dynamic? ──► [Catalina Servlet Container] ──► @RestController
                                                      │
                                                      └── YourService → DB
```

**Bottom line:** Tomcat **is both** - a lightweight HTTP server (Coyote) **+** Java servlet container (Catalina). That's why Spring Boot apps run standalone without external web servers![1][3]

[1](https://support.hpe.com/hpesc/public/docDisplay?docId=a00055695en_us&page=GUID-D7147C7F-2016-0901-0274-0000000005CC.html&docLocale=en_US)
[2](https://tomcat.apache.org/tomcat-3.2-doc/uguide/tomcat_ug.html)
[3](https://www.logicmonitor.com/blog/what-is-apache-tomcat-server-and-how-does-it-work)
[4](https://www.packtpub.com/en-us/learning/how-to-tutorials/overview-tomcat-6-servlet-container-part-1)
[5](https://www.geeksforgeeks.org/devops/architecture-of-apache-tomcat/)
[6](https://tomcat.apache.org/tomcat-4.1-doc/config/server.html)
[7](https://tomcat.apache.org/tomcat-5.5-doc/config/server.html)
[8](https://help.blackboard.com/Learn/Administrator/Hosting/Architecture/About_Apache_Tomcat)
[9](http://fms.b-u.ac.in/docs/config/server.html)
[10](https://www.infoworld.com/article/2265307/what-is-apache-tomcat-the-original-java-servlet-container.html)
