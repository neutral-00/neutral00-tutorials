# httpd

Q. Is Coyote == Httpd?

**Yes, httpd is VERY similar to Coyote!** Both are **HTTP servers/connectors**, but with key differences:

## httpd vs Coyote Comparison

| **Aspect**       | **httpd (Apache HTTP Server)**  | **Coyote (Tomcat)**     |
| ---------------- | ------------------------------- | ----------------------- |
| **Language**     | C/C++ (native)                  | Java                    |
| **Primary Use**  | Standalone web server           | Tomcat's HTTP connector |
| **Static Files** | ⚡ Excellent (primary strength) | Good                    |
| **Performance**  | Higher throughput               | Good for Java apps      |
| **Modules**      | 100+ (mod_rewrite, mod_proxy)   | Limited                 |
| **Runs Alone**   | ✅ Yes                          | ❌ Needs Tomcat         |

## What is httpd?

**httpd** = **Apache HTTP Server** (the original Apache web server binary)

- Listens on port 80/443
- Serves static files (HTML, CSS, images) blazing fast
- Uses **mod_proxy** to forward dynamic requests to Tomcat

## Typical Production Setup

```
Browser → port 80
       ↓
[httpd - Apache HTTP Server] ← Static files (Nginx-like)
       │
       └── mod_proxy → [Tomcat port 8080]
                     ↓
                 [Coyote HTTP] → [Catalina Servlets]
```

## Code Example: httpd + Tomcat

**httpd.conf (Apache config):**

```apache
# Serve static files directly
DocumentRoot /var/www/html
<Directory /var/www/html>
    AllowOverride All
</Directory>

# Proxy dynamic requests to Tomcat
ProxyPass /app http://localhost:8080/app
ProxyPassReverse /app http://localhost:8080/app
```

**Result:** httpd (fast static) + Tomcat (Java dynamic) = **best of both worlds**

## Spring Boot Context

**Spring Boot uses EMBEDDED Tomcat:**

```
Spring Boot App (.jar)
└── Embedded Tomcat
    ├── Coyote (HTTP port 8080) ← httpd equivalent
    └── Catalina (Servlets)
```

**No separate httpd needed** - Coyote handles HTTP directly!

## When to Use Each

```
Use httpd when:
├── High traffic static sites
├── Need mod_rewrite rules
├── SSL termination
└── Load balancing

Use Coyote when:
├── Spring Boot apps (embedded)
├── Pure Java stack
└── Simpler deployments
```

## Mental Model

```
httpd = Full Apache HTTP Server (standalone)
Coyote = Tomcat's "mini-httpd" (embedded HTTP connector)

Both do: HTTP parsing → Request routing → Response serving
```

**Bottom line:** **httpd ≈ Coyote + 100 modules + native performance**. For Spring Boot, Coyote is sufficient 95% of time![1]

**Next Spring Boot question?** (Embedded Tomcat config → Custom connectors?)

[1](https://stackoverflow.com/questions/30632/difference-between-the-apache-http-server-and-apache-tomcat)
[2](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)
[3](https://www.theserverside.com/video/Tomcat-vs-Apache-HTTP-Server-Whats-the-difference)
[4](https://www.logicmonitor.com/blog/what-is-apache-tomcat-server-and-how-does-it-work)
[5](https://whatcms.org/compare/Cowboy-vs-Apache-HTTP-Server)
[6](https://www.wappalyzer.com/compare/cowboy-vs-apache-http-server/)
[7](https://opensource.com/business/16/8/top-5-open-source-web-servers)
[8](https://en.wikipedia.org/wiki/Comparison_of_web_server_software)
