BaseModel
=========

PHP BaseModel Class

### Basic Usage

for a simple database
```
school
 - id
 - name

classroom
 - id
 - room_number
 - school_id

teacher
 - id
 - name
 - classroom_id

student
 - id
 - name
 - classroom_id

```

```php

class School Extends BaseModel { ... }
class Student Extends BaseModel { ... }
class Teacher Extends BaseModel { ... }
class Classroom Extends BaseModel {
    protected $table = 'classroom';

    protected $relationships = array(
            'teacher' => array(self::HAS_ONE, 'Teacher', 'classroom_id'),
            'students' => array(self::HAS_MANY, 'Student', 'classroom_id'),
            'school' => array(self::BELONGS_TO, 'School', 'school_id'),
        );
}

$math = new Classroom();
echo 'School: '.$math->school->name;
echo 'Room: '.$math->room_number;
echo 'Teacher: '.$math->teacher->name;
echo 'Students: ';
foreach($math->students as $student) {
    echo ' - '.$student->name;
}
```