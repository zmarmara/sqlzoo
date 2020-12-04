# sqlzoo
_,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
Solutions to https://sqlzoo.net
_,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
       _(_      _Y_      _Y_      _Y_      _Y_      _)_
      [___]    [___]    [___]    [___]    [___]    [___]
      /:' \    /:' \    /:' \    /:' \    /:' \    /:' \
     |::   |  |::   |  |::   |  |::   |  |::   |  |::   |
     \::.  /  \::.  /  \::.  /  \::.  /  \::.  /  \::.  /
 jgs  \::./    \::./    \::./    \::./    \::./    \::./
       '='      '='      '='      '='      '='      '='

_,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
7. More Join (https://sqlzoo.net/wiki/More_JOIN_operations)
_,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_

                .-=====-.
                |_      |
                |=      |
              '=:=======:='
               /   * *   \
       ,_ .    \  '.V.'  /    ,
         >-\_  /'----'--`\  _/-<
          /  `|     *     |`  \
              \     *     /
              /'--'-'----'\
             |      *      |
             |             |
      -.-jgs--\           /---.-
               '--'---'--`
               
 _,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
 
 10. Lead actors in 1962 movies.
 List the films together with the leading star for all 1962 films. 
 
 SELECT title, name FROM
 movie JOIN casting ON movie.id=movieid 
       JOIN actor ON actor.id=actorid
 WHERE yr='1962' AND ord=1
 
 
 _,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
 
 11. Busy years for Rock Hudson
 
 Which were the busiest years for 'Rock Hudson', show the year 
 and the number of movies he made each year for any year in which he made more than 2 movies. 
 
 SELECT yr,COUNT(title) FROM
 movie JOIN casting ON movie.id=movieid
       JOIN actor   ON actorid=actor.id
 WHERE name='Rock Hudson'
 GROUP BY yr
 HAVING COUNT(title) > 2
 
 
 _,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
 
 12. Lead actor in Julie Andrews movies
 List the film title and the leading actor for all of the films 'Julie Andrews' played in.
 
 SELECT title,name FROM
 movie JOIN casting ON movie.id=movieid
      JOIN actor   ON actorid=actor.id
 WHERE ord=1 AND movieid IN (
 SELECT movieid FROM actor 
 JOIN casting ON actor.id=actorid
 WHERE name='Julie Andrews')
 
  _,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,__,.-'~'-.,_
 
 13. Actors with 15 leading roles
 Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.
 

 SELECT name FROM 
 movie JOIN casting ON movie.id=movieid 
       JOIN actor ON actorid=actor.id
 where ord=1
 GROUP BY name
 HAVING COUNT(movieid)>=15
 ORDER BY name ASC
