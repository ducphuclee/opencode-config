# Cypher Query Examples for GitNexus

## Basic Patterns

### Find Callers
```cypher
MATCH (a)-[:CodeRelation {type: 'CALLS'}]->(b:Function {name: "targetFunction"})
RETURN a.name, a.filePath
```

### Find Callees
```cypher
MATCH (a:Function {name: "sourceFunction"})-[:CodeRelation {type: 'CALLS'}]->(b)
RETURN b.name, b.filePath
```

### Trace Call Chain (1-3 levels)
```cypher
MATCH path = (a)-[:CodeRelation {type: 'CALLS'}*1..3]->(b:Function {name: "target"})
RETURN [n IN nodes(path) | n.name] AS chain
```

### Find Community Members
```cypher
MATCH (f)-[:CodeRelation {type: 'MEMBER_OF'}]->(c:Community)
WHERE c.heuristicLabel = "Auth"
RETURN f.name
```

### Trace Process Steps
```cypher
MATCH (s)-[r:CodeRelation {type: 'STEP_IN_PROCESS'}]->(p:Process)
WHERE p.heuristicLabel = "UserLogin"
RETURN s.name, r.step ORDER BY r.step
```

## Advanced Patterns

### Find All Paths Between Two Functions
```cypher
MATCH path = (start:Function {name: "funcA"})-[:CodeRelation {type: 'CALLS'}*1..5]->(end:Function {name: "funcB"})
RETURN [n IN nodes(path) | n.name] AS chain
```

### Find Hot Paths (Many Callers)
```cypher
MATCH (caller)-[:CodeRelation {type: 'CALLS'}]->(target:Function)
WITH target, count(caller) AS callerCount
WHERE callerCount > 5
RETURN target.name, callerCount
ORDER BY callerCount DESC
```

### Find External Dependencies
```cypher
MATCH (f:Function)-[:CodeRelation {type: 'CALLS'}]->(ext)
WHERE ext.filePath CONTAINS "node_modules" OR ext.filePath CONTAINS "vendor"
RETURN f.name, ext.name, ext.filePath
```

## Tips

- Use `*1..3` for variable path length (1 to 3 hops)
- Filter by `confidence` for high-confidence relationships only
- Use `heuristicLabel` for human-readable community/process names
- Always check `filePath` to disambiguate common names
