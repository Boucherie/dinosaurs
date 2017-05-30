Use SQL queries to complete the following, and save your answers into a file for submission. You can complete them in any order, if you're not sure how to approach one, move on and come back to it:

<!-- 1. Let's start by figuring out how many dinosaurs we have. Count the number of dinosaurs. -->

SELECT COUNT(name) FROM dinos;
count
-------
  331
(1 row)
<!-- 2. We want to open up our own version of Jurassic Park, but this time only with dinosaurs who are actually from the Jurassic period. Find all the dinosaurs from the Jurassic period. -->

SELECT * FROM dinos WHERE period='Jurassic';

<!-- 3. Jurassic Park was a huge success for us. Now we want to open up a sequel park: Cretaceous Park. This time though, we're a little more organized, and we want to know how much space all these dinosaurs are going to take up. Find the total sum length of all the dinosaurs from the Cretaceous period. -->


SELECT SUM(length) FROM dinos WHERE period='Cretaceous';
sum   
---------
1366.45
(1 row)


<!-- 4. Great news! Our board of investors recently secured us a large island where we can put all the dinosaurs from both Jurassic Park and Cretaceous Park. This new park will be called Juraceous Park, which according to our focus groups really rolls off the tongue. Find all the dinosaurs from either the Jurassic OR Cretaceous periods, and order them by their species name alphabetically. -->

SELECT * FROM dinos WHERE period='Jurassic' OR period='Cretaceous' ORDER BY species ASC;

<!-- 5. Saurischians are the "lizard hipped" order of dinosaurs, and one of the two main branches. All carnivorous dinosaurs are Saurischians, but not all Saurischians are carnivorous. Find all the dinosaurs from the t_order Saurischia that are Herbivorous. -->

SELECT * FROM dinos WHERE t_order='Saurischia' AND diet='Herbivorous';

<!-- 6. Dinosaur names are hard to remember. Find the shortest dinosaur, and rename it Shortie. -->

dinosaurs=# UPDATE dinos
dinosaurs-# SET name = 'Shortie'
dinosaurs-# WHERE length in(SELECT MIN(length) FROM dinos);
UPDATE 1
dinosaurs=# SELECT MIN(length) FROM dinos;

<!-- 7. It's the first day of Dino School, and we're doing roll call. Find the alphabetically first dinosaur, so we can make sure they're present for class. -->

dinosaurs=# SELECT name
dinosaurs-# FROM dinos
dinosaurs-# ORDER BY name ASC
dinosaurs-# LIMIT 1
dinosaurs-# ;
   name   
----------
 Aardonyx
(1 row)


<!-- 8. Rename the five longest dinosaurs The Famous Five. -->

dinosaurs=# UPDATE dinos
dinosaurs-# SET name = 'The Famous Five'
dinosaurs-# WHERE length in(SELECT length FROM dinos WHERE > length > 0 ORDER BY length DESC LIMIT 5);
