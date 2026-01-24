## Actual Question Metadata

- company: LTIMindtree
- role: Fullstack Java + Angular Developer
- Date: 2025-12-14

Q. Suppose you have a list of employees. write java code to extract those employees whose salary is greater 10k and sort them by alphabetical order.

```java
List<Employee> filteredAndSortedEmployees = employees.stream()
    // Step 1: Keep only employees with salary > 10k
    .filter(employee -> employee.getSalary() > 10000)

    // Step 2: Sort alphabetically by name
    .sorted((e1, e2) -> e1.getName().compareToIgnoreCase(e2.getName()))

    // Step 3: Collect into a new list
    .collect(Collectors.toList());
```



