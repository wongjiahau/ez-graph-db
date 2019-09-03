# EZ Graph DB Specification

EZG means EZ Graph DB.

## Axioms
1. An operating system can launch multiple instances of EZG.
2. Each instance of EZG contains many nodes and edges.
3. There are two type of nodes:  
  (a) Terminal Node (TN)  
  (b) Non-terminal Node (NN)
4. There are two types of edges:  
  (a) Non-directional Edge (NE)
  (b) Directional Edge (DE)
5. Each NN can be connected by zero to many NEs or DEs.
6. Each TN can only be connected by zero to many inbound DEs.
7. Each TN carry one of the following values:
  (a) String  
  (b) Number  
  (c) Date
  (d) Boolean
8. Each NN must have a label.

## Operations
### Query
Query also means the pattern to be matched, and ad-hoc creation of variables is allowed.

Grammar:
```
Query 
  = "MATCH" Space Expr [Space ("AND" | "OR") Expr]*
  
Expr 
  = Variable 
  | NodeLabel 
  | Value 
  | Expr Edge Expr 
  | "NOT" Expr
  
Edge 
  = ">" 
  | "-"
  
Variable 
  = [a-z][a-zA-Z0-9]*
  
NodeLabel 
  = [A-Z][a-zA-Z0-9]*
  
Value 
  = INT 
  | FLOAT 
  | STRING 
  | BOOLEAN 
  | DATE
```

Example:
```
MATCH 
      a - Marries - b 
  AND Marries - On - Date("2018/07/07")
  AND b - AffairWith - c
```

```
QUERY
[ RETURN_EXPR | CREATE_EXPR | DELETE_EXPR ]
```

## Constraints
