# LINQ Cheat Sheet (.NET)

Quick reference for common LINQ (Language Integrated Query) operations in C#.

---

## 📄 Basic Syntax

```csharp
var result = from item in collection
             where item.Property == value
             select item;
```

OR using method syntax:

```csharp
var result = collection.Where(item => item.Property == value);
```

---

## 🔍 Filtering

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Where            | `list.Where(x => x.Age > 30)`                   |
| OfType           | `objects.OfType<string>()`                      |

---

## 📊 Projection

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Select           | `list.Select(x => x.Name)`                      |
| SelectMany       | `list.SelectMany(x => x.Children)`              |

---

## 🔢 Ordering

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| OrderBy          | `list.OrderBy(x => x.Name)`                     |
| OrderByDescending| `list.OrderByDescending(x => x.Score)`          |
| ThenBy           | `list.OrderBy(x => x.Name).ThenBy(x => x.Age)` |

---

## 🧮 Aggregation

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Count            | `list.Count()`                                  |
| Sum              | `list.Sum(x => x.Amount)`                       |
| Average          | `list.Average(x => x.Age)`                      |
| Min / Max        | `list.Min(x => x.Price)`                        |

---

## 🔗 Joining

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Join             | `list1.Join(list2, a => a.Id, b => b.Id, (a, b) => ...)` |
| GroupJoin        | `categories.GroupJoin(products, c => c.Id, p => p.CategoryId, (c, p) => ...)` |

---

## 📦 Grouping

```csharp
var groups = list.GroupBy(x => x.Category);
```

---

## 🧪 Quantifiers

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Any              | `list.Any(x => x.IsActive)`                     |
| All              | `list.All(x => x.IsValid)`                      |
| Contains         | `list.Contains(value)`                          |

---

## 🔄 Element Operations

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| First / FirstOrDefault | `list.First(x => x.IsReady)`            |
| Single / SingleOrDefault | `list.Single(x => x.Id == 1)`        |
| Last / LastOrDefault   | `list.LastOrDefault()`                 |
| ElementAt / ElementAtOrDefault | `list.ElementAt(2)`            |

---

## 🧹 Set Operations

| Operation         | Example                                         |
|------------------|-------------------------------------------------|
| Distinct         | `list.Distinct()`                               |
| Union            | `list1.Union(list2)`                            |
| Intersect        | `list1.Intersect(list2)`                        |
| Except           | `list1.Except(list2)`                           |

---

## 🧠 Useful Tips

- Use `ToList()` or `ToArray()` to execute queries immediately.
- LINQ queries are **lazy** by default — they only execute when enumerated.
- Use `.AsQueryable()` to enable LINQ-to-Entities in EF.

