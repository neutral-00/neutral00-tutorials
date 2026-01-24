# Sort By Salary Desc and Map to Id

## Inteview Metadata
- Company: Emphasis
- Role: FSD
- Date: 2026-01-22

## Problem statement

Sort map2 by value(salary) in desceding order and then lookup in map 1 using key of map 2(name) and get the keys(id).
Finally create a sorted map having id as key and salary as value.

```java
import java.util.Map;
import java.util.HashMap;
import java.util.LinkedHashMap;

public class Main {
    public static void main(String[] args) {
        Map<Integer, String> map1 = new HashMap<>();
        map1.put(401,"Joesph");
        map1.put(503,"Syed");
        map1.put(206,"Anjali");
        map1.put(305,"Rakesh");
        Map<String, Double> map2 = new HashMap<>();
        map2.put("Anjali",45000.0);
        map2.put("Rakesh",63000.0);
        map2.put("Syed",60000.0);
        map2.put("Joesph",30000.0);
        
        LinkedHashMap<Integer, Double> result = new LinkedHashMap<>(); 
		//Problem Statement :
		    //1. sort the second map based on values in descending order & 
		map2.entrySet().stream()
		    .sorted(Map.Entry.<String, Double>comparingByValue().reversed())
    	    .forEach(f->{
    	        Integer foundKey = 0;
    	        String valueToFind = f.getKey();
    	        for (Map.Entry<Integer, String> entry : map1.entrySet()) {
                        if (entry.getValue().equals(valueToFind)) {
                            foundKey = entry.getKey();
                            break; // Exit the loop once the key is found
                        }
                }
    	       // System.out.println(foundKey);
    	        result.put(foundKey, f.getValue());
    	    });
		    // 2/ then map keys from first map, Please use Java8 features
		    System.out.println(result);
		
	
	//	Sample Expected Output in Map format  :
	//	503,90000.0;305,63000.0;206,45000.0 like wise....
    }
}

```

You can optimize by pre-flipping map1.
```java

// Pre-flip map1 for O(1) lookup
Map<String, Integer> nameToId = map1.entrySet().stream()
    .collect(Collectors.toMap(Map.Entry::getValue, Map.Entry::getKey));

Map<Integer, Double> result = map2.entrySet().stream()
    .sorted(Map.Entry.<String, Double>comparingByValue().reversed())
    .collect(Collectors.toMap(
        e -> nameToId.get(e.getKey()), 
        Map.Entry::getValue, 
        (v1, v2) -> v1, 
        LinkedHashMap::new
    ));
```
