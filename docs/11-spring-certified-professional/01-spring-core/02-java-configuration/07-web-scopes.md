# Web Scoped Beans

## Let's have a demo to understand the web scoped beans

## Project Metadata

- repository: `$gp/pocs/poc-springboot`
- branch named `bean-scope-demo`

## Steps

1. create a package name `scope`
1. inside it create a bean named `RequestScopedBean`
   - decorate the class with
     - `@Component`
     - `@Scope(value = WebApplicationContext.SCOPE_REQUEST, proxyMode = ScopedProxyMode.TARGET_CLASS)`
1. inside it create a bean named `SessionScopedBean`
   - decorate the class with
     - `@Component`
     - `@Scope(value = WebApplicationContext.SCOPE_SESSION, proxyMode = ScopedProxyMode.TARGET_CLASS)`
   - let the class the following fields
     - `private int visitCount = 0`
   - let the class have the following methods:
     - `public int incrementVisit(){return ++visitCount;}`
1. Create a RestController named `WebScopeDemoController`
   - define the fields:
     - requestScopedBean
     - sessionScoppedBean
   - define the methods
     - demoScopes()
       - annotate it with `@GetMapping("/scopes")`
       - return the strings:
         - "Request UUID : " + requestScopedBean.getUuid()
         - "Session Visits: " + sessionScopedBean.incrementVisit();
