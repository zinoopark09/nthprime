# Final Exam Practice Set

## ROUGH BULLET POINTS ON TOPICS 
- Django
- ORM
- Swagger
- Luigi
- Descriptors
- Composition
- Inheritance
- Iterators
- Visualization
- Memoization/caching
- Dask
- Optimization
- Templating/bootstrapping
- Metaprogramming
- APIs/clients
- Data containers/structures
- DB design


### Question
**True or False?**
- SQLAlchemy allows users to interact with the database in a more SQL-like fashion than the Django ORM
- The main appeal of the Django ORM is that it is much easier to do complex joins than in pure SQL.
- Swagger is a useful tool for documenting Django Rest Framework APIs and testing endpoints

**Answer: True, False, True**

### Question
**Which Django feature is responsible for translating instances of Model classes to/from common content types like JSON, XML to communicate over an API?**  
A. Serializers  
B. Views  
C. Viewsets  
D. Routers  

**Answer: A. Serializers**

### Question

#### Name and explain 3 things that are wrong with this visualization, based on the topics we discussed in class and in sections.

![Image](visualization2.png)

** Some possible answers:**
- Data ink ratio - uneccessarily 3D which means more ink than necessary
- Gives no measure of quantity - i.e. percentage of what total?
- Not clear why the color scheme was chosen as-is
- Text for one of the slices is difficult to read

### Question
**Categorize the following based on whether they relate to prefetch_related versus select_related**

| - | prefetch_related | select_related |
| - | - | - |
| Joins involving many-to-many relationships | - | - |
| Joins completed in python | - | - |
| More efficient if on average publishers have only 1 book | - | - |  
| Returns copies of the object, not the object itself | - | - | 

### Question
Imagine the following sequence of events:  
i. You have a model as follows (as well as other code), which has already been migrated to a server/pizza-ordering application that people are using, and there is already data in the database:  
```
class PizzaTopping(models.Model):
    name = models.CharField(max_length=155)
    price = models.FloatField()
```
ii. You decide to add a field `is_premium_topping`, which flags a topping as "premium" if it costs more than $1, like this:
``` is_premium_topping=models.BooleanField()```   
iii. You try to migrate the change via the `makemigrations` and `migrate` commands.   

**Something goes wrong. What is it?**   
A. You cannot perform migrations on a model if there is already existing data and the application is live      
B. Since there is already "Pizza Toppings" data, you need to do something like make this new field nullable to temporarily handle the previously-created data   
C. You need to remove the previous PizzaToppings model, clear the data, migrate, and create a new PizzaToppings model with the new field. 
D. It is not possible to perform this migration until you write the logic/code to set "is_premium_topping" to True when price is greater than $1.

**Answer: B**


### Question

Atomic Workflows: Bulk Inserts

DB's and Parquet are both great for storing tabular data.  If your task
generates multiple rows for some input (eg a dataset of students per class,
homes per region, tweets per day, etc), what is the biggest weakness of a DB vs
Parquet with respect to an atomic, decentralized workflow?

1. Not every DB backend offers atomic writes; Django assumes the "Lowest Common
Denominator" in terms of features and you have to be careful to ensure the data
is inserted atomically, if at all.

2. Parquet is a column store, whereas a DB typically is not; therefore,
inserting multiple rows of data can be much more performant in a Parquet column
store if the data is large.

3. DB's only offer true atomic writes for single row inserts, or may behave
poorly with atomic bulk inserts.

4. Your output might legitimately contain 0 rows; there is no way know that 0
rows have been successfully inserted into a DB without storing additional
metadata

**Answer: 4**


### Question
Normalization

Would normalization of an existing database typically result in a greater,
fewer, or unchanged number of ORM models?

1. Greater
2. Fewer
3. Unchanged
4. Depends on the models - there is no general pattern

**Answer: 1**

### Question

Visualization: Grammars

A grammar of graphics:

1. Suggests when to use a particular plot, such as boxplot or scatterplot
2. Describes the optimal data-ink ratio of a given plot
3. Allows us to gain insight into the deep structure that underlies statistical data
4. Describes elements of a plot independently from their presentation

**Answer: 4**


### Question
Plotting

The following code snippet is likely to generate a graph with which problem?

```python
import numpy as np
from some_plotting_library import scatter_plot

# Create data
N = 50000
x = np.random.rand(N)
y = np.random.rand(N) + 3
colors = (0, 0, 0)
area = np.pi * 3

# Plot
scatter_plot(x, y, size=area, colors=colors, alpha=0.5)
```

1. A non-uniform, perceptually distracting colormap
2. Data privacy issues, if the data is sent to an external server
3. Over-plotting
4. Low data/ink ratio

**Answer: 3**

### Question
Out of the following, which is the best reason to use an ORM?

1. Portability across different database systems (including SQLite, Postgres and NoSQL) without refactoring code

2. Optimized queries compared to raw SQL

3. Views, routing and templating framework for rapid web development

4. Ability to work with data in Pythonic / object-oriented fashion

**Answer: 4**

### Question

Python vs SQL: SQL Frameworks

The best reason to choose SQLAlchemy over Django is:

1. It exposes more DB-specific features, without assuming the lowest common
denominator of DB features

2. The backend, in general, produces higher quality and more performant SQL

3. SqlAlchemy operates better with Flask, which is a better web framework than
the relevant web serving components of Django.  Together, the two frameworks
are considered the gold standard for serious python web applications.

4. Better ability to write arbitrary SQL code like joining tables that don't
have explicit foreign keys

**Answer: 4**

### Question
Design patterns: Custom property

Suppose we have the following method:
```python
def custom_property(func):
    @property
    @wraps(func)
    def wrapped(self):
        attr = '_' + func.__name__
        try:
            return getattr(self, attr)
        except AttributeError:
            v = func(self)
            setattr(self, attr, v)
            return v
    return wrapped

```

Which of the following design patterns best describes the provided `custom_property`
implementation?

1. descriptor
2. memoization
3. monkey patching
4. factory

**Answer: 2**
(Memoization is a technique of recording the intermediate results so that it can be used to avoid repeated calculations )

