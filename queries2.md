## Group by:
1-Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(id), YEAR(enrolment_date) FROM students GROUP BY YEAR(enrolment_date);
``````````````````````````````
2-Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(id), office_address FROM teachers GROUP BY office_address;
``````````````````````````````
3-Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(vote), exam_id FROM exam_student GROUP BY exam_id;
``````````````````````````````
4-Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(id), department_id FROM degrees GROUP BY department_id;
``````````````````````````````````````````````````````````````````````````````````````````
## Join:
1-Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.`name`, `students`.`surname`, `students`.`date_of_birth`, `students`.`registration_number`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name`= 'Corso di Laurea in Economia';
``````````````````````````````
2-Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `courses.name`, `courses.period`, `courses.year`, `courses.cfu`, `courses.website`, `degrees.level`, `departments.name` 
FROM `courses`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN departments ON `degrees`.`department_id` = `departments.id`
WHERE `degrees`.`level` = 'magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';
``````````````````````````````
3-Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.*, `teachers`.`name`, `teachers`.`surname`, `teachers`.`id`
FROM `courses`
JOIN `course_teacher` ON `course`.`id` = `course_teacher`.`courses_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = 'Fulvio' AND `teachers`.`surname` = 'Amato'
``````````````````````````````
4-Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.name, students.surname, degrees.name, departments.name
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.name, students.surname;
``````````````````````````````
5-Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT degrees.name, courses.name, courses.period, courses.year, courses.cfu, teachers.name, teachers.surname
FROM degrees
JOIN courses ON degrees.id = courses.degree_id
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
``````````````````````````````
6-Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT teachers.*
FROM teachers
JOIN course_teacher ON teachers.id = course_teacher.teacher_id
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Matematica';
``````````````````````````````
7-BONUS: Selezionare per ogni studente quanti tentativi d???esame ha sostenuto per superare ciascuno dei suoi esami