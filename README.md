[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=14796464&assignment_repo_type=AssignmentRepo)
<h1 align="center">StylusDB SQL</h1>
<p align="center">
A SQL database engine written in JavaScript

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-green.svg)](https://github.com/ChakshuGautam/stylusdb-sql)
[![GitHub Repo](https://img.shields.io/github/stars/ChakshuGautam/stylusdb-sql?style=social)](https://github.com/ChakshuGautam/stylusdb-sql)
</p>

This is the base repository for cohort members to follow the tutorial and send in their own StylusDB SQL implementations. You can refer to a complete implementation @ [ChakshuGautam/stylusdb-sql](https://github.com/ChakshuGautam/stylusdb-sql).

Follow the steps given in the documentation to create your own implementation and make those tests pass.

> **Disclaimer**:
This database is for educational purposes only. It is not intended for production use. It is written ground up in JavaScript and is a great way to learn how databases work. You can find the tutorial in the [docs](./docs) directory.

### Features
- [x] Support for [Prisma](https://www.prisma.io/)
- [x] `INSERT`, `DELETE`, `SELECT`
- [x] CLI
- [x] Server/Client Basic Protocol
- [x] NPM Package for StylusDB-SQL
- [ ] `UPDATE`, `CREATE TABLE`, `DROP TABLE`
- [ ] SQL Spec Tracker
- [ ] Minimal PostgreSQL Protocol for Server/Client Communication

### Installation

```bash
npm i stylusdb-sql
```

### Usage

#### SELECT
Assuming you have a CSV file called `student.csv` with the following data:
```
id,name,age
1,John,25
2,Jane,25
```
```javascript
const { executeSELECTQuery } = require('stylusdb-sql');
const query = 'SELECT id, name FROM student WHERE age = 25';
const result = await executeSELECTQuery(query);

// result = [{ id: '1', name: 'John' }, { id: '2', name: 'Jane' }]
```

#### INSERT
```javascript
const { executeINSERTQuery } = require('../src/queryExecuter');
const { readCSV, writeCSV } = require('../src/csvReader');
async function createGradesCSV() {
    const initialData = [
        { student_id: '1', course: 'Mathematics', grade: 'A' },
        { student_id: '2', course: 'Chemistry', grade: 'B' },
        { student_id: '3', course: 'Mathematics', grade: 'C' }
    ];
    await writeCSV('grades.csv', initialData);
}
await createGradesCSV();
const insertQuery = "INSERT INTO grades (student_id, course, grade) VALUES ('4', 'Physics', 'A')";
await executeINSERTQuery(insertQuery);
```

Verify the new entry in `grades.csv`:
```csv
student_id,course,grade
1,Mathematics,A
2,Chemistry,B
3,Mathematics,C
4,Physics,A
```

#### DELETE
```javascript
async function createCoursesCSV() {
    const initialData = [
        { course_id: '1', course_name: 'Mathematics', instructor: 'Dr. Smith' },
        { course_id: '2', course_name: 'Chemistry', instructor: 'Dr. Jones' },
        { course_id: '3', course_name: 'Physics', instructor: 'Dr. Taylor' }
    ];
    await writeCSV('courses.csv', initialData);
}
 await createCoursesCSV();

// Execute DELETE statement
const deleteQuery = "DELETE FROM courses WHERE course_id = '2'";
await executeDELETEQuery(deleteQuery);

// Verify the course was removed
const updatedData = await readCSV('courses.csv');
const deletedCourse = updatedData.find(course => course.course_id === '2');
```

### CLI Usage

Open a terminal and run the following command to start the CLI:
```bash
stylusdb-sql-lordgrm18
```
Execute a query as shown below.
<img src="https://github.com/ChakshuGautam/stylusdb-sql/blob/36245e339c192028a0f4e60274deebc38b190496/docs/tutorials/assets/tutorial-19.gif?raw=true" />


### npm package

The npm package is available @ [stylusdb-sql-lordgrim](https://www.npmjs.com/package/stylusdb-sql-lordgrim)

### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md)