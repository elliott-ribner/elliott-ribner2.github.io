## An Introduction To Relational Databases

Through the ages humans have stored records on stone tablets, and then books, and now databases! A database is an efficient way to store and retrieve large amounts of data. A database is very similar to a group of spreadsheets. Imagine we have a group of spread sheets to store student data at a very small college. The spreadsheet for the student list might have three columns: `Name`, `Gender`, and `Major`. In the database we would call these `fields` instead of Column Names as we would in the spread sheet. Additionally, in the language of databases, we would call this spreadsheet a `table`. Pretty simple so far, right?

Each row will represent a student. For instance, row one might look like `Andrew Smith | Male | Econ`. You can see that the info matches up with the `fields` we described above. In database language we would describe this row, or any row, as a `document`. If we want to return a certain document from this database we can search the table rather than looking through the spreadsheet visually. 

#### In psql, a popular database, the query (or search) to find a student in the `Students` table would look like this:
`SELECT * FROM Students WHERE Name="Andrew Smith";`

#### And would return something like this:
```
| Name         | Gender  | Major |
----------------------------------
| Andrew Smith | Male    | Econ  |
----------------------------------
```

#### Or if we searched for something with multiple results like:
`SELECT * FROM Students WHERE Major="Econ";`

#### You would get a similar response with multiple documents such as:
```
| Name         | Gender  | Major |
----------------------------------
| Andrew Smith | Male    | Econ  |
----------------------------------
| Molly Li     | Female  | Econ  |
----------------------------------
```

Very cool, right!? So that is how we can query upon a single table. Let's consider a more complex scenario where we want to view all the academic majors of the students that got any particular grade. Something like this might be useful if we wanted to run an analysis on the GPA's of different majors. Grades wouldn't easily fit into the same spreadsheet as students, and similarly the grades would not fit into the same database table. Since there are multiple grades for each student with multiple fields, it would be really messy to try to contain the grades in a single row. In the same way you might create another spreadsheet to capture the grades, we would create another table. This table, as you may have guessed, would contain some `fields` such as `Class Name`, `Grade`, `Date` and `Student Name`. We could link the two tables using the shared fields of `Name` and `Student_Name`. This means whenever we grab a student we could easily grab the grade documents for that student in one query. Similarly, if you were querying for a specific grade you could grab the student that the grade belongs to. This is done in the query by using what we call a `join`. A `join` connects two tables together so you can query two distinct, but related tables at once. 

#### A basic example of how we might view all of the grades along with the academic major in one query:
```
SELECT Students.Major, Grades.Grade, Grades.Student_Name
FROM Grades
INNER JOIN Students ON Grades.Student_Name=Students.Name;
```

#### This query would return fields `Major`, `Grade` and `Student_Name` for the grades in the database:
```
| Student_Name | Grade   | Major |
----------------------------------
| Andrew Smith | 82      | Econ  |
----------------------------------
| Molly Li     | 91      | Econ  |
----------------------------------
| Liz Lam      | 89      | Math  |
----------------------------------
```

This is a simple example but you can already start to see the power of a relational database. I hope you found the blog post useful, if you have any questions please comment below.

